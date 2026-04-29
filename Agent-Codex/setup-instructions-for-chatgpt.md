# Obsidian Vault — Setup para Codex/ChatGPT

## Contexto

Tengo un Obsidian Vault que vive en un VPS (Linux) y está conectado a GitHub. Varios agentes de IA (Hermes, Clowy, Wolf, Polytrader) escriben en sus carpetas dentro del vault. Yo uso ChatGPT/Codex como mi "code operator" y necesito que también tenga acceso al vault para leer y escribir.

## Repo GitHub

- **URL**: https://github.com/tiencousillas1-glitch/obsidian-vault
- **Branch**: `master`
- **Username**: tiencousillas1-glitch

## Estructura del Vault

```
obsidian-vault/
├── Agent-Shared/        ← INFO COMPARTIDA (todos leen/escriben)
│   ├── Index.md
│   ├── Vault-Guide.md
│   ├── orchestration-plan.md
│   ├── project-state.md
│   ├── decisions-log.md
│   └── user-profile.md
├── Agent-Hermes/        ← Carpeta de Hermes (NO tocar)
├── Agent-Clowy/         ← Carpeta de Clowy (NO tocar)
├── Agent-Codex/         ← MI carpeta (aquí escribo yo)
├── Agent-Wolf/          ← Carpeta de Wolf (NO tocar)
├── Agent-Polytrader/    ← Carpeta de Polytrader (NO tocar)
├── Agent-Claude/        ← Carpeta de Claude (NO tocar)
├── daily/               ← Notas diarias (YYYY-MM-DD.md)
└── projects/            ← Documentación de proyectos
```

## Reglas

1. **Escribir SIEMPRE en `Agent-Codex/` o `Agent-Shared/`**
2. **NUNCA editar carpetas de otros agentes** sin permiso explícito
3. Nombres de archivos: minúsculas, guiones medios, sin espacios
4. Mensajes de commit: `codex: descripción del cambio`

## Flujo de Git — LO QUE NECESITO QUE AUTOMATICES

### El problema
Necesito que cada vez que yo trabaje con Codex, los cambios se sincronicen con el repo de GitHub para que los otros agentes (que corren en el VPS) los puedan ver, y viceversa — cuando los otros agentes escriben, Codex necesita ver esos cambios.

### Sync automático del VPS (YA CONFIGURADO)
- Hermes (agente en VPS) hace git sync cada 2 horas
- Hace `git add -A && git commit && git pull --rebase && git push origin master`

### Lo que necesito que CODEX haga
Antes de empezar a trabajar: `git pull origin master`
Después de hacer cambios: `git add -A && git commit -m "codex: descripción" && git push origin master`

### Lo que NECESITO que automatices
Quiero que este proceso sea lo más automático posible. Opciones a evaluar:

1. **Codex CLI con hooks** — ¿Se puede configurar un hook post-tarea que haga git push automático?
2. **Script wrapper** — Un script que envuelva las tareas de Codex y haga pull antes / push después
3. **GitHub Actions** — ¿Un workflow que detecte cambios y los sincronice?
4. **Cualquier otra solución** que encuentres

El objetivo: yo le doy una tarea a Codex, Codex trabaja, y sin que yo haga nada extra los cambios ya están en GitHub. Y cuando Codex empieza, automáticamente trae los cambios más recientes.

## Mi setup local (Windows + Obsidian)
- Uso la app Obsidian en Windows
- Tengo el plugin "Obsidian Git" que hace pull/push automático
- El repo local apunta al mismo `obsidian-vault` en GitHub
- Pull automático cada 30 min, push automático cada 30 min

## Lo que YA está funcionando
- ✅ Repo en GitHub con estructura completa
- ✅ Hermes en VPS hace sync cada 2 horas
- ✅ Obsidian Git plugin en Windows hace sync periódico
- ✅ Carpeta `Agent-Codex/` creada en el vault
- ❌ FALTA: automatización de git sync para Codex

## Resumen de lo que te pido
Encuentra la mejor forma de automatizar el git sync para Codex (OpenAI) de modo que:
1. Antes de cada tarea, haga pull automáticamente
2. Después de cada cambio, haga commit + push automáticamente
3. Yo no tenga que acordarme de hacer git manualmente
4. Todo se mantenga sincronizado entre VPS ↔ GitHub ↔ Windows ↔ Codex