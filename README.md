# Claude PM Kit

**Your digital peer product manager.** From idea to launch — with research, strategy, and discipline at every step.

---

## What This Is

A set of Claude Code skills that act as a PM Twin — guiding you through the full product lifecycle. Not just code scaffolding. Actual market research, competitive analysis, pricing strategy, and go-to-market planning — researched live, cited with sources, and packaged into presentation-ready formats.

```
"I want to build X"
       │
       ▼
  ┌─ DISCOVERY ─────────────────┐
  │ Problem interview            │
  │ Market research (live)       │
  │ Competitive analysis (live)  │
  │ Go/No-Go scorecard           │
  └──────────────┬──────────────┘
                 ▼
  ┌─ PLAN ──────────────────────┐
  │ PRD (pre-filled from research)│
  │ Architecture decisions        │
  │ Environment setup             │
  │ Roadmap                       │
  └──────────────┬──────────────┘
                 ▼
  ┌─ BUILD ─────────────────────┐
  │ Sprint guidance               │
  │ Progress tracking             │
  └──────────────┬──────────────┘
                 ▼
  ┌─ PRODUCTIZE ────────────────┐
  │ Intelligence Hub (HTML)      │
  │ Production infrastructure    │
  │ Pre-launch checklist         │
  └──────────────┬──────────────┘
                 ▼
  ┌─ LAUNCH ────────────────────┐
  │ Deploy (Railway/Vercel)      │
  │ Smoke test                   │
  └──────────────┬──────────────┘
                 ▼
  ┌─ GROW ──────────────────────┐
  │ Metrics, roadmap, pitch      │
  │ Stakeholder updates          │
  └─────────────────────────────┘
```

---

## Skills

| Skill | What It Does |
|-------|-------------|
| `/pm setup` | Assess your project state, identify gaps, offer a plan |
| `/pm status` | Product maturity scorecard across all lifecycle phases |
| `/pm next` | Recommend the single highest-impact next action |
| `/toolkit research` | Generate PM Intelligence Hub — 7-tab HTML dashboard with market research, pricing, competitive analysis |
| `/toolkit features` | Scaffold production infrastructure (KPIs, analytics, admin, A/B testing) |
| `/roadmap` | Product roadmap from PRD phases |
| `/pitch` | Pitch materials for investors, partners, or stakeholders |
| `/metrics` | Define and track product KPIs |
| `/stakeholder-update` | Status reports from git history and feature progress |
| `/userstudy` | User research plans and interview scripts |

---

## How to Use

### Option A: Start with PM Twin (recommended)

Copy the PM kit skills into your project:

```bash
# Copy all PM Twin skills
cp -r claude-pm-kit/.claude/skills/pm your-project/.claude/skills/
cp -r claude-pm-kit/.claude/skills/toolkit your-project/.claude/skills/
cp -r claude-pm-kit/.claude/skills/roadmap your-project/.claude/skills/
# ... (copy whichever skills you want)

# Launch Claude Code in your project
cd your-project && claude
```

Tell Claude: "Run `/pm setup` — I want to build [your idea]"

### Option B: Add to existing project

If you already have a project built with [claude-project-kit](https://github.com/gmarmat/claude-project-kit):

```bash
# Copy PM skills into your existing project
cp -r claude-pm-kit/.claude/skills/toolkit your-project/.claude/skills/
cp -r claude-pm-kit/.claude/skills/pm your-project/.claude/skills/

cd your-project && claude
```

Run `/toolkit research` to generate your Intelligence Hub.

---

## Part of the Claude Kit Ecosystem

| Kit | Purpose | When |
|-----|---------|------|
| [claude-project-kit](https://github.com/gmarmat/claude-project-kit) | Bootstrap new projects | Day 0 |
| [claude-workspace-kit](https://github.com/gmarmat/claude-workspace-kit) | Manage multiple projects | Day 0 |
| [claude-project-rehab](https://github.com/gmarmat/claude-project-rehab) | Fix existing projects | Anytime |
| **claude-pm-kit** | **Product management** | **Idea → Launch → Growth** |

Each kit works independently. The PM Twin can orchestrate all of them when available.

---

## Requirements

- [Claude Code](https://claude.ai/claude-code) (CLI)
- A product idea (or an existing project)

---

## License

MIT

---

**Created by [gmarmat](https://github.com/gmarmat)**
