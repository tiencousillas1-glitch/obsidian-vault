# Polytrader — Historial Completo

## Cronología de Sesiones

### 19-Abr-2026: Primer despliegue
- Bot + Dashboard online en VPS 100.111.136.58:3001
- API funcionando, datos reales
- Bullpen CLI v0.1.50, modo SIMULATION
- Dashboard mostraba "todo en cero" → fix: cache del navegador

### 21-Abr-2026: Implementación LIVE
- CopyEngine.ts con ejecución real via Bullpen CLI
- positions is not iterable → silenciado
- Dashboard v3 tutorial-style
- Preview buy confirmado

### 22-Abr-2026: Depósitos y recuperación
- $14.80 USDT0 recuperado de Safe{Wallet} via Python script
- USDT0 contract en Polygon: 0xc2132d05d31c914a87c6611c10748aeb04b58e8f
- RPC que funciona: polygon-bor-rpc.publicnode.com (drpc.org FALLA para eth_call)
- $39.98 USDC depositado en Polymarket via Arbitrum
- Bullpen CLI auth bug: v0.1.66 no guarda token
- Bullpen compensó $20 USDC a Hyperliquid

### 23-Abr-2026: Activación LIVE + Bug crítico
- Bot activado en LIVE, $54.57 bankroll, $3.80/trade
- Dan Added disaster: 12 trades en 30s, $19 en mercado resuelto, -$14.86
- CopyEngine v4 con 8 safety checks
- 3 posiciones redimidas via Safe execTransaction (+$3.35)
- Dashboard v8: 6 bugs corregidos, tabla rendimiento por trader

### 26-Abr-2026: Handoff Cloud Code — Auditoría + Filtros v6
- Auditoría on-chain de 15 wallets → 4 traders verificados seleccionados
- Nuevos traders: elkmonkey (+$1.7M PnL30d), risk-manager (+$68k), CarlosMC (+$1.9M), 0x4924 (+$4.9M)
- 11 traders eliminados → lista negra en trader_overrides.json
- Filtros v6: min $200 trade, precio 0.2-0.8, vol $5k+, cierre >2h
- Filtro WR desactivado (v5.1) — falsos positivos con whales
- Daily loss cap reseteado (estaba bloqueado con $5.90)
- Scripts: audit-traders.js, trader-style.js en /scripts/
- Bankroll: $29.48 USDC, PM2 id=7 (bot), id=0 (dashboard)

## Wallets
- Primary EVM: 0x7C83eb839c3a5Af65812de5c898491f3D154285C
- Routing Polymarket: 0xd77bBe3373D33b57C5d29C8a505692711B89E0Cb
- Safe{Wallet}: 0xD9161E48da6Ee5ad4F2dbd06e15678E52BD93d4a (signer = 0x7C83)
- Polymarket deposit: 0x233aFE02cd307c829c2dA7A104bFA296Dc240B45 (Arbitrum)
- **NUNCA** enviar POL al contrato Safe — siempre al signer 0x7C83

## Depósitos Completados
- Depósito 1: $39.98 USDC via Arbitrum ✅
- Depósito 2: $14.80 USDT0 → Binance → Polymarket (pendiente)
- Polymarket funded: $54.57 USDC (KiddThenkiu)

## Depósitos Pendientes
- $14.80 USDT0 en wallet Polygon → Binance → Polymarket

## Dan Added Disaster — Lección Crítica
- Bot compró 12 trades en 30s de swisstony → 5 trades mismo mercado → -$14.86
- Mercado ya estaba resuelto cuando bot compró
- Fix: CopyEngine v4 con 8 safety checks (ver skill polytrader-vps-deployment)

## Bullpen CLI Auth Bug
- v0.1.66: Login flow muestra "Login successful" pero NO guarda token
- Workaround: redeem via blockchain (Python web3.py, Safe execTransaction)
- o usar Polymarket web UI

## Config Actual (26-Abr-2026)
- Bankroll: $29.48 USDC
- Trade size: $2.00/trade
- Max deployed: 80%
- Stop-loss: DESACTIVADO (esperar resolución)
- Consecutive loss pause: 4 pérdidas → pausa 1h
- Cooldown: 15s entre trades
- Rate limit: 3 trades/cycle, 1 per trader
- Filtros v6: min $200, precio 0.2-0.8, vol $5k+, cierre >2h
- Filtro WR: DESACTIVADO (falsos positivos con whales)
- Traders activos: elkmonkey, risk-manager, CarlosMC, 0x4924 (4 verificados on-chain)
- 11 traders eliminados en lista negra (trader_overrides.json)

## Trader Performance (26-Abr-2026)
|| Trader | PnL 30d | Sharpe | AvgSize | Estado ||
||--------|---------|--------|---------|--------||
|| elkmonkey | +$1.7M | 6.3 | $171 | Activo ||
|| risk-manager | +$68k | 6.0 | $1,086 | Activo ||
|| CarlosMC | +$1.9M | 8.3 | $18,294 | Activo ||
|| 0x4924 | +$4.9M | 7.8 | $26,355 | Activo ||