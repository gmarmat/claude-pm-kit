# Claude PM Kit — Architecture

**Version:** 0.1 | **Updated:** 2026-04-14

> **LLM Instructions:** Token-optimized project index. Tables over prose, self-contained sections.

---

## Quick Reference

### What Is This?

A Claude Code skill kit that acts as a digital PM twin — guiding builders through the full product lifecycle from idea to launched product. It actively researches markets, generates business intelligence, scaffolds production infrastructure, and orchestrates other Claude kits.

### Tech Stack

| Component | Technology | Notes |
|-----------|------------|-------|
| Runtime | Claude Code skills (SKILL.md) | No server, no build step |
| Research | WebSearch + WebFetch | Live market/competitive data |
| Output (HTML) | Vanilla JS + Chart.js + CSS custom properties | Self-contained, no framework |
| Output (code) | Stack-aware generation | Next.js + Supabase primary, specs for others |
| Kit orchestration | Bash + Git | Fetch/detect other kits |

### Project Structure

```
claude-pm-kit/
├── CLAUDE.md                              # PM Twin persona + rules
├── README.md                              # Public docs
├── .claude/skills/                        # The 7 PM Twin skills
│   ├── pm/SKILL.md                        # Orchestrator: setup, status, next
│   ├── toolkit/SKILL.md                   # Intelligence Hub + Feature Tiers
│   ├── roadmap/SKILL.md                   # Product roadmap
│   ├── pitch/SKILL.md                     # Pitch materials
│   ├── metrics/SKILL.md                   # KPI definition + tracking
│   ├── stakeholder-update/SKILL.md        # Status reports
│   └── userstudy/SKILL.md                # User research plans
├── docs/
│   ├── arch.md                            # This file
│   ├── PRD.md                             # Product requirements
│   ├── features/                          # Feature deep-dives
│   ├── plans/                             # Research + decisions
│   └── meta/                              # Ecosystem docs, persona definition
└── templates/
    ├── toolkit-base.css                   # Minimal CSS for HTML output
    └── calculator.js                      # Reusable pricing calculator logic
```

---

## Domain Concepts

| Concept | Description |
|---------|-------------|
| PM Twin | The persona Claude adopts — peer product manager |
| Product Lifecycle | 6 phases: Discovery → Plan → Build → Productize → Launch → Grow |
| Discovery Gate | Go/No-Go decision from market research — before any code |
| Intelligence Hub | 7-tab HTML dashboard with researched business intelligence |
| Feature Tiers | 3 levels of production infrastructure: T1 (MVP), T2 (Growth), T3 (Enterprise) |
| Confidence Level | Data quality tag: Verified / Estimated / Calculated / User-Provided |
| Kit Orchestration | PM Twin fetches + uses other kits (project-kit, workspace-kit, rehab) |

---

## Skill Index

| Skill | Phase | Input | Output | Status |
|-------|-------|-------|--------|--------|
| `/pm setup` | 0-1 | User's idea or existing project | Assessment + gap-fill plan | Planned |
| `/pm status` | Any | Project state | Maturity scorecard | Planned |
| `/pm next` | Any | Project state | Single highest-impact action | Planned |
| `/toolkit research` | 0, 3 | PRD + arch.md + web research | Intelligence Hub HTML | Planned |
| `/toolkit features` | 3 | arch.md + tier selection | Routes, components, migrations OR specs | Planned |
| `/roadmap` | 1, 5 | PRD phases + feature index | Visual roadmap | Planned |
| `/pitch` | 5 | Intelligence Hub data | Pitch deck outline + speaker notes | Planned |
| `/metrics` | 5 | PRD + monitoring data | KPI definitions + report | Planned |
| `/stakeholder-update` | 5 | Git history + arch.md | Status report (markdown or HTML) | Planned |
| `/userstudy` | 5 | PRD | Research plan + interview script | Planned |

---

## Key Patterns

1. **Research-first** — Every skill that makes recommendations does web research first, cites sources
2. **Gate-driven** — Phase 0 has an explicit Go/No-Go. Phase 1 has roadmap confirmation. No skipping.
3. **Standalone output** — HTML Intelligence Hub works offline, no server needed
4. **Kit delegation** — PM Twin checks for other kits, delegates when available, works alone when not
5. **Confidence tagging** — Every data point tagged: Verified, Estimated, Calculated, User-Provided
6. **`[PM Twin]` prefix** — All skill descriptions start with `[PM Twin]` for disambiguation

---

## Feature Index

| # | Feature | Doc | Status |
|---|---------|-----|--------|
| 1 | PM Orchestration (/pm) | [docs/features/pm-orchestration.md](./features/pm-orchestration.md) | Planned |
| 2 | Intelligence Hub (/toolkit research) | [docs/features/intelligence-hub.md](./features/intelligence-hub.md) | Planned |
| 3 | Feature Tiers (/toolkit features) | [docs/features/feature-tiers.md](./features/feature-tiers.md) | Planned |
| 4 | Roadmap | — | Planned |
| 5 | Pitch | — | Planned |
| 6 | Metrics | — | Planned |
| 7 | Stakeholder Update | — | Planned |
| 8 | User Study | — | Planned |

---

## Version History

| Ver | Date | Changes |
|-----|------|---------|
| 0.1 | 2026-04-14 | **Initial scaffold.** 7 skills planned. PRD drafted. Ecosystem designed. |
