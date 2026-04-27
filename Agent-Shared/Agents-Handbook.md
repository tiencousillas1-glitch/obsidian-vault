# 🏢 AI Company — Agents Handbook

> Welcome to the team. This is where we document everything about our AI agents.

---

## 📋 Table of Contents

- [[#Company Structure|Company Structure]]
- [[#Agent Roster|Agent Roster]]
- [[#Onboarding New Agents|Onboarding New Agents]]
- [[#Communication Protocols|Communication Protocols]]
- [[#Tools & Access|Tools & Access]]

---

## 🏗️ Company Structure

```
┌─────────────────────────────────────────┐
│              HERMES (CEO)               │
│   Strategy, Vision, Final Decisions     │
└─────────────────────────────────────────┘
                    │
        ┌───────────┴───────────┐
        │                       │
┌───────▼────────┐    ┌────────▼────────┐
│   CLOWY (COO)  │    │  WOLF (CRO)     │
│   Operations   │    │  Sales & Rev    │
│   Delivery     │    │  Email Marketing│
└────────────────┘    └─────────────────┘
```

### Leadership Team

| Agent | Role | Emoji | Workspace | Status |
|-------|------|-------|-----------|--------|
| **[[Agent-Hermes/Hermes Overview\|Hermes]]** | CEO | 📋 | `Agent-Hermes/` | ✅ Active |
| **[[Agent-Clowy/Clowy Overview\|Clowy]]** | COO | 🌟 | `Agent-Clowy/` | ✅ Active |
| **[[Agent-Wolf/Wolf Overview\|Wolf]]** | CRO | 🐺 | `Agent-Wolf/` | ✅ Active |

---

## 🤖 Agent Roster

### Active Agents

#### 1. Clowy 🌟 — COO
- **Created:** 2026-03-28
- **Model:** minimax/minimax-m2.7
- **Workspace:** `/home/tien/.openclaw/workspace/`
- **Channels:** Telegram, Discord
- **Status:** ✅ Active

**Responsibilities:**
- Operations management
- Delivery coordination
- Infrastructure maintenance
- Heartbeat checks

📁 **Files:** [[Agent-Clowy/Clowy Overview]]

---

#### 2. Wolf 🐺 — CRO
- **Created:** 2026-04-24
- **Model:** minimax/minimax-m2.7
- **Workspace:** `/home/tien/.openclaw/workspace/agents/wolf/`
- **Channels:** TBD
- **Status:** ✅ Active

**Responsibilities:**
- Cold email campaigns
- Sales copy & scripts
- Lead research & outreach
- Revenue generation

📁 **Files:** [[Agent-Wolf/Wolf Overview]]

---

### Future Agents (Planned)

| Role | Name | Emoji | Status | Priority |
|------|------|-------|--------|----------|
| Scout | Research Agent | 🔍 | 📝 Planned | Medium |
| Quill | Content Writer | ✍️ | 📝 Planned | Medium |
| Pixel | Designer | 🎨 | 📝 Planned | Low |
| Echo | Social Media | 📱 | 📝 Planned | Low |
| Codex | Developer | 💻 | 📝 Planned | Medium |

---

## 🆕 Onboarding New Agents

### Step 1: Create Agent Identity

Every new agent needs these files in their workspace:

```
agents/[agent-name]/
├── SOUL.md          # Personality, tone, principles
├── IDENTITY.md      # Role, capabilities, boundaries
├── USER.md          # About the human (Tien)
├── TOOLS.md         # Tools, permissions, limits
├── MEMORY.md        # Long-term memory
└── memory/
    └── YYYY-MM-DD.md # Daily notes
```

### Step 2: Register in OpenClaw

```bash
openclaw agents add [Name] \
  --model minimax/minimax-m2.7 \
  --workspace /home/tien/.openclaw/workspace/agents/[agent-name] \
  --non-interactive
```

### Step 3: Add to Mission Control

1. Open http://100.111.136.58:8080/mission-control.html
2. Go to Agents section (🤖)
3. Click "+ New Agent"
4. Fill in details

### Step 4: Update This Handbook

Add the new agent to the [[#Agent Roster|Agent Roster]] section above.

### Step 5: Create Obsidian Files

```
Agent-[Name]/
├── [Name] Overview.md    # Main dashboard
├── SOUL-[Name].md        # Personality
├── MEMORY-[Name].md      # Long-term memory
├── Campaigns-[Name].md   # Active campaigns
└── Scripts-[Name].md     # Templates & scripts
```

---

## 💬 Communication Protocols

### Discord Channels
- `#agent-comms` — Hermes ↔ Clowy ↔ Wolf coordination
- `#general` — General chat
- `#personal` — Tien's personal channel

### Telegram
- Direct messages to Tien
- Bot notifications

### Handoff Rules

1. **Sales → Ops:** Wolf hands off to Clowy for delivery
2. **Ops → Strategy:** Clowy escalates to Hermes for decisions
3. **Strategy → Sales:** Hermes sets targets, Wolf executes

---

## 🛠️ Tools & Access

### Shared Tools
- **OpenClaw Gateway** — Core infrastructure
- **Mission Control** — Dashboard & monitoring
- **Discord** — Inter-agent communication
- **Telegram** — Human communication
- **Obsidian Vault** — Documentation & memory

### Agent-Specific Tools

**Clowy:**
- File system access
- Shell exec
- Web search
- TTS/voice

**Wolf:**
- Email templates
- CRM (Notion/Airtable)
- Sales scripts
- Research tools

---

## 📚 Memory System

### 4-Layer Architecture

1. **Layer 1:** Agent workspace (`MEMORY.md`, `memory/*.md`)
2. **Layer 2:** Shared context (`Agent-Shared/`)
3. **Layer 3:** Obsidian Vault (`/home/tien/Obsidian Vault/`)
4. **Layer 4:** External docs (Notion, Google Docs)

### Sync Rules

- Daily notes sync between workspace and Obsidian
- Major decisions logged in `Agent-Shared/decisions-log.md`
- Project state tracked in `Agent-Shared/project-state.md`

---

## 🎯 Company Mission

**Build, sell and operate AI systems that produce real income.**

### Priorities
1. **Revenue** — Anything that brings money in
2. **Delivery** — Anything that keeps clients paying
3. **Automation** — Anything that removes manual work
4. **Margin** — Anything that improves speed or consistency

### Decision Filter

Before doing anything, ask:
> Does this sell, deliver, automate, or improve margin?
> If no → deprioritize or kill.

---

_Last updated: 2026-04-24_  
_Created by: Clowy 🌟_
