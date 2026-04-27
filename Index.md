# Obsidian Vault — Tien's Second Brain

## Architecture: 4-Layer Memory System

| Layer | What | Auto-injected? |
|-------|------|-----------------|
| 1 | Built-in Memory (MEMORY.md) | ✅ Always |
| 2 | AGENTS.md + SOUL.md | ✅ Always |
| 3 | Obsidian Vault (this) | ❌ On-demand |
| 4 | Session Search | ❌ On-demand |

## Folder Structure

```
Agent-Shared/          ← Both agents read/write
  user-profile.md     ← Who Tien is, preferences, corrections
  project-state.md     ← All projects and status
  decisions-log.md     ← Shared decision history

Agent-Hermes/         ← Hermes private workspace
  working-context.md  ← What I'm actively doing
  mistakes.md          ← Things I've gotten wrong
  daily/              ← Daily logs (one per day)

Agent-OpenClaw/       ← OpenClaw's space (don't touch)
Agent-Clowy/          ← Clowy (COO) private workspace
Agent-Polytrader/     ← Polytrader private workspace
```

## Workflow

1. **Session start:** Read Agent-Shared/* + Agent-Hermes/working-context + today's daily log
2. **During work:** Checkpoint every 3-5 tool calls to vault
3. **Session end:** Flush working-context to daily log

## Last Updated
2026-04-23
