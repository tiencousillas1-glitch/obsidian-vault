# Mistakes — Polytrader

## 2026-04-23

### Dashboard números duplicados/inconsistentes
- **Error:** 6 posiciones se contaban 2 veces (Polymarket API + resolved.json). Resultado: Ganadas mostraba $7.87 en tile pero $9.91 en barra, Invertido $15.70 vs Activas $5.79, etc.
- **Causa:** mergePositions() en frontend añadía posiciones de resolved.json sin verificar si ya existían en los datos de la API
- **Fix:** Dedup en server.js — posiciones de la API se marcan con `source: 'api'`, resolved-only con `source: 'resolved'`. Si una posición aparece en ambos, se usa el PnL de resolved (más preciso) y se cuenta solo UNA vez
- **Lección:** Siempre verificar que los datos no se dupliquen cuando hay dos fuentes (API + archivo manual)

### Stats calculados en frontend vs backend
- **Error:** Cada métrica se calculaba en un lugar distinto (tile, barra, chip) con fórmulas ligeramente diferentes, provocando inconsistencias
- **Fix:** Todos los cálculos se hacen en server.js y se envían como `real` object. Frontend solo renderiza los valores que vienen del server
- **Lección:** Una sola fuente de verdad para los números. Nunca calcular lo mismo en dos lugares con fórmulas distintas