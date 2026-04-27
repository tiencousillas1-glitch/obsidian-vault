# Working Context — Polytrader

## Última sesión: 2026-04-26 — Handoff Cloud Code

### Qué pasó
1. **Auditoría completa de traders** — de 15 wallets → 4 seleccionados on-chain (PnL30d+ y Sharpe>6)
2. **Nuevos traders verificados** — elkmonkey, risk-manager, CarlosMC, 0x4924
3. **Filtros v6 implementados** — min $200 trade, precio 0.2-0.8, vol $5k+, cierre >2h
4. **Filtro WR desactivado** — falsos positivos con whales de alto R/R
5. **Daily loss cap reseteado** — estaba bloqueado con $5.90 acumulado
6. **11 traders eliminados** — siguen en trader_overrides.json como lista negra

### Estado actual del bot
- **Modo:** LIVE (dinero real)
- **Bankroll:** $29.48 USDC
- **Trade size:** $2.00/trade
- **Traders activos:** 4 (elkmonkey, risk-manager, CarlosMC, 0x4924)
- **Filtros v6:** min $200, precio 0.2-0.8, vol $5k+, cierre >2h
- **Safety checks:** 14 en total (ver handoff-2026-04-26.md)
- **Dashboard:** http://100.111.136.58:3001
- **PM2:** polytrader-bot (id=7), dashboard (id=0)

### Mantenimiento semanal (DOMINGOS)
1. Ejecutar auditoría: `node scripts/audit-traders.js`
2. Pausar traders con PnL30d < 0
3. Despausar solo si PnL30d positivo sostenido + Sharpe > 4
4. Verificar dashboard y logs

### Próxima sesión: ANÁLISIS DIARIO
Tien pidió análisis diario:
1. Resumen del día — trades, resultados, P&L
2. Análisis rendimiento — qué fue bien/mal
3. Recomendaciones prácticas — ajustes sobre la marcha
4. Ser proactivo — no esperar a que Tien pregunte

### VPS
- Contabo: 100.111.136.58, user tien
- PM2: dashboard (id 0), polytrader-bot (id 7)
- Bullpen CLI v0.1.64 (auth rota en v0.1.66)
- Bullpen auth expira ~Mayo 19

### APIs clave
- user-pnl-api.polymarket.com — PnL on-chain
- data-api.polymarket.com — trades y positions
- gamma-api.polymarket.com — market info (slug, vol, endDate)

### Pendientes
- Bullpen CLI auth rota — workaround: redeem via Safe{Wallet} o web UI
- Dashboard data "ABIERTA" en mercados resueltos — workaround: resolved.json manual
- $14.80 USDT0 aún en Binance? Verificar estado del depósito 2