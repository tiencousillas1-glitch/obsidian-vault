# 📋 Proposal: Reestructuración del Vault de Obsidian

**Fecha:** 2026-04-27  
**Autor:** Hermes (CEO Agent)  
**Para:** Tien Cousillas

---

## 1. Estado Actual del Vault

### 1.1 Estructura Encontrada

```
/home/tien/Obsidian Vault/
├── Index.md                          ← Guía básica del sistema de 4 capas
├── daily/                            ← Notas diarias sueltas (top-level)
│   └── 2026-04-24.md
├── Agent-Hermes/                     ← Espacio privado de Hermes
│   ├── working-context.md
│   ├── mistakes.md
│   ├── nova-ai-voice-context.md      ← Contexto de Nova AI Voice
│   ├── tien-context-pack.md          ← Contexto profundo de Tien
│   └── daily/
│       ├── 2026-04-23.md
│       └── 2026-04-25.md
├── Agent-Shared/                     ← Compartido: leer y escribir
│   ├── user-profile.md                ← Perfil de Tien
│   ├── project-state.md               ← Estado de proyectos
│   ├── decisions-log.md               ← Decisiones importantes
│   ├── Agents-Handbook.md             ← Manual de agentes
│   ├── tien-context-pack.md
│   └── openclaw-project-context.md
├── Agent-Clowy/                       ← Espacio privado de Clowy
│   └── working-context.md
├── Agent-OpenClaw/                    ← YouTube automation research
│   ├── working-context.md
│   ├── PROTOCOL.md
│   ├── youtube-automation-research.md
│   └── youtube-automation-research.pdf
├── Agent-Polytrader/                  ← Trading agent
│   ├── working-context.md
│   ├── mistakes.md
│   ├── PROTOCOL.md
│   ├── history.md
│   ├── handoff-2026-04-26.md
│   └── daily/
│       └── 2026-04-23.md
└── Agent-Wolf/                        ← Sales agent
    └── 00 - Wolf Overview.md
```

### 1.2 Qué Funciona Bien

- ✅ Sistema de 4 capas de memoria implementado
- ✅ Carpeta `Agent-Shared/` con archivos compartidos claros
- ✅ Protocolo de lectura al inicio de sesión definido
- ✅ `decisions-log.md` y `project-state.md` como fuentes de verdad
- ✅ Cada agente tiene su carpeta privada

### 1.3 Qué NO Funciona / Qué Falta

| Problema | Impacto |
|----------|---------|
| No hay estructura para **clientes** (Fiverr, Nova AI Voice) | Cada proyecto está disperso |
| No hay **lead tracking** (prospect → demo → closed) | No se sabe quién está en qué etapa |
| No hay **templates** reutilizables | Cada nota se crea desde cero |
| No hay **tracking de ingresos** formal | Los ingresos mezclados en project-state |
| Los **daily logs** están en 3 lugares distintos | Difícil encontrar info |
| No hay **zona de triage** para leads nuevos | Se mezclan con proyectos activos |
| Los archivos de contexto son **muy largos** (981 líneas en tien-context-pack) | Difíciles de escanear rápido |

---

## 2. Nueva Estructura Recomendada

### 2.1 Mapa del Vault

```
/home/tien/Obsidian Vault/
│
├── 📂 00-TIEN/                        ← TODO sobre Tien (lectura obligatoria)
│   ├── perfil.md                      ← Perfil breve (no 981 líneas)
│   ├── visión-y-metas.md              ← Visión, goals, direction
│   ├── prefs-de-trabajo.md            ← Cómo trabaja, comunicación
│   └── errores-y-correcciones.md      ← Lecciones aprendidas
│
├── 📂 01-PROYECTOS/                   ← TODOS los proyectos activos
│   │
│   ├── 📂 FIVERR/                     ← Servicio UGC Video
│   │   ├── estado.md                  ← Overview del servicio
│   │   ├── gigs.md                    ← Gigs activos y configuración
│   │   └── 📂 clientes/
│   │       └── [cliente-id]/
│   │           ├── cliente.md         ← Template: Perfil del cliente
│   │           ├── proyecto-activo.md ← Template: Proyecto en curso
│   │           └── hitos.md           ← Checkpoints del proyecto
│   │
│   ├── 📂 NOVA-AI-VOICE/              ← Agentes de voz (clinicas dentales)
│   │   ├── estado.md                  ← Overview del negocio
│   │   ├── offer.md                   ← Oferta, pricing, objection handling
│   │   ├── demo-chloe.md              ← Info del demo agent "Chloe"
│   │   └── 📂 clientes/
│   │       └── [cliente-id]/
│   │           ├── cliente.md
│   │           ├── proyecto-activo.md
│   │           └── hitos.md
│   │
│   └── 📂 OTROS-SERVICIOS/            ← Futuros servicios AI
│       └── [nombre-del-servicio]/
│           └── estado.md
│
├── 📂 02-LEADS/                       ← Pipeline de ventas (CRM simple)
│   ├── pipeline.md                    ← Vista Kanban del pipeline
│   ├── 📂 leads/
│   │   └── [lead-id].md               ← Una nota por lead
│   └── 📂 templates/
│       └── lead-template.md
│
├── 📂 03-INGRESOS/                    ← Tracking financiero
│   ├── resumen-mensual.md             ← Tabla de ingresos por mes
│   ├── facturas-recibidas.md          ← Facturas/pytracks de clientes
│   └── gastos.md                      ← Gastos del negocio
│
├── 📂 04-REUNIONES/                   ← Notas de calls y demos
│   ├── [YYYY-MM-DD]-call-[cliente].md
│   └── template-call.md
│
├── 📂 05-AGENTES/                     ← Documentación de agentes
│   ├── Agents-Handbook.md             ← Mantener el existente
│   ├── 📂 Agent-Hermes/               ← Mantener estructura actual
│   ├── 📂 Agent-Clowy/
│   ├── 📂 Agent-Wolf/
│   ├── 📂 Agent-[Nombre]/
│   └── protocolos/
│       ├── protocolo-hermes.md
│       ├── protocolo-clowy.md
│       └── protocolo-wolf.md
│
├── 📂 06-CONTEXTOS/                   ← Context packs pesados (no leer daily)
│   ├── tien-context-pack-full.md      ← Solo leer si needed, no daily
│   ├── nova-ai-voice-context-full.md
│   └── openclaw-context-full.md
│
├── 📂 07-DIARIO/                      ← Unificada: daily logs de todos
│   ├── 2026/
│   │   ├── 2026-04-WEEK-17.md
│   │   ├── 2026-04-WEEK-18.md
│   │   └── 2026-04-WEEK-19.md
│   └── templates/
│       └── template-weekly-review.md
│
├── 📂 08-RECURSOS/                   ← Links, tools, bookmarks
│   ├── herramientas.md
│   ├── links-utiles.md
│   └── skills-del-agente.md
│
├── Index.md                            ← Este archivo actual (actualizar)
└── DAILY-READ.md                      ← Archivo rápido: leer al inicio
```

### 2.2 Principios de la Nueva Estructura

1. **Separación clara**: Tien (00-TIEN), Servicios (01-), Ventas (02-), Dinero (03-), Calls (04-), Agentes (05-), Contexto Pesado (06-), Diario (07-), Recursos (08-)
2. **Carpetas por cliente**: Cada cliente tiene su subcarpeta con archivos predecibles
3. **Pipeline de leads separado** de proyectos activos
4. **Ingresos separados** de proyectos
5. **Daily logs semanales** en vez de diarios sueltos

---

## 3. Sistema de Templates

### 3.1 Template: Nuevo Lead

```markdown
---
id: LEAD-YYYYMMDD-001
fecha-creado: YYYY-MM-DD
fuente: [cold-email | fiverr | referral | linkedin | inbound | otro]
servicio-interes: [Fiverr-UGC | Nova-AI-Voice | Automatización | Otro]
---

# Lead: [Nombre de la Empresa / Contacto]

## Contacto
- **Nombre:** 
- **Email:** 
- **Teléfono:** 
- **Cargo:** 
- **Empresa:** 
- **Ubicación:** 

##的情报 (Inteligencia)
- Qué hacen: 
- Problema conocido: 
- Usa actualmente (herramientas/competidores): 
- Budget estimado: 
- Timeline: 

## Pipeline Stage
```
[ ] Prospect
[ ] Contactado
[ ] Demo/Call
[ ] Proposal Enviado
[ ] Negociación
[ ] Closed Won ✅
[ ] Closed Lost ❌
```

## Historia de Conversación
- **YYYY-MM-DD:** [Resumen del primer contacto]
- **YYYY-MM-DD:** [Siguiente paso]

## tareas
- [ ] tarea 1
- [ ] tarea 2

## Dueños
- **Owner:** [Wolf | Clowy | Hermes]

## Última Actualización
_Actualizado: YYYY-MM-DD por [Agente]_
```

### 3.2 Template: Cliente Fiverr (Onboarding)

```markdown
---
id: FIVERR-YYYYMMDD-001
fecha-onboarding: YYYY-MM-DD
estado: [onboarding | activo | completado | pausado | cancelado]
---

# Cliente Fiverr: [Nombre]

## Info del Cliente
- **Nombre completo:** 
- **Username Fiverr:** 
- **Email:** 
- **Tiempo en Fiverr:** 
- **Nivel actual (New/Seller/Level 1/2/Premium):** 
- **Review rating promedio:** 

## Détalles del Servicio
- **Gig contratado:** [URL del gig]
- **Paquete:** [Basic | Standard | Premium]
- **Precio pagado:** $XXX
- **Fecha del pedido:** YYYY-MM-DD
- **Deadline:** YYYY-MM-DD

## Requisitos del Proyecto
### Brief del cliente:
_Aquí va el brief o instrucciones que dio_

### entregables:
- [ ] Entregable 1
- [ ] Entregable 2

### Referencias de estilo:
_

## Comunicación
- **Plataforma:** [Fiverr | WhatsApp | Email]
- **Tono preferido:** [Profesional | Casual | Formal]
- **Horario de disponibilidad:** 

## Progreso

| Hito | Fecha | Estado |
|------|-------|--------|
| Onboarding completado | YYYY-MM-DD | ✅/🔄 |
| Primer draft enviado | YYYY-MM-DD | ✅/🔄 |
| Revisiones | YYYY-MM-DD | ✅/🔄 |
| Aprobación final | YYYY-MM-DD | ✅/🔄 |
| Review dejado | YYYY-MM-DD | ✅/🔄 |

## Revisión Fiverr
- **Review recibido:** ⭐⭐⭐⭐⭐
- **Comentario:** 
- **Link:** 

## Notas Internas
_

## Owner
**Asignado a:** [Clowy | otro agente]
```

### 3.3 Template: Cliente Nova AI Voice (Onboarding)

```markdown
---
id: NOVA-YYYYMMDD-001
tipo: [lead | prospect | demo | cliente]
estado: [investigando | contactado | demo-programado | trial | activo | pausado | churned]
fecha-alta: YYYY-MM-DD
---

# Clinica: [Nombre de la Clínica]

## Info de la Clínica
- **Nombre:** 
- **Dirección:** 
- **Teléfono:** 
- **Web:** 
- **Tipo:** [Dental | Ortodoncia | General]
- **Tamaño:** [Solo dueño | 1-5 empleados | 6-15 | 15+]
- **Ubicación:** [Ciudad, Estado, US]

## Persona de Contacto
- **Nombre:** 
- **Cargo:** 
- **Email:** 
- **Teléfono:** 
- **Mejor hora para llamar:** 

## Pain Points Conocidos
- 
- 
- 

## Solución Ofrecida
- **Pack de Nova AI Voice:** [Starter $297 | Pro $497 | Enterprise $700]
- **Setup fee:** $300
- **Trial:** 14 días

## Seguimiento

| Fecha | Acción | Resultado | Próximo Paso |
|-------|--------|-----------|--------------|
| YYYY-MM-DD | Cold email enviado | Open ✅ / No open ❌ | Waiting reply |
| YYYY-MM-DD | Follow-up | Reply received ❌ | Call scheduled |
| YYYY-MM-DD | Demo call | Interested ✅ | Send proposal |
| YYYY-MM-DD | Proposal enviado | Sent | Pending decision |

## Propuesta / Contract
- **Documento:** [link o archivo]
- **Enviado:** YYYY-MM-DD
- **Estado:** [Pending | Accepted | Rejected | Negotiation]

## Técnico (para implementación post-venta)
- **Software de agenda:** 
- **Phone provider:** 
- **Número principal:** 
- **Hours de atención:** 
- **Special instructions:** 

## Notas
_

## Owner
**Owner:** [Wolf | Clowy | Hermes]
```

### 3.4 Template: Status de Proyecto (Weekly Update)

```markdown
# 📊 Status del Proyecto: [Nombre]
**Semana:** YYYY-WXX  
**Servicio:** [Fiverr UGC | Nova AI Voice | Otro]  
**Cliente:** [Nombre]  
**Owner:** [Agente]  

## Resumen Ejecutivo
_1-2 líneas sobre en qué va el proyecto_

## lo Hecho (Esta Semana)
- [ ] Logro 1
- [ ] Logro 2

## En Progreso
- [ ] Tarea 1 — _XX% — blocked by: [blocker]_
- [ ] Tarea 2 — _50%_

## Bloqueadores
- 🔴 Bloqueador 1: [descripción]
- 🟡 Bloqueador 2: [descripción]

## Próxima Semana (Prioridades)
1. **HIGH:** [ ]
2. **MED:** [ ]
3. **LOW:** [ ]

## Métricas
| Métrica | Antes | Ahora | Meta |
|---------|-------|-------|------|
| | | | |

## Decisiones Tomadas
- _Decisión 1:_ [Razón]
- _Decisión 2:_ [Razón]

## Notas del Cliente
_Cualquier feedback o request del cliente_
```

### 3.5 Template: Weekly Review

```markdown
# 📅 Weekly Review — YYYY-WXX

**Fecha:** YYYY-MM-DD  
**Agent:** [Hermes | Clowy | Wolf]  

---

## 🎯 Goals de la Semana (del Monday Planning)
1. [Goal 1]
2. [Goal 2]
3. [Goal 3]

---

## ✅ Completado
| Task | Resultado |
|------|-----------|
| | |

---

## ❌ No Completado + Razóm
| Task | Por qué no | Carry over? |
|------|-----------|--------------|
| | | Sí/No |

---

## 💰 Revenue
| Fuente | Cantidad | Estado |
|--------|----------|--------|
| Fiverr - Cliente X | $XXX | Cobrado/Pendiente |
| Nova AI - Clinica Y | $XXX | Pagado/Pendiente |

**Total esta semana:** $XXX

---

## 🔥 Wins de la Semana
1. 
2. 

## 😭 Lecciones de la Semana
1. 

---

## 📊 Pipeline de Leads (al cierre de semana)
| Lead | Stage | Próximo Paso |
|------|-------|--------------|
| | | |

---

## 🎯 Goals para Próxima Semana
1. **HIGH:** 
2. **HIGH:** 
3. **MED:** 
4. **LOW:** 

---

## Blockers que Necesitan Soporte de Tien
- [ ] 
```

---

## 4. Workflows por Agente

### 4.1 Hermes (CEO) — Qué Leer al Iniciar

```
ARCHIVO                      FRECUENCIA     PROPOSITO
─────────────────────────────────────────────────────────────────
00-TIEN/perfil.md            SIEMPRE        Quién es Tien, contexto rápido
00-TIEN/visión-y-metas.md   Semanal        Dirección estratégica
01-PROYECTOS/estado.md       Diario         Overview de todos los servicios
02-LEADS/pipeline.md        Diario         Estado del pipeline de ventas
03-INGRESOS/resumen-mensual.md  Semanal     Tracking de dinero
07-DIARIO/[semana-actual].md Diario        Qué pasó, qué sigue

SOLO SI NECESARIO (no daily):
06-CONTEXTOS/tien-context-pack-full.md
```

**Qué Escribir:**
- `07-DIARIO/YYYY-WXX.md` — Actualizar al final de cada día
- `02-LEADS/[lead-id].md` — Si surge lead nuevo
- `01-PROYECTOS/[servicio]/estado.md` — Si cambia estado de proyecto
- `decisions-log.md` (en 05-AGENTES/Agent-Hermes/) — Si decisión importante

### 4.2 Wolf (CRO/Sales) — Qué Leer al Iniciar

```
ARCHIVO                      FRECUENCIA     PROPOSITO
─────────────────────────────────────────────────────────────────
00-TIEN/perfil.md            SIEMPRE        Quién es Tien
02-LEADS/pipeline.md         Diario         Todos los leads y su stage
02-LEADS/leads/*.md          Diario         Detalle de leads activos
01-PROYECTOS/FIVERR/estado.md  Diario      Estado de gigs Fiverr
01-PROYECTOS/NOVA-AI-VOICE/estado.md Diario  Estado de Nova AI Voice
05-AGENTES/Agent-Wolf/campaigns.md  Diario  Estado de campañas activas
07-DIARIO/[semana-actual].md Diario        Resumen semanal
```

**Qué Escribir:**
- `02-LEADS/leads/[nuevo-lead].md` — Cada vez que aparece lead nuevo
- `02-LEADS/pipeline.md` — Actualizar stage del lead
- `05-AGENTES/Agent-Wolf/campaigns.md` — Estado de campañas email
- `07-DIARIO/YYYY-WXX.md` — Log de qué hizo, qué sigue

### 4.3 Clowy (COO) — Qué Leer al Iniciar

```
ARCHIVO                      FRECUENCIA     PROPOSITO
─────────────────────────────────────────────────────────────────
00-TIEN/perfil.md            SIEMPRE        Quién es Tien
01-PROYECTOS/FIVERR/clientes/*/proyecto-activo.md  Diario  Clientes activos
01-PROYECTOS/NOVA-AI-VOICE/clientes/*/  Semanal  Clientes en trial/implementación
07-DIARIO/[semana-actual].md Diario        Resumen de la semana
05-AGENTES/Agent-Clowy/*.md  Diario        Su estado y tareas
```

**Qué Escribir:**
- `01-PROYECTOS/FIVERR/clientes/[id]/proyecto-activo.md` — Update semanal del cliente
- `01-PROYECTOS/FIVERR/clientes/[id]/hitos.md` — Cuando se completa un hito
- `05-AGENTES/Agent-Clowy/working-context.md` — Estado actual
- `07-DIARIO/YYYY-WXX.md` — Log de operaciones

### 4.4 Nuevo Agente (Onboarding)

```
1. Leer: 00-TIEN/perfil.md + prefs-de-trabajo.md
2. Leer: 05-AGENTES/protocolo-[agente].md
3. Leer: 07-DIARIO/[semana-actual].md
4. Escribir: 05-AGENTES/Agent-[Nombre]/working-context.md
5. Actualizar: 05-AGENTES/Agents-Handbook.md (agregar al roster)
```

---

## 5. Cómo Manejar Leads (Pipeline)

### 5.1 Etapas del Pipeline

```
PROSPECT → CONTACTADO → DEMO → PROPOSAL → NEGOCIACIÓN → CLOSED WON ✅
                                                    ↘ CLOSED LOST ❌
```

### 5.2 Reglas del Pipeline

| Evento | Acción |
|--------|--------|
| Lead nuevo identificado | Crear `02-LEADS/leads/[lead-id].md` desde template |
| Se envió email/call | Agregar entrada en historial del lead |
| Stage cambió | Actualizar checkbox en pipeline.md y fecha en lead |
| Demo completado | Crear nota en `04-REUNIONES/YYYY-MM-DD-call-[lead].md` |
| Proposal enviado | Link al doc en lead + actualizar stage |
| Closed Won | Mover a `01-PROYECTOS/[servicio]/clientes/[id]/` como cliente activo |
| Closed Lost | Archivar en lead con razón |

### 5.3 Prioridades Semanales de Wolf (Sales)

1. **Lunes:** Revisar pipeline, identificar stalled leads, plan outreach
2. **Martes-Jueves:** Ejecutar campañas, follow-ups, demos
3. **Viernes:** Weekly review, actualizar pipeline, prep Monday

---

## 6. Plugins de Obsidian Recomendados (2026)

### 6.1 Plugins Esenciales

| Plugin | Qué Hace | Por qué Importa |
|--------|----------|-----------------|
| **Templater** | Templates avanzados con variables | Crear archivos con fecha, id, owner automático |
| **Dataview** | Queries sobre archivos markdown | Filtrar leads por stage, proyectos por estado |
| **Kanban** | Tableros Kanban visuales | Visualizar pipeline de leads como Trello |
| **QuickAdd** | Crear notas rápido con shortcuts | Crear lead nuevo en 2 clicks |
| **Calendar** | Vista de calendario | Ver qué días hay meetings/calls |
| **Reminder** | Notificaciones in-app | Seguimiento de deadlines de proyectos |

### 6.2 Plugins para Productividad

| Plugin | Qué Hace | Por qué Importa |
|--------|----------|-----------------|
| **Local REST API** | API local para automatizaciones | Agents pueden escribir al vault via HTTP |
| **Shell Commands** | Ejecutar shell desde Obsidian | Automatizar tareas repetitivas |
| **Meta Clean** | Personalizar metadata | Mantener frontmatter consistente |
| **Auto Templates Prompt** | Auto-aplicar template según carpeta | No olvidar usar el template correcto |

### 6.3 Plugins para Mantener el Vault Limpio

| Plugin | Qué Hace | Por qué Importa |
|--------|----------|-----------------|
| **Style Settings** | Configurar temas visualmente | Mantener look consistente |
| **Hide Folders in Sidebar** | Ocultar carpetas específicas | 06-CONTEXTOS no satura el sidebar |
| **Recent Files Excluded** | Excluir archivos de "recent" | No mezclar contextos viejos |
| **File Colour** | Colores en archivos del sidebar | Diferenciar tipos de archivo visualmente |

### 6.4 Instalación Rápida (Commands)

En Obsidian: `Settings → Community Plugins → Browse` y buscar cada uno.

---

## 7. Prioridad de Implementación

### 🔴 FASE 1 — Lo Que Hay Que Hacer PRIMERO (Esta semana)

**Objetivo:** Tener la estructura mínima viable funcionando

1. **Crear carpetas nuevas** (01-PROYECTOS, 02-LEADS, 03-INGRESOS, 04-REUNIONES, 05-AGENTES, 06-CONTEXTOS, 07-DIARIO, 08-RECURSOS)
2. **Crear `00-TIEN/perfil.md`** — Versión corta del context pack (max 100 líneas)
3. **Crear `DAILY-READ.md`** — Archivo de 1 página con lo que cada agente debe leer daily
4. **Crear `02-LEADS/pipeline.md`** con los 3 leads actuales (Wolf, Fiverr, Nova)
5. **Instalar Templater + QuickAdd** — Para crear notas desde templates rápido
6. **Instalar Kanban** — Para ver pipeline visualmente
7. **Mover archivos existentes** a las carpetas correctas:
   - `nova-ai-voice-context.md` → `06-CONTEXTOS/`
   - `tien-context-pack.md` → `06-CONTEXTOS/` (como backup, no lectura daily)
   - Daily logs → `07-DIARIO/YYYY-WXX.md` (consolidar en weekly)

### 🟡 FASE 2 — Segunda Semana

**Objetivo:** Templates funcionando + tracking de ingresos

1. **Crear todos los templates** en sus carpetas correspondientes
2. **Crear `03-INGRESOS/resumen-mensual.md`** con tabla
3. **Crear estado.md en cada servicio** (FIVERR/estado.md, NOVA-AI-VOICE/estado.md)
4. **Instalar Dataview** — Para queries sobre los leads y proyectos
5. **Instalar Calendar** — Para ver fechas de calls y deadlines
6. **Crear `05-AGENTES/protocolos/`** con protocolo específico por agente
7. **Actualizar Index.md** — Con la nueva estructura completa

### 🟢 FASE 3 — Tercera Semana+

**Objetivo:** Automatización y refinamiento

1. **Instalar Local REST API** — Para que agentes escriban al vault programmatically
2. **Crear QuickAdd macros** para cada tipo de nota (lead nuevo, cliente nuevo, weekly review)
3. **Instalar Reminder** — Para deadlines de proyectos Fiverr
4. **Crear dashboard en Dataview** — Ver todos los leads en stage X con una query
5. **Revisar y limpiar** — Qué funciona, qué no, iterar
6. **Documentar el sistema** — Actualizar protocolos con lo aprendido

---

## 8. Resumen: Cambios Más Importantes

| Cambio | Impacto |
|--------|---------|
| **Separar leads de proyectos** | Sales y delivery no se mezclan |
| **Templates para todo** | Cada nota se crea igual, es predecible |
| **Carpeta 00-TIEN corta** | Contexto rápido sin leer 1000 líneas |
| **Weekly reviews** | No daily logs sueltos que se pierden |
| **Pipeline visual (Kanban)** | Siempre claro quién está en qué etapa |
| **Tracking de ingresos separado** | Separas el dinero de las operaciones |
| **Carpeta 06-CONTEXTOS** | Archivos pesados no saturan la lectura daily |

---

## 9. Cómo Empezar (Checklist)

```bash
# 1. Crear carpetas nuevas en el vault
mkdir -p /home/tien/Obsidian\ Vault/00-TIEN
mkdir -p /home/tien/Obsidian\ Vault/01-PROYECTOS/FIVERR/clientes
mkdir -p /home/tien/Obsidian\ Vault/01-PROYECTOS/NOVA-AI-VOICE/clientes
mkdir -p /home/tien/Obsidian\ Vault/01-PROYECTOS/OTROS-SERVICIOS
mkdir -p /home/tien/Obsidian\ Vault/02-LEADS/leads
mkdir -p /home/tien/Obsidian\ Vault/02-LEADS/templates
mkdir -p /home/tien/Obsidian\ Vault/03-INGRESOS
mkdir -p /home/tien/Obsidian\ Vault/04-REUNIONES
mkdir -p /home/tien/Obsidian\ Vault/05-AGENTES/protocolos
mkdir -p /home/tien/Obsidian\ Vault/06-CONTEXTOS
mkdir -p /home/tien/Obsidian\ Vault/07-DIARIO/2026
mkdir -p /home/tien/Obsidian\ Vault/07-DIARIO/templates
mkdir -p /home/tien/Obsidian\ Vault/08-RECURSOS

# 2. Crear archivo DAILY-READ.md en raíz
# (con la tabla de qué leer por agente)

# 3. Instalar plugins desde Obsidian
# Templater, QuickAdd, Kanban, Calendar, Dataview, Hide Folders in Sidebar

# 4. Mover archivos existentes
# 5. Crear templates
# 6. Actualizar Index.md
```

---

## Nota Final

Este sistema está diseñado para que **cada agente sepa exactamente qué leer y dónde escribir** sin tener que pensar. La estructura predecible reduce la carga cognitiva y permite que cualquier agente pueda retomar el trabajo de otro en cualquier momento.

La regla más importante: **si no está en el vault, no existe para los agentes.**

---

*Proposal generado por Hermes — 2026-04-27*
