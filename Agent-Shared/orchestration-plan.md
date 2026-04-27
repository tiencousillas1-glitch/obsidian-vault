---
created: 2026-04-27
status: active
type: orchestration
owner: Hermes
last-review: 2026-04-27
---

# 🎯 Orchestration Plan — AI Company

> **Mantra:** Build → Test → Demo → Sell → Fix → Repeat
> **Filtro de decisión:** ¿Esto vende, entrega, automatiza o mejora margen? Si no → kill.

---

## 1. Foco actual (decidido 2026-04-27)

**Dos tracks en paralelo. Sin más distracciones.**

| Track | Goal | Time-to-cash | Owner principal |
|---|---|---|---|
| **A. Nova AI Voice** | $297-700 MRR por clínica cerrada | 3-6 semanas | Wolf (sales) |
| **B. Fiverr UGC + VEO 3** | $50-150 por gig | 1-2 semanas | Clowy (delivery) |

**Descartado por ahora:** YouTube faceless, Nano Banana, otros AI services. Sin foco no hay ingreso.

---

## 2. Arquitectura de agentes

```
HERMES (CEO)
├─ Plan semanal Lunes
├─ Review semanal Viernes
└─ Tie-breaker en decisiones de prioridad
        │
   ┌────┴────┐
   ↓         ↓
 WOLF      CLOWY
 (CRO)     (COO)
 Sales     Delivery
   └─── handoffs ───┘
```

### Lanes (sin solapamiento)

**Hermes — Strategy & Orchestration**
- Define goals semanales (Lunes)
- Review viernes con métricas
- Resuelve bloqueos cross-agent
- Mantiene `project-state.md` y `decisions-log.md`

**Wolf — Sales & Pipeline**
- Research de prospects
- Cold email + cold call (cuando aplique)
- Pipeline tracking
- Demo booking
- Handoff a Clowy cuando lead → trial/order

**Clowy — Delivery & Ops**
- Setup de Chloe para clínicas en trial
- Generación + edit de videos VEO 3
- Entrega de orders Fiverr
- Customer success (trials Nova)
- Handoff a Hermes si decisión estratégica

---

## 3. Tracks detallados

### Track A — Nova AI Voice

**Pipeline stages:**
```
Prospect → Contactado → Demo Booked → Trial Active → Paid Customer
   ↓           ↓             ↓             ↓
 (Wolf)     (Wolf)       (Wolf→Clowy)  (Clowy)    → (Hermes review)
```

**Wolf weekly targets:**
- 50 clínicas researched (US, ortodoncia)
- 50 cold emails enviados
- 5+ replies
- 2+ demos booked

**Clowy weekly targets (cuando hay leads):**
- 100% trials con Chloe configurada en <48h
- Check-in semanal con cada trial
- Conversión a paid documented

**Métricas tracked:**
| Métrica | Meta semanal | Tracker |
|---|---|---|
| Emails enviados | 50 | `Agent-Wolf/campaigns.md` |
| Open rate | >40% | mismo |
| Reply rate | >10% | mismo |
| Demos booked | 2+ | `02-LEADS/pipeline.md` |
| Trials activos | tracked | `01-PROYECTOS/NOVA/clientes/` |
| MRR | $0 → $297 → escalar | `03-INGRESOS/resumen-mensual.md` |

---

### Track B — Fiverr UGC + VEO 3

**Pipeline stages:**
```
Gig Live → Order Received → Brief → Prompts → Generation → Edit → Delivery → Review
   ↓            ↓             ↓        ↓           ↓          ↓        ↓         ↓
 (Wolf)     (Wolf→Clowy)    (Clowy)  (Clowy)   (Tien)    (Clowy)  (Clowy)  (Wolf)
```

**Wolf one-time setup:**
- 1 gig Fiverr publicado ("AI UGC video for [niche]")
- 3 portfolio samples generados
- Pricing: Basic $50 / Standard $100 / Premium $150
- Gig copy + thumbnail listos

**Clowy per-order workflow:**
1. Recibe order → crear `01-PROYECTOS/FIVERR/clientes/[id]/`
2. Lee brief del cliente
3. Drafts 5-10 prompts para VEO 3 en `prompts.md`
4. **Pasa a Tien:** "Genera estos prompts en AI Studio"
5. Tien devuelve videos descargados
6. Clowy edita (cortes simples) y entrega vía Fiverr
7. Pide review al cliente

**Métricas tracked:**
| Métrica | Meta semanal | Tracker |
|---|---|---|
| Gig views | tracked | Fiverr stats |
| Orders received | 1+ semana 2 | `01-PROYECTOS/FIVERR/estado.md` |
| Avg order value | $75+ | mismo |
| Reviews 5★ | 100% | mismo |
| Créditos VEO 3 usados | mantener stock | `Agent-Shared/VEO3/uso-mensual.md` |

---

## 4. Comunicación entre agentes

### Handoff format (cuando un agente pasa task a otro)

Archivo en: `Agent-Shared/handoffs/YYYY-MM-DD-[from]-to-[to]-[topic].md`

```markdown
---
from: Wolf
to: Clowy
date: 2026-04-29
topic: Lead Smith Orthodontics → Trial setup
---

## Handoff: Smith Orthodontics

**Current goal:** Setup Chloe for 14-day trial
**Status:** Demo done, accepted trial
**Completed:**
- Demo call done 2026-04-28
- Owner agreed to trial
- Got: clinic hours, phone provider, calendar tool

**Blocked by:** None

**Next action:** Configure Chloe with their calendar (Cal.com), set business hours

**Relevant context:**
- Lead file: `02-LEADS/leads/SMITH-001.md`
- Their calendar: [link]
- Their phone: [number]

**Do not change:** Their existing receptionist setup — Chloe is overflow only

**Definition of done:** Chloe takes a test call successfully and books a fake appointment
```

### Heartbeat format (cada 4h durante work hours)

Vía Telegram al canal `#agent-comms`:

```
[AGENT] HH:MM — STATUS
Last: [acción concreta completada]
Next: [próxima acción concreta]
Blocker: [si hay] / None
Human input: Yes/No
```

### Weekly review (Viernes, Hermes)

Archivo: `07-DIARIO/2026/2026-W[XX]-review.md`

Formato: usar template existente en propuesta de Hermes (sección 3.5 de `Agent-Hermes/obsidian-vault-proposal.md`).

---

## 5. Cadencia semanal

| Día | Quién | Qué | Output |
|---|---|---|---|
| **Lun AM** | Hermes | Plan semanal: 3 goals max | Update `project-state.md` |
| **Lun-Jue** | Wolf | Outreach + research | Heartbeats + leads en pipeline |
| **Lun-Jue** | Clowy | Delivery + trials | Heartbeats + clientes actualizados |
| **Vie AM** | Wolf + Clowy | Reportar métricas semanales | Update sus campaigns/estado.md |
| **Vie PM** | Hermes | Review semanal | Weekly review + decisions-log |
| **Sab-Dom** | Todos | Mantenimiento ligero | Heartbeats opcionales |

---

## 6. Autonomía: qué sí, qué no

### Pueden los agentes solos:
- Web research (Apify, web scraping)
- Draft de emails desde templates
- Tracking de pipeline en vault
- Generación de prompts VEO 3
- Updates a project-state
- Weekly reviews
- Heartbeats Telegram

### Necesitan a Tien:
- **Click "Generate" en AI Studio** (VEO 3 vía UI, no API gratuita)
- Calls de demo en inglés
- Aprobaciones >$500
- Procesamiento de pagos
- Decisiones que cambian estrategia (ej: pivotar niche)

### Plan para destrabar VEO 3 generation:
1. **Semana 1-2:** Tien batchea 1x/día (~15 min para 30 videos)
2. **Semana 3+ (si Fiverr UGC funciona):** Playwright vía OpenClaw automatiza UI, o VA Fiverr a $3-5/hr

---

## 7. Cómo escala el sistema (cuándo agregar agentes)

**Triggers para sumar agentes:**

| Si pasa esto | Crear este agente | Razón |
|---|---|---|
| Wolf >100 leads/semana | **Scout** (research) | Wolf debe enfocarse en outreach, no scrape |
| Clowy >10 orders/semana | **Pixel** (designer) | Edit + thumbnails se vuelven cuello |
| 3+ clientes Nova activos | **Echo** (customer success) | Trials necesitan check-ins constantes |
| Tien dice "necesito código" | **Codex** (developer) | Builds custom (n8n, automation) |

**No crear antes de tiempo.** Cada agente nuevo es overhead hasta que prueba ROI.

---

## 8. Definition of Done por semana

**Semana 1 (esta semana, 2026-04-27 → 05-03):**
- [x] Orchestration plan creado (este archivo)
- [ ] Project-state actualizado con nuevo foco
- [ ] Wolf: 30 clínicas researched + 1 gig Fiverr draft
- [ ] Clowy: 3 videos VEO 3 de prueba para portfolio Fiverr
- [ ] Hermes: weekly review viernes

**Semana 2:**
- [ ] Wolf: 50 cold emails enviados, gig Fiverr publicado
- [ ] Clowy: stand by + portfolio listo
- [ ] Hermes: tracking de open/reply rates

**Semana 3:**
- [ ] Primer demo booked O primera order Fiverr
- [ ] Iteración basada en data real

---

## 9. Lo que NO se hace este mes

- YouTube faceless channel
- Nano Banana (sin info, sin ventaja)
- Más agentes (Scout, Quill, Pixel, Echo) hasta hit triggers
- Refactor de vault (ya hay propuesta — esperar)
- Migrar a otro stack (Minimax stays)

---

## 10. Riesgos y mitigaciones

| Riesgo | Mitigación |
|---|---|
| Cold emails van a spam | Domain warmup + Apollo/Smartlead, NO mandar 50 desde Gmail nuevo |
| VEO 3 credits se gastan rápido | Track diario en `Agent-Shared/VEO3/uso-mensual.md` |
| Tien overwhelmed con tracks paralelos | Hermes corta el segundo si Nova arranca solo |
| AI Studio cambia política (créditos) | Backup: Runway / Sora cuando salga API estable |
| Fiverr suspende gig | Diversificar a Upwork / direct outreach |

---

## 11. Próxima review de este plan

**Fecha:** 2026-05-03 (Viernes)
**Owner:** Hermes
**Trigger:** Si no hay 1+ reply o 1+ order después de 2 semanas → revisar foco.

---

*Plan vivo. Cualquier cambio: registrar en `decisions-log.md` con razón.*
