---
created: 2026-04-27
updated: 2026-04-27
agent: Claude Code (Windows)
type: session-handoff
---

# Handoff — Sesión 2026-04-27

> Para: próxima sesión (cualquier agente o Claude Code)
> Leer esto PRIMERO antes de tocar nada.

---

## Qué pasó en esta sesión

### 1. Vault de Obsidian conectado a Claude Code

**Problema resuelto:** El skill `obsidian-vault` tenía la ruta incorrecta (`/mnt/d/...` WSL) y el vault real estaba en Windows.

**Cambios hechos:**
- Path corregido → `C:\Users\tcousillas\Documents\obsidian-vault`
- Plugin `obsidian@obsidian-skills` habilitado en `settings.json`
- Carpeta `Agent-Claude/` creada (soy yo, Claude Code en Windows)
- Skill SKILL.md actualizado con path correcto, estructura real del vault, y datos de la REST API

**REST API del vault (si Obsidian está abierto):**
- Puerto: 27124 (HTTPS)
- API Key: `b7b1dc52594e2e3463fbf637cf430e7b65987d516e49002a941e59f1c7a183f3`

---

### 2. Contexto leído — resumen de lo que sé

Leí todos los archivos clave de `Agent-Shared/`:
- `user-profile.md`, `tien-context-pack.md`, `openclaw-project-context.md`
- `decisions-log.md`, `project-state.md`, `Agents-Handbook.md`
- `VEO3/README.md`, `Agent-Hermes/nova-ai-voice-context.md`

**Estado real de Tien al entrar a esta sesión:** $0 revenue, infraestructura construida, demasiados proyectos abiertos, sin primer cliente ni primera order.

---

### 3. Decisión estratégica tomada

**Foco:** Solo 2 tracks este mes.

| Track | Qué | Owner | Time-to-cash |
|---|---|---|---|
| **A. Nova AI Voice** | Cold outreach a clínicas ortodoncia US | Wolf (sales) → Clowy (delivery) | 3-6 semanas |
| **B. Fiverr UGC + VEO 3** | Gigs de video AI + créditos perecederos | Wolf (setup) → Clowy (delivery) → Tien (generation) | 1-2 semanas |

**Descartado:** YouTube faceless, Nano Banana, nuevos agentes. Registrado en `decisions-log.md`.

---

### 4. Archivos creados/modificados en esta sesión

| Archivo | Tipo | Qué contiene |
|---|---|---|
| `Agent-Shared/orchestration-plan.md` | NUEVO | Plan maestro completo: lanes, handoffs, cadencia, métricas, autonomía, fases |
| `Agent-Shared/project-state.md` | MODIFICADO | Foco actualizado a Track A+B, tareas esta semana definidas |
| `Agent-Shared/decisions-log.md` | MODIFICADO | 2 entries nuevas: foco + conexión Claude Code |
| `Agent-Wolf/campaigns.md` | NUEVO | Cold email template V1, gig Fiverr draft, tracker de métricas |
| `Agent-Shared/VEO3/uso-mensual.md` | NUEVO | Tracker de 3 cuentas (3000 créditos/mes), workflow Tien, log de uso |
| `Agent-Claude/working-context.md` | NUEVO | Este archivo |
| `skills/obsidian-vault/SKILL.md` | MODIFICADO | Path corregido + instrucciones actualizadas |
| `.claude/settings.json` | MODIFICADO | Plugin obsidian@obsidian-skills habilitado |

---

## Estado actual (al cierre de sesión)

### Track A — Nova AI Voice
- **Status:** Setup pendiente
- **Completado:** Posicionamiento, templates, orchestration plan
- **Pendiente esta semana:**
  - [ ] Wolf: research 30 clínicas ortodoncia (Houston, Phoenix, Miami, Dallas, Atlanta)
  - [ ] Wolf: setup dominio de warmup para cold email (no usar novaaivoice.com)
  - [ ] Hermes: definir tool de envío (Apollo / Smartlead)
  - [ ] Clowy: stand by para primer handoff de lead

### Track B — Fiverr UGC + VEO 3
- **Status:** Setup pendiente
- **Completado:** Gig draft en `Agent-Wolf/campaigns.md`, tracker de créditos
- **Pendiente urgente:**
  - [ ] **Tien (humano):** verificar las 3 cuentas de AI Studio — confirmar que VEO 3 está disponible y ver el contador de créditos
  - [ ] Clowy: generar 3 videos portfolio (necesita que Tien confirme cuentas)
  - [ ] Wolf: publicar gig en Fiverr con portfolio listo

### Vault
- **Status:** Conectado y funcionando
- **Estructura real confirmada:** `Agent-Claude/`, `Agent-Hermes/`, `Agent-Clowy/`, `Agent-Wolf/`, `Agent-Polytrader/`, `Agent-Shared/`, `daily/`
- **Nota:** La propuesta de restructuración de Hermes (`obsidian-vault-proposal.md`) existe pero NO se implementó — está en espera

---

## Lo que necesita Tien hacer AHORA (antes de que los agentes puedan avanzar)

1. **Verificar cuentas VEO 3:** Entrar a aistudio.google.com con cada una de las 3 cuentas. Ver si aparece "Veo 3" y cuántos créditos tiene. Anotar en `Agent-Shared/VEO3/uso-mensual.md`.

2. **Setup email para outreach:** Decidir si usa Apollo, Smartlead, u otra tool para los cold emails de Nova AI Voice. El dominio principal `novaaivoice.com` NO debe usarse para cold email (riesgo de spam). Necesita dominio secundario con warmup.

3. **Dar luz verde a Wolf:** Con el template en `Agent-Wolf/campaigns.md`, Wolf puede arrancar research de clínicas. Solo necesita confirmación de Tien.

---

## Contexto importante que no está en ningún otro archivo

- **VEO 3 no tiene API gratuita** — Los 3000 créditos son solo vía UI (aistudio.google.com). No hay forma de llamarlos por código sin pagar billing de Google Cloud. Flujo: Clowy genera prompts → Tien hace click en AI Studio → descarga videos → Clowy edita.

- **Minimax es el provider principal de OpenClaw** — No cambiar a OpenAI. Está documentado pero es fácil de olvidar.

- **El "V0" que mencionó Tien son créditos VEO 3**, no V0 de Vercel. Ambos existen pero en esta conversación habló de VEO 3 (Google, generación de video).

- **Wolf necesita dominio de warmup** — Enviar cold email desde Gmail nuevo o desde novaaivoice.com directamente va a spam. Hermes debe resolver esto antes del primer batch.

- **Tien prefiere español, respuestas directas, sin fluff.** Se frustra si le preguntan antes de actuar cuando ya hay contexto suficiente.

---

## Próxima acción prioritaria por agente

| Agente | Acción exacta | Archivo a actualizar |
|---|---|---|
| **Wolf** | Research 30 clínicas ortodoncia (Houston, Phoenix, Miami, Dallas, Atlanta) y llenar tabla en `Agent-Wolf/campaigns.md` | `campaigns.md` + `02-LEADS/pipeline.md` si existe |
| **Clowy** | Esperar confirmación de cuentas VEO 3. Cuando Tien confirme → generar 3 prompts de prueba + pedir generación | `01-PROYECTOS/FIVERR/estado.md` (crear si no existe) |
| **Hermes** | (1) Resolver dominio warmup para cold email. (2) Definir tool de envío. (3) Weekly review viernes 2026-05-03 | `decisions-log.md` + `project-state.md` |
| **Claude Code** | Esta sesión cerrada. Próxima sesión: leer este archivo + `orchestration-plan.md` + `project-state.md` | — |

---

## Definition of done — Semana 1 (cierra 2026-05-03)

- [ ] Wolf: 30 clínicas en tabla de research
- [ ] Tien: cuentas VEO 3 verificadas y documentadas
- [ ] Clowy: 3 videos portfolio generados
- [ ] Wolf: gig Fiverr draft finalizado (copy + pricing)
- [ ] Hermes: dominio warmup definido + tool de envío elegida
- [ ] Hermes: weekly review escrito

---

*Handoff generado por Claude Code — 2026-04-27*
*Siguiente lectura recomendada: `Agent-Shared/orchestration-plan.md`*
