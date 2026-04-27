# 📝 Decisions Log — AI Company

> Important decisions, rationale, and outcomes. Review weekly.

---

## 2026-04-24 — Create Wolf (CRO / Sales Agent)

**Decision:** Create Wolf as the first revenue-focused agent.

**Context:**
- Company needs consistent revenue ($100/week to start)
- Clowy was doing ops + sales → not focused
- Need dedicated agent for cold outreach & email marketing

**Alternatives Considered:**
1. Have Clowy do sales → rejected (dilutes ops focus)
2. Hire human VA → rejected (AI is faster/cheaper to start)
3. Create Scout (research) first → rejected (revenue > research)

**Rationale:**
- Revenue solves most problems
- Cold email is scalable and measurable
- Wolf can fund future agents (Scout, Quill, Pixel)

**Expected Outcome:**
- 200-500 emails/week
- 40%+ open rate, 10%+ reply rate
- $5k-20k/mes in closed deals

**Owner:** Tien (with Hermes approval)

**Status:** ✅ Done — Wolf created 2026-04-24

**Follow-up:**
- [ ] First campaign launch (TBD)
- [ ] First deal closed (TBD)
- [ ] Review metrics after 2 weeks

---

## 2026-04-24 — Mission Control Dashboard

**Decision:** Build Mission Control as central dashboard for agent management.

**Context:**
- Multiple agents need coordination
- No visibility into agent status/tasks
- Need single pane of glass for operations

**Features Built:**
- Agents section (create/manage agents)
- Tasks Kanban board
- Projects tracker
- Activity feed
- Workflow pipeline (Quill→Scout→Pixel→Echo)
- Calendar integration
- Memory/file browser

**Tech Stack:**
- Frontend: HTML/JS (single file)
- Backend: Python HTTP server (port 8080)
- Agent creation: Python backend (port 8081) → OpenClaw CLI
- Storage: localStorage (browser) + OpenClaw workspace

**URL:** http://100.111.136.58:8080/mission-control.html

**Status:** ✅ Deployed v7.0

**Next Steps:**
- [ ] Connect real OpenClaw API for live agent status
- [ ] Add sessions_send integration for agent comms
- [ ] Deploy to public domain

---

## Template for Future Decisions

### YYYY-MM-DD — [Decision Title]

**Decision:** [What was decided]

**Context:** [Situation that required the decision]

**Alternatives Considered:**
1. [Option A] → [Why rejected]
2. [Option B] → [Why rejected]

**Rationale:** [Why this option was chosen]

**Expected Outcome:** [What we expect to happen]

**Owner:** [Who is responsible]

**Status:** 🟡 In Progress / ✅ Done / ❌ Abandoned

**Follow-up:**
- [ ] [Task 1]
- [ ] [Task 2]

---

_Last updated: 2026-04-24_
