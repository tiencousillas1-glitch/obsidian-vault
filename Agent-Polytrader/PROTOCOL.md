# Protocolo Obsidian — Polytrader

## Ubicación del Vault
`/home/tien/Obsidian Vault/`

## Tu carpeta
`/home/tien/Obsidian Vault/Agent-Polytrader/`

## Estructura de TU carpeta
```
Agent-Polytrader/
├── working-context.md    ← Qué estás haciendo AHORA
├── mistakes.md           ← Errores y lecciones
└── daily/                ← Un archivo por día (YYYY-MM-DD.md)
```

## Carpeta COMPARTIDA (leer y escribir)
`/home/tien/Obsidian Vault/Agent-Shared/`
- `project-state.md` — estado de todos los proyectos
- `decisions-log.md` — decisiones importantes
- `user-profile.md` — perfil de Tien

---

## PROTOCOLO DE USO

### Al iniciar sesión:
1. Leé `Agent-Shared/user-profile.md`
2. Leé `Agent-Shared/project-state.md`
3. Leé `Agent-Shared/decisions-log.md`
4. Leé `Agent-Polytrader/working-context.md` (tu estado anterior)
5. Leé el daily de hoy si existe

### Durante la sesión:
- Cada 3-5 llamadas a herramientas → actualizá `working-context.md`
- Si tomás una decisión importante → escribila en `decisions-log.md`
- Si Tien menciona algo nuevo → actualizá `project-state.md`
- Si cometés un error → anotalo en `mistakes.md`

### Al terminar la sesión:
- Escribí resumen en `Agent-Polytrader/daily/YYYY-MM-DD.md`
- Actualizá `working-context.md` con lo que hiciste y qué sigue

---

## REGLA PRINCIPAL
**Si Tien te dice algo → escribilo en el vault inmediatamente.**
**No perdés contexto entre sesiones.**

## Consultas
Si necesitás contexto de otro agente → leé en `Agent-Shared/`
