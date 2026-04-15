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

### Option A: Start fresh with PM Twin (recommended)

```bash
# 1. Clone the PM kit
git clone https://github.com/gmarmat/claude-pm-kit.git

# 2. Create your project folder
mkdir my-product && cd my-product
mkdir -p .claude/skills docs/toolkit

# 3. Copy PM Twin skills into your project
cp -r ../claude-pm-kit/.claude/skills/* .claude/skills/

# 4. Launch Claude Code
claude
```

Tell Claude: **"Run `/pm setup` — I want to build [your idea]"**

The PM Twin will interview you, research the market, and guide you through the full lifecycle. It will create `docs/PRD.md`, `docs/arch.md`, and other files as you go.

### Option B: Add to existing project

If you already have a project (built with [claude-project-kit](https://github.com/gmarmat/claude-project-kit) or on your own):

```bash
# Copy the skills you want
cp -r claude-pm-kit/.claude/skills/pm your-project/.claude/skills/
cp -r claude-pm-kit/.claude/skills/toolkit your-project/.claude/skills/

cd your-project && claude
```

- Have a PRD? → Run `/toolkit research` to generate your Intelligence Hub
- No PRD yet? → Run `/pm setup` and it will guide you

### What you need in your project

The PM Twin skills read these files (and create them if missing):

```
your-project/
├── .claude/skills/        ← PM Twin skills go here
│   ├── pm/
│   ├── toolkit/
│   └── ...
├── docs/
│   ├── PRD.md             ← /pm setup creates this
│   ├── arch.md            ← /pm setup creates this
│   └── toolkit/           ← /toolkit research writes output here
└── CLAUDE.md              ← optional but recommended
```

---

## Part of the Claude Kit Ecosystem

| Kit | Purpose | When |
|-----|---------|------|
| [claude-project-kit](https://github.com/gmarmat/claude-project-kit) | Bootstrap new projects | Day 0 |
| [claude-workspace-kit](https://github.com/gmarmat/claude-workspace-kit) | Manage multiple projects | Day 0 |
| [claude-project-rehab](https://github.com/gmarmat/claude-project-rehab) | Assess + upgrade **existing** projects, guide **new** ideas | Anytime |
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
