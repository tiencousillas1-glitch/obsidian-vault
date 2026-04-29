# Propuesta de Reestructuración — Vault de Obsidian

> **Fecha:** 2026-04-29  
> **Autor:** Hermes (CEO)  
> **Propósito:** Transformar el vault en un sistema de conocimiento operativo para manejar clientes, leads e ingresos

---

## 1. Estado Actual — Análisis

### Estructura Actual (35 archivos)

```
/home/tien/Obsidian Vault/
├── Agent-Hermes/
│   ├── working-context.md
│   ├── mistakes.md
│   ├── nova-ai-voice-context.md
│   ├── session-notes-2026-04-27.md
│   └── daily/                       ← sin contenido
├── Agent-Claude/
│   └── working-context.md
├── Agent-Clowy/
│   └── working-context.md
├── Agent-Wolf/
│   ├── 00 - Wolf Overview.md
│   ├── SOUL-Wolf.md
│   ├── MEMORY-Wolf.md
│   ├── Campaigns-Wolf.md
│   └── Agent-Wolf/campaigns.md      ← duplicado
├── Agent-Polytrader/
│   ├── working-context.md
│   ├── history.md
│   ├── mistakes.md
│   ├── PROTOCOL.md
│   ├── handoff-2026-04-26.md
│   └── daily/2026-04-23.md         ← duplicado de /daily/
├── Agent-Shared/
│   ├── Index.md                     ← catálogo maestro
│   ├── Vault-Guide.md              ← guía de protocolos
│   ├── Agents-Handbook.md          ← estructura de agentes
│   ├── user-profile.md             ← perfil de Tien
│   ├── project-state.md            ← estado de proyectos
│   ├── decisions-log.md            ← log de decisiones
│   ├── orchestration-plan.md        ← plan de tracks A+B
│   ├── tien-context-pack.md        ← duplicado
│   ├── openclaw-project-context.md ← duplicado
│   └── VEO3/
│       ├── uso-mensual.md
│       └── README.md
└── daily/
    ├── 2026-04-23.md
    ├── 2026-04-24.md
    └── 2026-04-25.md
```

### Problemas Identificados

| # | Problema | Impacto |
|---|----------|---------|
| 1 | **Carpetas de agente mezcladas con datos de proyecto** | Dificulta encontrar info de clientes/leads |
| 2 | **No hay carpeta de templates** | Cada agente inventa su formato |
| 3 | **No hay carpeta de leads separada** | Leads mezclados con notas de agente |
| 4 | **No hay tracking de ingresos** | No hay forma de ver $ ganados por cliente |
| 5 | **Duplicados** | `campaigns.md` existe en 2 lugares, context packs duplicados |
| 6 | **Fiverr y Nova sin estructura de cliente** | Todo en Agent-Shared o notas de agente |
| 7 | **Daily notes en múltiples lugares** | `/daily/`, `/Agent-Polytrader/daily/`, sin consistency |
| 8 | **No hay workflow documentado por agente** | Cada uno hace lo que quiere |

---

## 2. Nueva Estructura Propuesta

### Arquitectura de Carpetas

```
Obsidian Vault/
│
├── 00-INDEX/                      ← PUNTO DE ENTRADA
│   ├── INDICE.md                  ← Mapa completo del vault
│   ├── Tien-perfil.md             ← Quién es Tien, preferencias
│   └── Arquitectura-sistema.md    ← Cómo funciona el vault
│
├── 01-SERVICIOS/                  ← LOS DOS TRACKS DE INGRESO
│   ├── NOVA-AI-VOICE/
│   │   ├── INDEX.md               ← Estado general del servicio
│   │   ├── positioning.md         ← Mensajes de venta
│   │   ├── pricing.md             ← $300 setup, $297/497/700 mensual
│   │   ├── objection-handling.md  ← Objeciones comunes + respuestas
│   │   │
│   │   ├── 00-LEADS/              ← PIPELINE DE PROSPECTS
│   │   │   ├── PIPELINE.md        ← Vista kanban/tabla de leads
│   │   │   ├── YYYY-MM-DD-nombre.md   ← Un archivo por lead
│   │   │   └── ... (más leads)
│   │   │
│   │   ├── 01-CLIENTES/           ← CLIENTES PAGANDO
│   │   │   ├── INDEX.md           ← Tabla de clientes activos
│   │   │   └── [nombre-clinica]/
│   │   │       ├── estado.md      ← Estado del contrato
│   │   │       ├── config.md      ← Setup de Chloe
│   │   │       ├── notas.md       ← Conversaciones, incidencias
│   │   │       └── billing.md    ← Historial de pagos
│   │   │
│   │   └── 02-ENTREGA/
│   │       ├── checklist-setup.md ← Qué hacer cuando inicia trial
│   │       └── checklist-onboarding.md
│   │
│   └── FIVERR-UGC/
│       ├── INDEX.md               ← Estado del gig
│       ├── gig-copy.md            ← Texto del anuncio
│       ├── pricing.md             ← $50/$100/$150
│       ├── portfolio/
│       │   └── (videos de muestra)
│       │
│       ├── 00-ORDERS/             ← ÓRDENES RECIBIDAS
│       │   ├── PIPELINE.md        ← Tabla de órdenes activas
│       │   ├── YYYY-MM-DD-cliente.md
│       │   └── ...
│       │
│       └── 01-CLIENTES/           ← CLIENTES FIOS (con reviews)
│           ├── INDEX.md
│           └── [nombre]/           ← Uno por cliente recurrente
│
├── 02-LEADS-COLD/                 ← LEADS QUE NO SON DE SERVICIOS
│   ├── INDEX.md                   ← Todos los leads pendientes
│   ├── YYYY-MM-DD-empresa.md
│   └── ...
│
├── 03-INGRESOS/                   ← TRACKING DE DINERO
│   ├── INDEX.md                   ← Dashboard mensual
│   ├── YYYY-MM-resumen.md         ← Resumen por mes
│   ├── NOVA-AI-VOICE/
│   │   └── YYYY-MM-detalle.md     ← Ingresos por clínica
│   └── FIVERR/
│       └── YYYY-MM-detalle.md     ← Ingresos por orden
│
├── 04-PLANTILLAS/                ← TEMPLATES REUTILIZABLES
│   ├── TEMPLATE-lead.md
│   ├── TEMPLATE-cliente-novavoice.md
│   ├── TEMPLATE-cliente-fiverr.md
│   ├── TEMPLATE-proyecto.md
│   ├── TEMPLATE-semanal-review.md
│   ├── TEMPLATE-handoff.md
│   └── TEMPLATE-decision.md
│
├── 05-PERSONA/                   ← CONTEXTO DE TIEN
│   ├── perfil.md                 ← Quién es, cómo trabaja
│   ├── preferencias.md            ← Canales, horarios, idioma
│   └── correcciones.md            ← Lo que no hacer (evitar repeticiones)
│
├── 06-SISTEMA/                   ← DOCUMENTACIÓN TÉCNICA
│   ├── arquitectura-agentes.md     ← Quién es cada agente
│   ├── orchestration-plan.md      ← Plan de tracks A+B
│   ├── comunicaciones.md         ← Protocolos de handoff
│   └── tech-stack.md             ← Herramientas y accesos
│
├── 07-DECISIONES/                ← LOG DE DECISIONES
│   ├── INDEX.md                   ← Índice cronológico
│   └── YYYY-MM-DD-titulo.md       ← Una nota por decisión
│
├── 08-PROYECTOS/                 ← PROYECTOS INTERNOS (infra, etc)
│   ├── INDEX.md
│   └── MISSION-CONTROL/
│       └── estado.md
│
├── 09-DIARIO/                    ← NOTAS DIARIAS
│   └── YYYY/
│       └── YYYY-MM-DD.md          ← Una nota por día
│
├── Agent-Hermes/                 ← WORKSPACE HERMES
│   ├── working-context.md         ← Qué estoy haciendo AHORA
│   ├── mistakes.md               ← Errores que cometí
│   └── sesion-hoy.md             ← Checkpoint al cerrar
│
├── Agent-Wolf/                   ← WORKSPACE WOLF
│   ├── working-context.md
│   ├── campaigns/
│   │   ├── INDEX.md
│   │   └── nova-voice-campaign.md
│   └── outreach/
│       └── email-templates.md
│
├── Agent-Clowy/                  ← WORKSPACE CLOWY
│   ├── working-context.md
│   ├── delivery/
│   │   ├── fiverr-orders.md
│   │   └── nova-trials.md
│   └── production/
│       └── veo3-tracking.md
│
├── Agent-Claude/                 ← WORKSPACE CLAUDE (Windows)
│   └── working-context.md
│
├── Agent-Polytrader/             ← WORKSPACE POLYTRADER
│   └── working-context.md
│
└── Agent-Shared/                 ← SOLO PARA COSAS MUY COMPARTIDAS
    ├── heartbeat-format.md
    ├── handoff-format.md
    └── reminders.md              ← Coherdas que todos deben ver
```

### Resumen de Cambios Clave

| Aspecto | Antes | Después |
|---------|-------|---------|
| Leades | Mezclados en Agent-Shared | `01-SERVICIOS/NOVA-AI-VOICE/00-LEADS/` |
| Clientes Nova | No hay estructura | `01-SERVICIOS/NOVA-AI-VOICE/01-CLIENTES/[nombre]/` |
| Órdenes Fiverr | Sin tracking | `01-SERVICIOS/FIVERR/00-ORDERS/` |
| Ingresos | No hay tracking | `03-INGRESOS/` |
| Templates | En Vault-Guide.md (inline) | `04-PLANTILLAS/` (archivos separados) |
| Notas diarias | `/daily/` + duplicados | `09-DIARIO/YYYY/` (centralizado) |
| Agentes | Mezclado con datos | Workspaces separados al final |

---

## 3. Sistema de Plantillas

### 3.1 Template: Lead (Prospecto)

```markdown
---
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: new|contacted|demo|won|lost
service: nova-voice|fiverr-ugc|other
owner: Wolf|Clowy|Hermes
source: cold-email|cold-call|referral|inbound
---

# Lead: [Nombre de Empresa]

## Datos de Contacto
- **Nombre:** 
- **Cargo:** 
- **Email:** 
- **Teléfono:** 
- **Ubicación:** Ciudad, Estado, País

## Fuente
[Cómo llegó este lead]

## Estado del Pipeline
```
new → contacted → demo booked → trial → paid
```

## Historial de Contacto
| Fecha | Tipo | Notas |
|-------|------|-------|
| YYYY-MM-DD | Email enviado | Intro pitch |
| YYYY-MM-DD | Reply | Interesado, quiere demo |
| YYYY-MM-DD | Demo call | Programó para... |

## Notas
[Conversaciones, objeciones, próximos pasos]

## Objetos Identificados
- **Objección:** [有什么] → [Cómo responder]

## Última Actualización
YYYY-MM-DD por [Agente]
```

### 3.2 Template: Cliente Nova AI Voice

```markdown
---
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: trial|paid|churned
plan: starter|professional|enterprise
owner: Clowy
clinic-name: 
location: 
contact-name: 
contact-email: 
contact-phone: 
---

# Clínica: [Nombre de Clínica]

## Info
- **Ubicación:** 
- **Contacto principal:** 
- **Tamaño:** [N] empleados / [N] sillas
- **Website:** 
- **CRM actual:** 

## Contrato
- **Plan:** $297 / $497 / $700 mensual
- **Inicio trial:** YYYY-MM-DD
- **Fin trial:** YYYY-MM-DD
- **Conversión a paid:** YYYY-MM-DD (o `pendiente`)
- **Billing:** mensual / trimestral / anual

## Setup de Chloe
- **Calendario:** Cal.com / Acuity / Google Calendar / otro
- **Horas de negocio:** 
- **Phone provider:** 
- **Config especial:** 
- **Script personalizado:** sí / no

## Pagos
| Mes | Monto | Fecha | Status |
|-----|-------|-------|--------|
| YYYY-MM | $297 | YYYY-MM-DD | ✅ pagado |

## Notas
[Bloqueos, incidencias, feedback del cliente]

## Próximo Paso
[ ] [acción] — fecha: YYYY-MM-DD
```

### 3.3 Template: Orden Fiverr

```markdown
---
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: received|in-progress|delivered|revision|completed
client-username: 
client-email: 
gig-tier: basic|standard|premium
price: $50|$100|$150
order-id: FIV-XXXXX
deliverable: 
deadline: YYYY-MM-DD
---

# Order: [Cliente] — [Fecha]

## Cliente
- **Username Fiverr:** @[username]
- **Email:** [email]
- **Tier comprado:** Basic / Standard / Premium

## Brief del Cliente
[Qué quiere — copiar del mensaje de Fiverr]

## brief
[Análisis del brief]

## VEO3 Prompts Generados
\`\`\`
1. [prompt]
2. [prompt]
3. [prompt]
\`\`\`

## Videos Generados
| # | Descripción | Link | Status |
|---|-------------|------|--------|
| 1 | | | pendiente/aprobado/rechazado |
| 2 | | | |

## Revisión del Cliente
- **Fecha entrega:** YYYY-MM-DD
- **Fecha review:** YYYY-MM-DD
- **Rating:** ⭐N
- **Feedback:** 

## Notas Internas
[Qué salió bien, qué mejorar]

## Ingreso
- **Precio:** $50 / $100 / $150
- **Fees Fiverr (20%):** $10 / $20 / $30
- **Neto:** $40 / $80 / $120
- **Fecha pago:** YYYY-MM-DD
```

### 3.4 Template: Weekly Review

```markdown
---
week: YYYY-WXX
date: YYYY-MM-DD
owner: Hermes
---

# Weekly Review — Semana WXX (YYYY-MM-DD → YYYY-MM-DD)

## Goal de la Semana
[Del orchestration plan]

## Resultados Obtenidos

### Track A — Nova AI Voice
| Métrica | Meta | Actual | Status |
|---------|------|--------|--------|
| Emails enviados | 50 | N | 🟢/🟡/🔴 |
| Replies | 5+ | N | |
| Demos booked | 2+ | N | |
| Trials | N | N | |

**Qué funcionó:**
- 

**Qué no funcionó:**
- 

### Track B — Fiverr UGC + VEO 3
| Métrica | Meta | Actual | Status |
|---------|------|--------|--------|
| Orders recibidas | 1+ | N | |
| Orders completadas | N | N | |
| Rating promedio | 5⭐ | N | |

**Qué funcionó:**
- 

**Qué no funcionó:**
- 

## Ingresos de la Semana
- **Nova AI Voice:** $0 / $297 / $497 / $700
- **Fiverr UGC:** $0 / $50 / $100 / $150
- **Total:** $0

## Decisiones Tomadas Esta Semana
- [ ] 

## Bloqueos
- [ ]

## Próxima Semana — Goals
1. 
2. 
3. 

## Notas para Tien
[Mensajes que necesitan su atención]
```

### 3.5 Template: Handoff

```markdown
---
from: Wolf|Clowy|Hermes
to: Wolf|Clowy|Hermes
date: YYYY-MM-DD
topic: 
priority: low|medium|high|critical
---

# Handoff: [Tema]

## De → Para
`[Agente A]` → `[Agente B]`

## Estado Actual
[Qué está pasando ahora]

## Lo Completed
- [x] 
- [x] 

## Lo Que Necesito
[Información, decisión, o acción que se necesita]

## Bloqueos
- **Bloqueado por:** [quién o qué]
- **Desde:** YYYY-MM-DD

## Próxima Acción
[ ] [acción específica] — @[agente] — fecha: YYYY-MM-DD

## Contexto Relevante
[Links a notas, archivos, etc]

## Do NOT Change
[Reglas o acuerdos que no se deben modificar]

## Definition of Done
[Cuándo se considera este handoff completo]
```

### 3.6 Template: Decisión

```markdown
---
created: YYYY-MM-DD
owner: Hermes|Tien
status: proposed|decided|implemented|reversed
tags: nova-voice|fiverr-ugc|pricing|hiring|strategy
---

# Decisión: [Título]

## Estado
🟡 Propuesta / ✅ Decidida / 🔄 Implementada / ❌ Reversida

## Contexto
[Por qué se tomó / necesita tomar esta decisión]

## Opciones Consideradas
1. **[Opción A]** → [Por qué rechazada]
2. **[Opción B]** → [Por qué rechazada]
3. **[Opción C — ELEGIDA]** → [Por qué elegida]

## Decisión Final
[Qué se decidió concretamente]

## Fecha de Decisión
YYYY-MM-DD

## Owner
[Quién es responsable de ejecutar]

## Expected Outcome
[Qué se espera que pase]

## Follow-up
- [ ] [Tarea 1]
- [ ] [Tarea 2]

## Review Date
YYYY-MM-DD (para verificar si funcionó)

---

*Decisión registrada por [Agente] — [Fecha]*
```

---

## 4. Workflows por Agente

### 4.1 Hermes (CEO) — Strategy & Decisions

#### Al Iniciar Sesión
1. Leer `09-DIARIO/YYYY/YYYY-MM-DD.md` (nota del día) o crear nueva
2. Leer `Agent-Hermes/working-context.md` 
3. Leer `Agent-Hermes/sesion-hoy.md` si existe (checkpoint previo)
4. Revisar `06-SISTEMA/orchestration-plan.md` si hay decisions pendientes

#### Durante el Día
- **Nueva decisión:** Crear nota en `07-DECISIONES/YYYY-MM-DD-titulo.md`
- **Nueva info de Tien:** Guardar en nota relevante del proyecto
- **Actualizar estado proyecto:** `06-SISTEMA/orchestration-plan.md`

#### Al Cerrar Sesión
1. Actualizar `09-DIARIO/YYYY/YYYY-MM-DD.md` con resumen del día
2. Escribir `Agent-Hermes/sesion-hoy.md` con checkpoint
3. Limpiar `Agent-Hermes/working-context.md` (tareas completadas)
4. Verificar `Agent-Hermes/mistakes.md` si hubo errores

#### Responsabilidades de Tracking
- `03-INGRESOS/INDEX.md` — actualizar cuando hay pago
- `07-DECISIONES/` — registrar toda decisión importante
- `06-SISTEMA/orchestration-plan.md` — mantener vivo

---

### 4.2 Wolf (CRO) — Sales & Outreach

#### Al Iniciar Sesión
1. Leer `09-DIARIO/YYYY/YYYY-MM-DD.md`
2. Leer `Agent-Wolf/working-context.md`
3. Revisar `01-SERVICIOS/NOVA-AI-VOICE/00-LEADS/PIPELINE.md`
4. Revisar `01-SERVICIOS/FIVERR/INDEX.md` si hay órdenes

#### Durante el Día

**Si trabaja leads (Nova AI Voice):**
1. Ir a `01-SERVICIOS/NOVA-AI-VOICE/00-LEADS/`
2. Abrir o crear lead `YYYY-MM-DD-nombre.md`
3. Actualizar `status` en frontmatter
4. Agregar entrada en `Historial de Contacto`
5. Si hay demo → actualizar PIPELINE.md

**Si trabaja Fiverr:**
1. Revisar `01-SERVICIOS/FIVERR/00-ORDERS/PIPELINE.md`
2. Crear nota de orden si es nueva
3. Siorder → handoff a Clowy via `Agent-Shared/handoff-format.md`

**Si escribe emails:**
1. Guardar templates en `Agent-Wolf/outreach/email-templates.md`
2. No guardar emails individuales — solo el template

#### Al Cerrar Sesión
1. Actualizar `09-DIARIO/YYYY/YYYY-MM-DD.md`
2. Escribir `Agent-Wolf/working-context.md` con estado actual
3. Enviar heartbeat a `#agent-comms` (Discord/Telegram)

#### NO Hacer
- ❌ Guardar leads en archivos personales
- ❌ Escribir emails completos — solo templates
- ❌ Guardar información de cliente Nova en archivos personales

---

### 4.3 Clowy (COO) — Delivery & Operations

#### Al Iniciar Sesión
1. Leer `09-DIARIO/YYYY/YYYY-MM-DD.md`
2. Leer `Agent-Clowy/working-context.md`
3. Revisar `Agent-Clowy/delivery/fiverr-orders.md`
4. Revisar `Agent-Clowy/delivery/nova-trials.md`
5. Revisar `Agent-Shared/` por handoffs pendientes

#### Durante el Día

**Si recibe handoff de Wolf (Fiverr order):**
1. Crear nota en `01-SERVICIOS/FIVERR/00-ORDERS/YYYY-MM-DD-cliente.md`
2. Generar prompts VEO 3 en la nota
3. Reportar a Tien: "Genera estos prompts"
4. Cuando Tien devuelve videos → editar → entregar

**Si recibe handoff de Wolf (Nova trial):**
1. Crear/cactualizar carpeta en `01-SERVICIOS/NOVA-AI-VOICE/01-CLIENTES/[nombre]/`
2. Llenar `config.md` con datos del setup
3. Configurar Chloe según `02-ENTREGA/checklist-setup.md`
4. Test call → reportar éxito

**Tracking de VEO 3:**
1. Actualizar `Agent-Clowy/production/veo3-tracking.md`
2. Reportar uso en `Agent-Shared/VEO3/uso-mensual.md`

#### Al Cerrar Sesión
1. Actualizar `09-DIARIO/YYYY/YYYY-MM-DD.md`
2. Escribir `Agent-Clowy/working-context.md`
3. Enviar heartbeat a `#agent-comms`

---

### 4.4 Claude (Windows) — Development

#### Al Iniciar Sesión
1. Leer `09-DIARIO/YYYY/YYYY-MM-DD.md`
2. Leer `Agent-Claude/working-context.md`
3. Revisar `08-PROYECTOS/` si hay tareas de code

#### Durante el Día
- Code en `08-PROYECTOS/` según tareas asignadas
- Documentar en notas del proyecto

#### Al Cerrar Sesión
1. Actualizar `09-DIARIO/YYYY/YYYY-MM-DD.md`
2. Escribir `Agent-Claude/working-context.md`

---

## 5. Plugins de Obsidian Recomendados (2026)

### Esenciales

| Plugin | Para qué | Prioridad |
|--------|----------|-----------|
| **Templater** | Plantillas dinámicas con variables (fecha, nombre de archivo) | 🔴 CRÍTICO |
| **Dataview** | Queries sobre frontmatter — dashboards, tablas de leads | 🔴 CRÍTICO |
| **QuickAdd** | Crear notas desde comandos rápidos | 🔴 CRÍTICO |
| **Folder Note** | Index.md como contenido de carpeta | 🟠 HIGH |
| **Auto Templates** | Aplicar template según carpeta | 🟠 HIGH |

### Highly Recommended

| Plugin | Para qué | Prioridad |
|--------|----------|-----------|
| **Kanban** | Tableros kanban para leads y pipeline | 🟠 HIGH |
| **Tracker** | Gráficos de métricas (emails enviados, revenue) | 🟡 MEDIUM |
| **Buttons** | Botones en notas para acciones comunes | 🟡 MEDIUM |
| **Advanced Tables** | Tablas ordenables y bien formateadas | 🟡 MEDIUM |

### Nice to Have

| Plugin | Para qué | Prioridad |
|--------|----------|-----------|
| **Icon Folder** | Íconos en carpetas (🟢🟡🔴) | 🟢 LOW |
| **Recent Files** | Archivos abiertos recientemente | 🟢 LOW |
| **Word Split** | Para escribir sin distracción | 🟢 LOW |

### Configuración Sugerida de Templater

```javascript
// <% tp.date.now() %> → fecha actual
// <% tp.file.title %> → título del archivo
// <% tp.file.folder() %> → carpeta actual
```

Carpeta de templates: `04-PLANTILLAS/`

---

## 6. Prioridad de Implementación

### Fase 1 — SEMANA 1 (Inmediato, sin bloquear trabajo)

**Objetivo:** Crear la estructura base sin mover archivos existentes

1. **Crear carpetas** según nueva estructura
2. **Mover templates** a `04-PLANTILLAS/` (desde Vault-Guide.md)
3. **Crear `00-INDEX/INDICE.md`** — mapa del vault actualizado
4. **Crear `01-SERVICIOS/NOVA-AI-VOICE/00-LEADS/PIPELINE.md`** con tabla
5. **Crear `01-SERVICIOS/FIVERR/00-ORDERS/PIPELINE.md`** con tabla
6. **Crear `03-INGRESOS/INDEX.md`** con dashboard básico

**Archivos a crear:**
- `04-PLANTILLAS/TEMPLATE-lead.md`
- `04-PLANTILLAS/TEMPLATE-cliente-novavoice.md`
- `04-PLANTILLAS/TEMPLATE-cliente-fiverr.md`
- `04-PLANTILLAS/TEMPLATE-semanal-review.md`
- `04-PLANTILLAS/TEMPLATE-handoff.md`
- `04-PLANTILLAS/TEMPLATE-decision.md`

### Fase 2 — SEMANA 2-3 (Migración gradual)

**Objetivo:** Mover datos existentes a nueva estructura sin perder nada

1. **Migrar leads** de `Agent-Shared/` a `01-SERVICIOS/NOVA-AI-VOICE/00-LEADS/`
2. **Migrar decisiones** a `07-DECISIONES/`
3. **Consolidar daily notes** en `09-DIARIO/YYYY/`
4. **Eliminar duplicados** (campaigns.md, context packs)
5. **Actualizar orchestration-plan.md** → mover a `06-SISTEMA/`

**Archivos a migrar:**
- `Agent-Shared/decisions-log.md` → `07-DECISIONES/INDEX.md`
- `Agent-Shared/project-state.md` → desintegrar en servicios
- `Agent-Hermes/nova-ai-voice-context.md` → `01-SERVICIOS/NOVA-AI-VOICE/INDEX.md`
- `Agent-Wolf/Campaigns-Wolf.md` → `Agent-Wolf/campaigns/INDEX.md`
- `/daily/*.md` → `09-DIARIO/YYYY/`

### Fase 3 — SEMANA 4+ (Optimización)

**Objetivo:** Plugins, dashboards, automatización

1. **Instalar Templater + Dataview + QuickAdd**
2. **Configurar templates automáticas por carpeta**
3. **Crear dashboard de leads** con Dataview query
4. **Crear dashboard de ingresos** con Tracker plugin
5. **Implementar Kanban** para pipeline visual
6. **Documentar workflows** en `00-INDEX/Arquitectura-sistema.md`

---

## 7. Reglas de Oro del Vault

1. **Todo documento va en su carpeta correcta** — no en Agent-Hermes/ porque es fácil
2. **Frontmatter siempre actualizado** — status, fecha, owner
3. **Linkear en vez de copiar** — si la misma info aparece en 2 lugares, está mal
4. **Templates para todo lo repetitivo** — no reinventar formato cada vez
5. **Weekly review cada Viernes** — si no se revisa, no existe
6. **Ingresos se registran el día que se reciben** — no esperar fin de mes
7. **Lead sin contacto en 7 días → status: cold** — no dejar leads huérfanos

---

## 8. Convenciones de Nomenclatura

| Tipo | Formato | Ejemplo |
|------|---------|---------|
| Leads | `YYYY-MM-DD-nombre.md` | `2026-05-01-smith-orthodontics.md` |
| Clientes | `[nombre-carpeta]/` | `smith-orthodontics/estado.md` |
| Decisiones | `YYYY-MM-DD-titulo.md` | `2026-05-03-pricing-enterprise-tier.md` |
| Orders Fiverr | `YYYY-MM-DD-cliente.md` | `2026-05-02-johndoe.md` |
| Daily notes | `YYYY-MM-DD.md` | `2026-05-01.md` |
| Weekly review | `YYYY-WXX-review.md` | `2026-W18-review.md` |
| Handoffs | `YYYY-MM-DD-from-to-topic.md` | `2026-05-01-wolf-clowy-fiverr-order.md` |

---

## 9. Tablas de Referencia Rápida

### Pipeline Nova AI Voice
```
new → contacted → demo_booked → trial → paid
  ↓         ↓            ↓          ↓        ↓
 (Wolf)   (Wolf)      (Wolf)     (Clowy)  (Hermes)
```

### Pipeline Fiverr
```
received → in_progress → delivered → revision → completed
    ↓            ↓             ↓           ↓           ↓
  (Wolf)       (Clowy)       (Clowy)   (Clowy)      (Wolf)
```

### Estructura de Ingresos
```
03-INGRESOS/
├── INDEX.md              ← Dashboard total
├── YYYY-MM-resumen.md    ← Resumen mensual
├── NOVA-AI-VOICE/
│   └── YYYY-MM-detalle.md
└── FIVERR/
    └── YYYY-MM-detalle.md
```

---

## 10. Próximos Pasos Inmediatos (esta semana)

- [ ] Hermes: Crear estructura de carpetas en Obsidian
- [ ] Hermes: Crear 6 archivos de plantilla
- [ ] Wolf: Migrar 3 leads de prueba a nueva estructura
- [ ] Clowy: Crear PIPELINE.md de Fiverr orders
- [ ] Clowy: Documentar 1 orden existente si hay
- [ ] Revisar weekly review el Viernes

---

*Propuesta viva — actualizar según se use y se descubran mejoras.*
*Última actualización: 2026-04-29*
*Owner: Hermes (CEO)*
