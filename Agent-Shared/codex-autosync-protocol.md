# Codex Autosync Protocol — Obsidian Vault

## Principio
Cada agente es responsable de hacer git push de SUS PROPIOS cambios. No hay sync centralizado.

## Regla de Oro
**Escribiste → Hiciste push. No escribiste → Hacés pull antes de escribir.**

## Flujo por agente

### Hermes (VPS)
1. Pull antes de leer: `git -C "/home/tien/Obsidian Vault" pull --rebase origin master`
2. Escribe en `Agent-Hermes/` o `Agent-Shared/`
3. Push después de escribir:
```
git -C "/home/tien/Obsidian Vault" add Agent-Hermes/ Agent-Shared/
git -C "/home/tien/Obsidian Vault" commit -m "hermes: descripción del cambio"
git -C "/home/tien/Obsidian Vault" push origin master
```

### Codex (ChatGPT)
1. Pull antes de trabajar: `git pull --rebase origin master`
2. Escribe en `Agent-Codex/` o `Agent-Shared/`
3. Push después de escribir:
```
git add Agent-Codex/ Agent-Shared/
git commit -m "codex: descripción del cambio"
git push origin master
```

### Clowy / Wolf / Polytrader
Mismo patrón: pull → escribir en su carpeta → push con su prefijo.

### Tien (Windows + Obsidian)
Obsidian Git plugin hace pull/push automático. Sin acción manual necesaria.

## Prefijos de commit
- `hermes:` → cambios de Hermes
- `codex:` → cambios de Codex
- `clowy:` → cambios de Clowy
- `wolf:` → cambios de Wolf
- `polytrader:` → cambios de Polytrader
- `tien:` → cambios manuales de Tien

## Conflictos
Si hay merge conflict en push: `git pull --rebase origin master`, resolver, y push de nuevo.

## Repo
- **URL**: https://github.com/tiencousillas1-glitch/obsidian-vault
- **Branch**: master
- **Username**: tiencousillas1-glitch

## Archivos de estado (solo Agent-Codex)
- `Agent-Codex/autosync-status.md` — último sync timestamp
- `Agent-Codex/codex-autosync.log` — log de operaciones