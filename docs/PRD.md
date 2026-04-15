# Claude PM Kit — Product Requirements Document

**Version:** 0.1 | **Updated:** 2026-04-14 | **Status:** Draft

---

## LLM Quick Start

- **What:** A digital PM twin — an always-available peer product manager that walks users through the full product lifecycle: discovery → validation → planning → building → productizing → launching → growing
- **Who:** Solo builders, indie hackers, small teams using Claude Code to build apps
- **Stack:** Claude Code skills (SKILL.md files) + standalone HTML generation + code scaffolding + deployment orchestration
- **Key constraint:** Must be generic (no personal/company data), work for ANY project type, and produce presentation-ready output
- **Data strategy:** Does live web research for market/competitive data, reads user's PRD + arch.md for context, orchestrates other kits (project-kit, workspace-kit, rehab) as needed
- **Unique angle:** The only tool that connects product thinking to product building in one continuous workflow. Other tools help you code faster — this helps you build the RIGHT thing.

---

## Executive Summary

Most people who build apps with AI jump straight to code. They skip market research, guess at pricing, ignore competitors, have no go-to-market plan, and never build production infrastructure. The result: technically functional apps that never become real products.

The PM Twin is a digital peer product manager that walks builders through the **entire product lifecycle** — from initial idea validation to launch and growth. It's not just another dev tool. It's the first tool that connects product thinking to product building in one continuous workflow.

Unlike static templates (Lean Canvas, PRD generators), the PM Twin actively researches your specific market, analyzes your actual competitors, models your real infrastructure costs, and packages everything into presentation-ready formats. It then orchestrates the build using the other Claude kits (project-kit, workspace-kit, rehab) and deploys to your hosting provider.

**The gap it fills:** Other tools help you code faster. The PM Twin helps you build the right thing — with the discipline of a $200K/year PM, available to anyone.

### Value Proposition

| Stakeholder | Value |
|-------------|-------|
| Solo builder | Goes from "I have an idea" to "I have a launched product with research, pricing, GTM, and a plan" — not just "I have code" |
| Small team | PM-quality discipline without hiring a PM. Discovery gates prevent building the wrong thing. |
| Indie hacker | Investor/pitch-ready materials generated from actual market research and real financials |
| Vibe coder | Guided end-to-end: idea → validation → build → launch. Can't skip the important parts. |
| Experienced PM | Digital twin that automates the research/documentation grind. Focuses PM time on strategy. |

### Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Intelligence Hub completeness | 7/7 tabs populated with real data | Tab count + source citation count |
| Research quality | 80%+ sources from reputable domains (.gov, .org, major pubs) | Source URL analysis |
| Time to generate | < 10 minutes for full Intelligence Hub | Skill execution time |
| Feature tier adoption | Users scaffold at least T1 after building core features | Opt-in rate |

---

## Problem Statement

### Current State

Builders using Claude Code (and the project kit) can bootstrap and build apps effectively. But the workflow ends at "code works." There's no structured path from "working app" to "viable product."

### Pain Points

| # | Pain Point | Who Feels It | Severity |
|---|-----------|-------------|----------|
| 1 | No market research — builders guess at TAM, don't know competitors | Solo builders | High |
| 2 | No pricing strategy — either free or random number | Indie hackers | High |
| 3 | No go-to-market plan — "I'll just post on Twitter" | Everyone | High |
| 4 | No production infrastructure — no analytics, no monitoring, no admin | Small teams | Medium |
| 5 | Can't pitch — no structured materials for investors/stakeholders | Builders seeking funding | High |
| 6 | Reinventing PM infrastructure — every app rebuilds settings, admin, A/B testing | Everyone | Medium |

### Desired State

After running `/toolkit`, a builder has:
- A researched, cited, interactive business intelligence dashboard they can open in a browser
- A pricing model grounded in real competitor data and their actual infrastructure costs
- A go-to-market plan with specific channels and messaging
- Presentation-ready materials they can show to investors, partners, or executives
- (Optionally) Production infrastructure scaffolded into their app

---

## Target Users & Roles

| Role | Description | Key Needs |
|------|-------------|-----------|
| Solo builder | One person building an app with Claude Code | Everything — market research, pricing, GTM, infrastructure |
| Indie hacker | Builder aiming to monetize | Pricing strategy, competitor analysis, pitch materials |
| Small team lead | Technical lead who also does PM work | Structured PM artifacts, stakeholder-ready docs |
| Vibe coder | New to structured development, using claude-project-kit | Guided workflow, can't be overwhelmed |

### Access Model

Open source. Users install by copying skills into their project's `.claude/skills/` directory, or by using the kit's scaffolding tools.

---

## Boundaries

| Category | Rule |
|----------|------|
| **ALWAYS** | Cite every data point with source URL and retrieval date |
| **ALWAYS** | Read user's PRD and arch.md before any research — context-aware, not generic |
| **ALWAYS** | Generate self-contained output (HTML opens without a server, docs work standalone) |
| **ASK FIRST** | Before generating code that modifies the user's app (feature tiers) |
| **ASK FIRST** | Before making pricing recommendations (present options, user decides) |
| **NEVER** | Include personal data, company names, or identifying info in templates |
| **NEVER** | Hardcode industry-specific data — all market data must be researched live |
| **NEVER** | Present research as authoritative fact — always note confidence level and sources |

---

## Core Concepts

| Concept | Definition | Relates To |
|---------|-----------|------------|
| PM Twin | Digital peer product manager — always-available, strategic, research-driven | The persona Claude adopts when PM kit skills are active |
| Product Lifecycle | 6 phases: Discovery → Plan → Build → Productize → Launch → Grow | The full journey PM Twin guides |
| Discovery Gate | Go/No-Go decision based on market research before any code is written | Phase 0 — prevents building the wrong thing |
| Intelligence Hub | Interactive HTML dashboard with 7 tabs of business intelligence | /toolkit research output |
| Feature Tiers | 3 levels of product infrastructure (MVP → Growth → Enterprise) | /toolkit features output |
| Confidence Level | Rating on data quality: Verified / Estimated / Calculated / User-Provided | All research output |
| Kit Orchestration | PM Twin fetches and uses other kits (project-kit, workspace-kit, rehab) as tools | /pm setup |

---

## Core Features

### Phase 0 — Discovery & Validation (before ANY code)

**Goal:** Research and validate the product idea before committing to building
**Priority:** P0 — this is the differentiator. No other tool does this.

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 0.1 | Problem interview | PM Twin asks 5-8 strategic questions to understand the problem space | P0 |
| 0.2 | Market research | WebSearch for TAM/SAM/SOM, industry size, growth rate. Cited sources. | P0 |
| 0.3 | Competitive analysis | Find 3-8 competitors, pricing, features, strengths/weaknesses. Comparison table. | P0 |
| 0.4 | Feasibility assessment | Recommend stack, estimate infra costs, estimate build time | P0 |
| 0.5 | Business model | Revenue model, pricing benchmarks from research, unit economics estimate | P0 |
| 0.6 | Go/No-Go scorecard | 6-factor score (problem, market, competition, differentiation, feasibility, business model). Explicit gate. | P0 |
| 0.7 | Discovery output | Save research to docs/toolkit/discovery.md + go-no-go.md with all sources | P0 |
| 0.8 | Pivot support | If No-Go: help user refine idea, explore adjacent angles, re-run discovery | P1 |

### Phase 1 — Plan & Scaffold

**Goal:** PRD-first planning, architecture decisions, project scaffolding, environment setup
**Priority:** P0
**Depends on:** Phase 0 Go decision (or user brings existing PRD)

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 1.1 | PRD creation (pre-filled) | PM Twin writes PRD from Phase 0 research — not a blank template. User confirms. | P0 |
| 1.2 | Architecture decisions | Use /advise for each major decision (auth, DB, hosting). Save to docs/plans/. | P0 |
| 1.3 | Kit orchestration | Fetch project-kit/workspace-kit if needed. Scaffold project via StartHere.md. | P0 |
| 1.4 | Environment detection | Detect required CLIs from stack. Check install + auth. Guide setup. | P0 |
| 1.5 | Resource creation | Create Supabase project, Railway project, GitHub repo as needed | P1 |
| 1.6 | Roadmap generation | Create prioritized sprint roadmap from PRD phases + features | P0 |

### Phase 2 — Build (guided development)

**Goal:** PM Twin advises during development, enforces discipline
**Priority:** P0
**Depends on:** Phase 1 scaffold complete

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 2.1 | Sprint guidance | Present current sprint features with specs and acceptance criteria | P0 |
| 2.2 | Build loop support | Works with project-kit skills: /startnow, /advise, /updatenow, /l3, /audit | P0 |
| 2.3 | Progress tracking | Track feature completion against roadmap. Show progress bars. | P1 |
| 2.4 | Quality nudges | Remind about commits, docs, tests, audits (advisory, not blocking) | P1 |

### Phase 3 — Productize (Intelligence Hub + Infrastructure)

**Goal:** Generate business intelligence and scaffold production infrastructure
**Priority:** P0

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 3.1 | Intelligence Hub | 7-tab HTML dashboard: market, competitive, pricing, GTM, technical, sales tools | P0 |
| 3.2 | Interactive calculator | Pricing/margin calculator with sensitivity sliders in HTML | P0 |
| 3.3 | Source citations | Every claim has collapsible source with URL + date + confidence tag | P0 |
| 3.4 | Feature Tiers T1 | KPI dashboard, settings system, audit log, health endpoint | P0 |
| 3.5 | Feature Tiers T2 | Analytics, monitoring, A/B testing, notifications | P1 |
| 3.6 | Feature Tiers T3 | Multi-tenant admin, RBAC, developer API, compliance | P2 |
| 3.7 | Pre-launch checklist | Security, performance, legal, analytics, monitoring, content, DNS checks | P0 |

### Phase 4 — Launch (deployment orchestration)

**Goal:** Deploy the app to production with proper infrastructure
**Priority:** P1

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 4.1 | Deploy to Railway | Create project, set env vars, deploy from git, generate domain, verify health | P1 |
| 4.2 | Deploy to Vercel | Link project, set env vars, deploy production, verify | P1 |
| 4.3 | Supabase production | Run migrations, verify RLS, set env vars | P1 |
| 4.4 | Smoke test | Hit health endpoint, test auth, verify DB, check public pages | P1 |
| 4.5 | Custom domain | Guide DNS setup for custom domain (optional) | P2 |
| 4.6 | Post-launch | Update Intelligence Hub with live URL, create git tag, generate status update | P1 |

### Phase 5 — Grow (ongoing PM support)

**Goal:** Continue as peer PM with ongoing product management capabilities
**Priority:** P1-P2

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 5.1 | /pm status | Product maturity scorecard across all phases | P1 |
| 5.2 | /pm next | Recommend single highest-impact next action | P1 |
| 5.3 | /stakeholder-update | Generate status report from git history + metrics | P1 |
| 5.4 | /roadmap | Visual roadmap, updateable as priorities shift | P1 |
| 5.5 | /metrics | Define, track, review KPIs (connects to T2 monitoring if scaffolded) | P2 |
| 5.6 | /pitch | Pitch deck outline from Intelligence Hub (investor/partner/enterprise/internal) | P2 |
| 5.7 | /userstudy | User research plan + interview script from PRD | P2 |
| 5.8 | Research refresh | Re-run market/competitive research to update Intelligence Hub | P2 |

---

## Non-Functional Requirements

| Category | Requirement | Target |
|----------|-------------|--------|
| **Performance** | Intelligence Hub generation | < 10 minutes including web research |
| **Portability** | HTML output | Opens in any modern browser, no server needed |
| **Print** | Intelligence Hub | Print-friendly CSS, looks good as PDF |
| **Accessibility** | HTML output | Semantic HTML, keyboard navigable tabs, screen reader friendly |
| **Offline** | HTML after generation | Works fully offline (Chart.js loaded from CDN at generation time, embedded in output) |
| **Security** | No secrets in output | Never include API keys, passwords, or .env values |

---

## Data Sources & Integrations

| Source | Type | Purpose | Auth | Rate Limits |
|--------|------|---------|------|-------------|
| User's PRD | Local file | Product context, domain, users | None | None |
| User's arch.md | Local file | Stack, costs, data model | None | None |
| Web search | WebSearch tool | Market data, competitors, pricing | Claude Code built-in | Standard |
| Web fetch | WebFetch tool | Deep-dive specific pages | Claude Code built-in | Standard |

### Data Flow

```
PRD + arch.md → Extract context → Web research (5-8 queries)
    → Synthesize findings → Ask user to confirm/correct
    → Generate HTML with all tabs → Save to docs/toolkit/index.html
    → Update arch.md with toolkit reference
```

---

## Cost Model

| Category | Cost | Notes |
|----------|------|-------|
| Infrastructure | $0 | Skills are text files, HTML is static |
| API costs | Claude Code session tokens | Same as any skill usage |
| Web research | Included in Claude Code | WebSearch is built-in |
| **Total** | **$0 incremental** | Only cost is Claude Code subscription |

---

## Out of Scope

| Feature | Why Not Now | Target Version |
|---------|-----------|----------------|
| Real-time data dashboards | Requires server infrastructure | Never (different tool) |
| CRM integration | Too specific, many CRM providers | v2 if demand |
| Financial modeling beyond pricing | Requires domain expertise | v2 |
| Multi-language research | English web search only for now | v2 |
| Automated competitor monitoring | Requires scheduled jobs | v2 |

---

## Open Questions

| # | Question | Impact | Status |
|---|----------|--------|--------|
| 1 | Should Chart.js be embedded in HTML or loaded from CDN? | Offline capability vs file size | Open — leaning embed for offline |
| 2 | How to handle non-SaaS products (hardware, services, content)? | Tab relevance varies | Open — need to make tabs adaptive |
| 3 | Should the skill support updating an existing Intelligence Hub? | UX for iterating | Open — leaning yes, overwrite with confirmation |
| 4 | How detailed should T2/T3 feature scaffolding be? | Build time vs value | Open — start with specs, add code gen later |
| 5 | Should the PM kit ship its own CLAUDE.md or inherit from workspace? | Independence vs integration | Open — leaning own CLAUDE.md |

---

## Technical References

| Doc | Purpose | Status |
|-----|---------|--------|
| `skills-inventory.md` | All planned skills with detailed I/O | Draft |
| `toolkit-research-flow.md` | Step-by-step research pipeline | Draft |
| `toolkit-features-flow.md` | Feature tier scaffolding flow | Planned |
| `html-prototype-spec.md` | HTML output specification | Planned |

---

## Revision History

| Ver | Date | Changes |
|-----|------|---------|
| 0.1 | 2026-04-14 | Initial draft from /advise session. Boris + PrepRight patterns analyzed. |
