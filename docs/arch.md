# Claude PM Kit — Architecture

**Version:** 0.5 | **Updated:** 2026-04-22

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
├── .claude/skills/                        # PM Twin skills
│   ├── pm/SKILL.md                        # Orchestrator: setup, status, next (includes Sprint Plan step)
│   ├── toolkit/SKILL.md                   # Intelligence Hub + Feature Tiers
│   ├── roadmap/SKILL.md                   # Product roadmap
│   ├── pitch/SKILL.md                     # Pitch materials
│   ├── metrics/SKILL.md                   # KPI definition + tracking
│   ├── stakeholder-update/SKILL.md        # Status reports
│   ├── userstudy/SKILL.md                 # User research plans
│   ├── qa-feature/SKILL.md                # Per-feature Playwright + self-heal
│   └── verify/SKILL.md                    # Sprint-boundary gate — orchestrates qa-feature + integration flows
├── docs/
│   ├── arch.md                            # This file
│   ├── PRD.md                             # Product requirements
│   ├── features/                          # Feature deep-dives
│   ├── plans/                             # Research + decisions
│   └── meta/                              # Ecosystem docs, persona definition
└── templates/                              # Planned — CSS + JS for HTML output
    └── (toolkit-base.css, calculator.js — created when /toolkit research is built)
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
| `/pm setup` | 0-1 | User's idea or existing project | Discovery, complexity assessment, feature parity, recommendation, PRD, journey flows | Built |
| `/pm status` | Any | Project state | Maturity scorecard | Built |
| `/pm next` | Any | Project state | Single highest-impact action | Built |
| `/toolkit research` | 3 | PRD + arch.md + web research | Intelligence Hub HTML (7-tab dashboard) | Built |
| `/toolkit features` | 2-3 | arch.md + tier selection | Production infrastructure (T1/T2/T3) | Built |
| `/toolkit hero` | 3 | PRD + discovery + journey flows | Public-facing landing/hero page | Built |
| `/toolkit help` | 3 | Journey flows + PRD features | In-app help section + onboarding wizard spec | Built |
| `/toolkit sales` | 3 | Intelligence Hub + PRD | One-pager, objection handlers, pitches, battle cards | Built |
| `/roadmap` | 1, 5 | PRD phases + feature index | Visual roadmap | Built |
| `/pitch` | 5 | Intelligence Hub data | Pitch deck outline + speaker notes | Built |
| `/metrics` | 5 | PRD + monitoring data | KPI definitions + report | Built |
| `/stakeholder-update` | 5 | Git history + arch.md | Status report (markdown or HTML) | Built |
| `/userstudy` | 5 | PRD | Research plan + interview script | Built |
| `/qa-feature` | 2 | Feature + journey flow | Playwright test, screenshots, self-heal 3x, per-feature QA report | Built |
| `/verify` | 2 | Sprint scope from sprint-plan.md | Sprint-boundary gate — per-feature QA + sprint integration run + aggregated evidence report | Draft |

---

## Key Patterns

1. **Research-first** — Every skill that makes recommendations does web research first, cites sources
2. **Gate-driven** — Phase 0 has Go/No-Go, Phase 1 has journey flow review. No skipping.
3. **Standalone output** — HTML pages (Intelligence Hub, hero) work offline, no server needed
4. **Kit delegation** — PM Twin checks for other kits, delegates when available, works alone when not
5. **Confidence tagging** — Every data point tagged: Verified, Estimated, Calculated, User-Provided
6. **`[PM Twin]` prefix** — All skill descriptions start with `[PM Twin]` for disambiguation
7. **Peer narration** — Show thinking by narrating, never lecture or teach frameworks
8. **Standard features auto-included** — Auth, RBAC, audit, dark mode, search in every PRD
9. **Feature parity assessment** — Competitive table (our MVP vs competitor A vs B) in every PRD
10. **Journey flows before code** — User reviews onboarding + core action flows before building starts
11. **Full artifact suite** — Discovery → PRD → flows → code → hero → help → sales toolkit
12. **User is CEO** — pmtwin is the entire product team (PM + eng + design + marketing + sales enablement)
7. **Peer narration tone** — PM Twin narrates its work ("Checking competitors...") rather than teaching PM theory. User absorbs product thinking by watching, not being lectured.

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
| 0.2 | 2026-04-15 | **QA + e2e hardening.** Fixed 3 blockers. Discovery: 4 new questions, peer narration tone. E2e trial vs DharmaLink: 7.5/10. |
| 0.3 | 2026-04-15 | **Security + token optimization.** ALWAYS/ASK/NEVER constraints, code gen security, intent branching, pm 290→205 lines. |
| 0.4 | 2026-04-15 | **Phase 2 hardening.** All 5 Phase 2 skills (roadmap, pitch, metrics, stakeholder-update, userstudy) hardened with prereq checks, safety rules, write-path constraints, existing-file-first patterns. QA grade: A (92%). |
| 0.5 | 2026-04-22 | **Auto-fetch + sprint gate.** `/pm` Step 2 now detects missing public kits and offers to clone project-kit into `~/.claude/kits/` on demand — one-clone install for new users. `/verify` sprint-boundary gate skill added, sprint planning step added to `/pm`. Skill count 9 → 10. Enables Greg-style internal pilots where cloning pm-kit alone bootstraps the full ecosystem. |
