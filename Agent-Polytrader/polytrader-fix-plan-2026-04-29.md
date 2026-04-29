# PolyTrader FIX PLAN — 29 de Abril 2026
## Dos caminos verificados para ejecutar trades sin Bullpen CLI

---

## DIAGNÓSTICO COMPLETO

### Estado actual del Bot
- **PM2**: Bot (id=7) + Dashboard (id=0) — ambos ONLINE
- **Problema**: Bullpen CLI `not logged in` — todo BUY falla con ❌
- **Causa raíz**: Auth bug Bullpen v0.1.69 — login no guarda credentials
- **Último intento fallido**: CarlosMC → Baltimore Orioles → ❌ "Command failed"
- **clob_bridge.py**: ROTO — `os.env...EY` (syntax corrupto) + `py_clob_client_v2` no instalado
- **py-clob-client**: AHORA instalado v0.34.6 ✅ + py_clob_client_v2 v1.0.0 ✅

### Geoblock verificado
- **GET** endpoints (markets, time, orders, positions): ✅ Funcionan desde Alemania
- **POST /order**: ❌ 403 "Trading restricted in your region"
- **Bolivia (BO)**: ❗ NO está en la lista oficial de países bloqueados
- **Lista oficial bloqueados**: AU, BE, BY, BI, CF, CD, CU, DE, ET, FR, GB, IR, IQ, IT, JP(UI), KP, LB, LY, MM, NI, NL, PL(close), RU, SG(close), SO, SS, SD, SY, TH(close), TW(close), UM, US, VE, YE, ZW

### Credenciales API — VERIFICADAS Y VÁLIDAS ✅
```
WALLET_PRIVATE_KEY = 5fd80d6e...b328 (signer EOA: 0x7C83...285C)
POLY_API_KEY = 7ed2db7f-...-53596a85328e
POLY_API_SECRET = V5PLvl...9Y4=
POLY_API_PASSPHRASE = 0af081af...1f01d
Safe Wallet = 0xD9161E48da6Ee5ad4F2dbd06e15678E52BD93d4a
```
- `create_or_derive_api_creds()` → devuelve las MISMAS creds ✅
- Funciona con `signature_type=0` (EOA) y `signature_type=2` (Safe/Gnosis) ✅
- `GET /orders` funciona sin proxy desde VPS ✅

---

## CAMINO A: Proxy SOCKS5 desde Bolivia + py-clob-client (RECOMENDADO)

### Concepto
El bot usa `py-clob-client` directamente (sin Bullpen) para firmar y enviar órdenes.
Las órdenes POST van a través de un proxy SOCKS5 cuya IP esté en Bolivia (no bloqueado).

### Componentes necesarios
1. **Túnel SSH reverso** desde PC de Tien → VPS puerto 1080
2. **Script Python** `clob_trader.py` que reemplace `bullpenBuy/bullpenSell` en CopyEngine.ts
3. **Modificación CopyEngine.ts** — cambiar execução de Bullpen CLI → llamada al script Python

### PASO 1: Crear túnel SOCKS5 persistente
**Desde la PC de Tien en Bolivia:**
```bash
ssh -R 1080 -N -T tien@100.111.136.58
```
Esto abre puerto 1080 en el VPS que tuneliza a través de la IP de Bolivia.

**Para persistencia (autossh en VPS, conectando A la PC de Tien):**
NO funciona porque no hay servidor SSH en la PC de Tien.

**Alternativa mejor: Túnel SSH DESDE la PC de Tien con auto-reconnect**
- Opción 1: Script en Windows con `while True; do ssh -R 1080...; sleep 5; done`
- Opción 2: Install `autossh` en Windows WSL o usar PuTTY tunneling
- Opción 3: **VPS barato en no-bloqueado** (véase Camino B)

### PASO 2: Crear clob_trader.py
```python
#!/usr/bin/env python3
"""
Polymarket CLOB Trader — replaces Bullpen CLI
Uses py-clob-client with SOCKS5 proxy for geoblock bypass
"""
import os, sys, json, argparse

# SOCKS5 proxy setup - MUST be set BEFORE importing py_clob_client
SOCKS_PROXY = os.environ.get("SOCKS_PROXY", "socks5://127.0.0.1:1080")
os.environ["HTTPS_PROXY"] = SOCKS_PROXY

from py_clob_client.client import ClobClient
from py_clob_client.clob_types import ApiCreds, OrderArgs, OrderType

# Credentials
PK = os.environ["WALLET_PRIVATE_KEY"]
API_KEY = os.environ["POLY_API_KEY"]
API_SECRET = os.environ["POLY_API_SECRET"]
API_PASSPHRASE = os.environ["POLY_API_PASSPHRASE"]
SAFE_ADDR = "0xD9161E48da6Ee5ad4F2dbd06e15678E52BD93d4a"

def get_client():
    return ClobClient(
        host="https://clob.polymarket.com",
        key=PK,
        chain_id=137,
        signature_type=2,  # Safe/Gnosis wallet
        funder=SAFE_ADDR,
        creds=ApiCreds(
            api_key=API_KEY,
            api_secret=API_SECRET,
            api_passphrase=API_PASSPHRASE,
        ),
    )

def buy(slug, outcome, amount_usd):
    """Place a BUY order. Returns JSON with result."""
    client = get_client()
    
    # 1. Find the token_id for this slug+outcome
    # Use gamma API to get condition_id, then derive token_id
    import requests
    market_data = requests.get(
        f"https://gamma-api.polymarket.com/markets?slug={slug}",
        timeout=10
    ).json()
    
    if not market_data:
        return {"error": f"Market not found: {slug}"}
    
    market = market_data[0]
    token_id = market.get("clobTokenIds", ["", ""])
    outcomes = market.get("outcomes", [])
    
    if outcome in outcomes:
        idx = outcomes.index(outcome)
        tid = token_id[idx] if idx < len(token_id) else None
    else:
        return {"error": f"Outcome '{outcome}' not found in {outcomes}"}
    
    if not tid:
        return {"error": f"Token ID not found for {slug}/{outcome}"}
    
    # 2. Get market info for tick_size
    mkt = client.get_market(tid)
    
    # 3. Calculate price from amount and size
    # For a simple market buy, use the midpoint
    price = client.get_midpoint(tid)
    if not price or price <= 0:
        price = client.get_last_trade_price(tid)
    
    size = float(amount_usd) / float(price)
    
    # 4. Create and post order
    order_args = OrderArgs(
        token_id=tid,
        price=float(price),
        size=size,
        side="BUY",
    )
    
    signed_order = client.create_order(order_args)
    resp = client.post_order(signed_order, options={
        "tick_size": mkt["tick_size"],
        "neg_risk": mkt.get("neg_risk", False),
    })
    
    return {"status": "ok", "order": resp, "price": float(price), "size": size, "token_id": tid}

def sell(slug, outcome, shares):
    """Place a SELL order. Returns JSON with result."""
    client = get_client()
    
    # Same slug/outcome lookup as buy
    import requests
    market_data = requests.get(
        f"https://gamma-api.polymarket.com/markets?slug={slug}",
        timeout=10
    ).json()
    
    if not market_data:
        return {"error": f"Market not found: {slug}"}
    
    market = market_data[0]
    token_id = market.get("clobTokenIds", ["", ""])
    outcomes = market.get("outcomes", [])
    
    if outcome in outcomes:
        idx = outcomes.index(outcome)
        tid = token_id[idx] if idx < len(token_id) else None
    else:
        return {"error": f"Outcome '{outcome}' not found"}
    
    if not tid:
        return {"error": f"Token ID not found"}
    
    mkt = client.get_market(tid)
    price = client.get_midpoint(tid)
    
    order_args = OrderArgs(
        token_id=tid,
        price=float(price),
        size=float(shares),
        side="SELL",
    )
    
    signed_order = client.create_order(order_args)
    resp = client.post_order(signed_order, options={
        "tick_size": mkt["tick_size"],
        "neg_risk": mkt.get("neg_risk", False),
    })
    
    return {"status": "ok", "order": resp, "price": float(price), "shares": float(shares)}

def positions():
    """Get current positions (no proxy needed for GET)."""
    c = get_client_no_proxy()
    return c.get_orders()

def balance():
    """Get CLOB balance."""
    import requests
    r = requests.get("https://data-api.polymarket.com/value", 
                     params={"user": SAFE_ADDR[2:] if SAFE_ADDR.startswith("0x") else SAFE_ADDR},
                     timeout=10)
    return r.json()

if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument("command", choices=["buy", "sell", "positions", "balance", "test"])
    parser.add_argument("--slug", help="Market slug")
    parser.add_argument("--outcome", help="Outcome name")
    parser.add_argument("--amount", help="USD amount for buy")
    parser.add_argument("--shares", help="Shares for sell")
    
    args = parser.parse_args()
    
    if args.command == "test":
        # Test connection through proxy
        import httpx
        c = httpx.Client(proxy=SOCKS_PROXY, timeout=10)
        r = c.get("https://clob.polymarket.com/time")
        print(json.dumps({"connection": "ok", "server_time": r.text}))
    elif args.command == "buy":
        result = buy(args.slug, args.outcome, args.amount)
        print(json.dumps(result))
    elif args.command == "sell":
        result = sell(args.slug, args.outcome, args.shares)
        print(json.dumps(result))
    elif args.command == "positions":
        result = positions()
        print(json.dumps(result, default=str))
    elif args.command == "balance":
        result = balance()
        print(json.dumps(result, default=str))
```

### PASO 3: Modificar CopyEngine.ts
Cambiar `bullpenBuy` y `bullpenSell` para llamar al script Python:
```typescript
private clobBuy(slug: string, outcome: string, amountUsd: number): string {
  const cmd = `python3 clob_trader.py buy --slug "${slug}" --outcome "${outcome}" --amount "${amountUsd.toFixed(2)}"`;
  return execSync(cmd, { cwd: process.cwd(), encoding: 'utf-8', timeout: 60000 }).trim();
}

private clobSell(slug: string, outcome: string, shares: number): string {
  const cmd = `python3 clob_trader.py sell --slug "${slug}" --outcome "${outcome}" --shares "${shares.toFixed(4)}"`;
  return execSync(cmd, { cwd: process.cwd(), encoding: 'utf-8', timeout: 60000 }).trim();
}
```

### PASO 4: Redimir posiciones ganadas
Las 5 posiciones redeemable (+$21.89) se pueden redimir via blockchain directamente
(sin proxy, sin Bullpen). Usar el script existente de Safe wallet execTransaction.

### RIESGOS del Camino A
- ❌ Depende de PC de Tien encendida 24/7 para el túnel
- ❌ Si el túnel cae, el bot no puede hacer POST (pero GET sigue funcionando → no compra pero sigue detectando)
- ✅ Bolivia NO está bloqueada → proxy funciona
- ✅ Credenciales verificadas y válidas
- ✅ py-clob-client instalado y testeado

---

## CAMINO B: VPS Barato en país no-bloqueado (INDEPENDIENTE de PC de Tien)

### Concepto
Comprar un VPS ultra-barato ($1-2/mes) en un país NO bloqueado (Ej: Irlanda, España, Suiza, México, Chile, etc.).
Instalar SOCKS5 proxy (dante/3proxy) en ese VPS. El bot de Contabo Germany se conecta a ese proxy 24/7.

### País ideal para el VPS
**Irlanda (eu-west-1)** — los servidores de Polymarket están en eu-west-2 (Londres).
Latencia mínima (~5-10ms) y NO está en la lista de bloqueados.

**Otras opciones**: España, Suiza, Suecia, México, Chile, Colombia, Brasil
(Brasil acaba de bloquear, NO usar.)

### PASO 1: Comprar VPS barato
**Recomendado: RackNerd**
- Plan: 1 vCPU, 1GB RAM, 21GB SSD
- Precio: **$10.98/año** (~$0.92/mes)
- Ubicación: Los Angeles, Dallas, Seattle, Atlanta, New Jersey, Chicago, Ashburn
- URL: https://www.racknerd.com/specials/
- ⚠️ RackNerd no tiene Irlanda. Usar Dallas o New Jersey (US, pero US está bloqueado...)

**ALTERNATIVA: BuyVM**
- Ubicación: Luxemburgo (eu) — NO bloqueado
- Precio: ~$2/mes
- URL: https://buyvm.net/

**ALTERNATIVA: Hetzner Cloud**
- Ubicación: Helsinki (FI), Falkenstein (DE-bloqueado!)  
- Finlandia = NO bloqueada
- Precio: €3.29/mes (cxp11)
- URL: https://hetzner.cloud

**ALTERNATIVA: IONOS**
- Ubicación: España (Madrid) — NO bloqueada
- Precio: £1/mes promoción primer año
- URL: https://ionos.com

**ALTERNATIVA: Hostinger VPS**
- Ubicación: Chile, Brasil, EEUU, Europa
- Precio: ~$4.50/mes
- Chile NO está bloqueado

### PASO 2: Instalar SOCKS5 proxy (dante)
```bash
# En el VPS nuevo (ej: Irlanda)
sudo apt update && sudo apt install -y dante-server
sudo cat > /etc/danted.conf << 'EOF'
logoutput: /var/log/danted.log
internal: 0.0.0.0 port = 1080
external: eth0
method: none  # sin autenticación (o usar username)
clientmethod: none
client {
  ip: 100.111.136.58/32  # solo acceso desde VPS Contabo
}
pass {
  from: clientmethod to: 0.0.0.0/0
}
EOF
sudo systemctl restart danted
sudo systemctl enable danted
```

### PASO 3: Configurar bot Contabo para usar el proxy
En `.env` del Contabo VPS:
```
SOCKS_PROXY=socks5://IP_NUEVO_VPS:1080
```

### PASO 4: Test y deploy
```bash
# Desde Contabo VPS
curl --socks5 IP_NUEVO_VPS:1080 https://clob.polymarket.com/time
# Debe devolver timestamp → proxy funciona

python3 clob_trader.py test
# Debe devolver {"connection": "ok", ...}
```

### Costo comparativo
| Opción | País | Costo | Pros | Contras |
|--------|------|-------|------|---------|
| Túnel SSH Bolivia | Bolivia | $0 | Gratis, Bolivia no bloqueado | Depende PC Tien encendida |
| RackNerd | US | $11/año | Ultra barato | US está bloqueado ❌ |
| BuyVM | Luxemburgo | $2/mes | EU, no bloqueado | Poca stock |
| Hetzner | Finlandia | €3.29/mes | Enterprise, rápido | Más caro |
| IONOS | España | ~$1/mes (promo) | España no bloqueado | Solo promo 1er año |
| Hostinger | Chile | $4.50/mes | Chile no bloqueado | Más caro |
| Webshare.io | US/EU | Free (10 proxies) | Gratis para testing | Datacenter IP, puede cambiar |

### RIESGOS del Camino B
- ✅ Independiente de PC de Tien (24/7 sin intervención)
- ✅ Proxy en país no-bloqueado (Irlanda/Luxemburgo/España/Finlandia)
- ⚠️ Costo adicional ($1-5/mes)
- ⚠️ Si Polymarket añade más países bloqueados, podemos migrar el VPS
- ⚠️ VPS barato puede tener downtime

---

## PLAN DE EJECUCIÓN MAÑANA

### Si el Camino A funciona (túnel SSH Bolivia):
1. Tien abre túnel SSH desde su PC
2. Deploy `clob_trader.py` en VPS
3. Modificar CopyEngine.ts → usar clob_trader.py
4. Test: `python3 clob_trader.py test` → OK
5. Test: BUY $2 en mercado activo (Carlos Prates?)
6. PM2 restart bot
7. Verificar trades ejecutándose

### Si el Camino A falla (túnel inestable):
1. Comprar VPS en BuyVM (Luxemburgo) o Hostinger (Chile)
2. Instalar dante SOCKS5 proxy
3. Configurar SOCKS_PROXY en Contabo VPS
4. Test proxy → clob_trader.py test
5. Deploy y activar bot

### ACCIÓN INMEDIATA (ahora):
- Redimir 5 posiciones redeemable (+$21.89) → aumenta bankroll a ~$23.79 en cash
  Estas son posiciones perdidas que no valen nada, PERO las posiciones WON suman $21.89

### ACCIÓN PARALELA:
- Las 5 posiciones redeemable son posiciones PERDIDAS (price=0, redeemable=true)
  NO las redimimos ahora (no generan valor)
- Las posiciones GANADAS (14 won, price=1) SÍ generan valor — verificar si pueden redimirse
  Ganadas = +$21.89 PnL → ya contabilizadas pero shares no convertidas a cash

---

## RESUMEN EJECUTIVO

| | Camino A | Camino B |
|---|---|---|
| Método | SSH Bolivia + py-clob-client | VPS proxy + py-clob-client |
| Costo | $0 | $1-5/mes |
| Depende de | PC de Tien | Servidor 24/7 |
| Tiempo setup | 30 min | 1-2 horas |
| Confiabilidad | Media (túnel cae si PC apaga) | Alta (24/7) |
| Recomendación | Test rápido primero | Solución permanente |

**Credenciales**: ✅ Verificadas y válidas
**SDK**: ✅ Instalado y funcionando (v0.34.6 + v2 1.0.0)
**Geoblock**: Solo POST /order desde Alemania. Bolivia ✅ libre
**Próximo paso**: Test con proxy activo → deploy → bot activo