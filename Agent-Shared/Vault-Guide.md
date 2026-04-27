# Vault de Conocimiento — Guía para Agentes

> Adaptado de [claude-obsidian](https://github.com/AgriciDaniel/claude-obsidian) por AgriciDaniel
> Basado en el patrón LLM Wiki de Andrej Karpathy

---

## Concepto Central

El vault es un **cerebro de conocimiento persistente y acumulativo**. Cada vez que Tien da información, hace un proyecto, o cierra un cliente, eso se integra al vault. Cada pregunta que se hace tira de todo lo que se sabe. El conocimiento se compostea como interés.

---

## Estructura del Vault

```
Obsidian Vault/
├── Agent-Hermes/       ← Hermes (este agente)
├── Agent-Claude/       ← Claude Code en Windows
├── Agent-Clowy/        ← Clowy (OpenClaw)
├── Agent-Wolf/         ← Wolf (OpenClaw)
├── Agent-Polytrader/   ← Polytrader (OpenClaw)
├── Agent-Shared/       ← ⚡ PROTOCOLO PARA TODOS — leer primero
│   ├── PROTOCOL.md     ← Reglas de uso del vault
│   └── INDEX.md        ← Catálogo maestro de todo el vault
└── projects/           ← Proyectos activos de Tien
    ├── nova-ai-voice/  ← Nova AI Voice
    ├── fiverr-ugc/     ← Fiverr UGC videos
    └── <nuevo>/        ← Nuevos proyectos van aquí
```

---

## Convenciones Clave

### Hot Cache (Memoria de Sesión)
- **Archivo:** `Agent-Hermes/hot.md` (para Hermes)
- **Qué es:** Al final de cada sesión, el agente escribe un resumen de contexto reciente
- **Al iniciar:** Leer `hot.md` primero — restaura contexto sin que Tien repita

### Flujo de Trabajo por Proyecto

Para cada proyecto nuevo:

1. **Crear carpeta** en `projects/<nombre-proyecto>/`
2. **Crear `INDEX.md`** con:
   - Objetivo del proyecto
   - Estado actual
   - Próximo paso
   - Blockers (si hay)
3. **Guardar en `hot.md`** al final de cada sesión

### Save Workflow (Cómo Guardar Conversaciones)

Cuando Tien dice algo importante:

1. Crear nota en `projects/<proyecto>/<tema>.md`
2. Usar formato:

```markdown
---
created: 2026-04-27
source: Telegram
project: nova-ai-voice
type: decision
---

# Decisión: Pricing de Nova AI Voice

Tien decidió:
- Setup fee: $300
- Monthly: $297 / $497 / $700
- 14-day free trial

Fecha: 2026-04-27
```

### Query Workflow (Cómo Responder Preguntas)

Cuando Tien pregunta algo:

1. Leer `Agent-Shared/INDEX.md` primero
2. Si no alcanza, ir a `projects/<proyecto>/INDEX.md`
3. Buscar en páginas relevantes
4. Responder citando fuentes específicas del vault

### Lint (Chequeo de Salud) — Mensual

Buscar:
- Notas huérfanas (nadie las linkea)
- Links rotos
- Información desactualizada
- Decisiones tomadas que no se registraron

---

## Comandos Adaptados para Cada Agente

| Acción | Qué hacer |
|--------|-----------|
| **Nueva información de Tien** | Guardar en `projects/<proyecto>/` + actualizar `hot.md` |
| **Nueva decisión** | Registrar en `Agent-Shared/decisions-log.md` |
| **Nuevo lead/prospecto** | Crear nota en `projects/<proyecto>/leads/<nombre>.md` |
| **Nuevo cliente** | Crear carpeta en `projects/<proyecto>/clients/<nombre>.md` |
| **Error o mistake** | Registrar en `Agent-Hermes/mistakes.md` |
| **Al terminar sesión** | Actualizar `hot.md` con resumen de sesión |

---

## Plantillas

### Nota de Proyecto
```markdown
---
created: YYYY-MM-DD
status: active|paused|completed
project: nombre
---

# Proyecto: [Nombre]

## Objetivo
[Qué se quiere lograr]

## Estado Actual
[Qué pasó esta semana]

## Próximo Paso
[Una sola acción]

## Blockers
[Nada] o [Qué está bloqueando]

## Decisiones Tomadas
- [Decisión] — [Fecha]
```

### Nota de Lead/Prospecto
```markdown
---
created: YYYY-MM-DD
status: new|contacted|demo|won|lost
project: nova-ai-voice
type: lead
---

# Lead: [Nombre de Clínica]

## Datos
- **Ubicación:** Ciudad, País
- **Contacto:** Nombre, Teléfono, Email
- **Fuente:** Cómo llegó

## Estado
[new|contacted|demo|won|lost]

## Notas
[Conversaciones, objeciones, siguiente paso]

## Última Actualización
YYYY-MM-DD
```

### Nota de Decisión
```markdown
---
created: YYYY-MM-DD
project: [proyecto]
type: decision
---

# Decisión: [Título]

## Contexto
[Por qué se tomó esta decisión]

## Decisión
[Qué se decidió]

## Fecha
YYYY-MM-DD

## Involucrados
[Quién participó]
```

---

## Reglas de Oro

1. **Todo va al vault** — Si no está en el vault, no existe para los agentes
2. **Una fuente** — Cada nota tiene `source: <origen>` en el frontmatter
3. **Linkear** — Usar `[[wikilinks]]` para conectar notas relacionadas
4. **Estado visible** — El frontmatter siempre tiene `status` actualizado
5. **Hot cache al cerrar** — Siempre actualizar `hot.md` antes de terminar

---

## Proyecto: Nova AI Voice — Estructura Sugerida

```
projects/nova-ai-voice/
├── INDEX.md                    ← Estado general
├── positioning.md              ← Mensajes de venta
├── pricing.md                  ← $300 setup, $297/497/700 mensual
├── clinics/
│   ├── bogota-001.md         ← Primer prospecto Bogotá
│   ├── medellin-001.md        ← Primer prospecto Medellín
│   └── cartagena-001.md       ← Primer prospecto Cartagena
└── outreach/
    └── email-templates.md      ← Plantillas de email frío
```

---

## Inspiración

- [Karpathy's LLM Wiki Pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [claude-obsidian by AgriciDaniel](https://github.com/AgriciDaniel/claude-obsidian)

---

*Última actualización: 2026-04-27*
