# Vault Guide — Obsidian Knowledge Base

## Estructura del Vault

```
Obsidian Vault/
├── Agent-Shared/        ← INFO COMPARTIDA (todos leen/escriben)
│   ├── Index.md           Mapa del vault
│   ├── Vault-Guide.md     Esta guía
│   ├── orchestration-plan.md
│   ├── project-state.md
│   ├── decisions-log.md
│   └── user-profile.md
├── Agent-Hermes/        ← Carpeta privada de Hermes
├── Agent-Clowy/         ← Carpeta privada de Clowy
├── Agent-Codex/         ← Carpeta privada de Codex
├── Agent-Wolf/          ← Carpeta privada de Wolf
├── Agent-Polytrader/    ← Carpeta privada de Polytrader
├── Agent-Claude/        ← Carpeta privada de Claude Code
├── daily/               ← Notas diarias (YYYY-MM-DD.md)
└── projects/            ← Documentación de proyectos
```

## Reglas de Oro

1. **Cada agente escribe en SU carpeta** y en `Agent-Shared/`
2. **NUNCA editar la carpeta de otro agente** sin permiso explícito
3. **Agent-Shared** es para info que TODOS necesitan: contexto proyectos, decisiones, estado
4. **Git sync cada 30 min** — VPS ↔ GitHub ↔ Windows (Obsidian app)
5. **Conflictos**: si hay merge conflict, el agente QUE ESCRIBIÓ ÚLTIMO gana

## Protocolo de Git Sync

### Para agentes en VPS (Hermes, cronjobs):
- Pull al inicio de cada sesión
- Push después de cada escritura importante
- El cronjob de Hermes hace sync automático cada 30 min

### Para Codex (en ChatGPT):
Codex NO tiene acceso directo al git del VPS. El flujo es:

1. **Codex trabaja en su carpeta local** (ChatGPT sandbox)
2. **Codex hace commit y push** al repo `obsidian-vault` en GitHub
   - Repo: https://github.com/tiencousillas1-glitch/obsidian-vault
   - Branch recomendado: `codex-updates`
3. **Hermes hace pull** y mergea los cambios
4. **Si hay conflictos**, Hermes resuelve manteniendo lo más reciente

### Para Tien (en Windows con Obsidian):
- Obsidian + plugin Git hace pull/push automático
- Si Codex sube cambios, Obsidian los baja en el próximo sync

## Nombres de Archivos
- Minúsculas, guiones medios: `working-context.md`, `project-state.md`
- Daily notes: `YYYY-MM-DD.md` en `daily/`
- Sin espacios en nombres de archivo