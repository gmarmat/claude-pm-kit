# Skills Inventory — Claude PM Kit

**Updated:** 2026-04-14

---

## Phase 1 Skills (P0)

### `/toolkit`

The core skill. Two modes via argument.

```yaml
---
name: toolkit
description: "Generate PM Intelligence Hub and scaffold product infrastructure"
argument-hint: "[research | features | features t1 | features t2 | features t3]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, Edit, Bash, WebSearch, WebFetch, AskUserQuestion
---
```

#### Mode: `/toolkit research`

**Purpose:** Generate a researched, cited, interactive PM Intelligence Hub as standalone HTML.

**Inputs:**
| Source | What It Reads | Why |
|--------|--------------|-----|
| `docs/PRD.md` | Product domain, target users, value prop, features, phases | Context for all research |
| `docs/arch.md` | Tech stack, data model, API routes, infrastructure | Technical tab + cost estimation |
| `CLAUDE.md` | Constraints, security model | Technical tab |
| User input | Infrastructure costs, pricing preferences | Pricing & Economics tab |

**Research Queries (5-8 web searches):**
```
1. "[domain] market size TAM SAM SOM 2025 2026"
2. "[domain] competitors alternatives comparison"
3. "[domain] SaaS pricing models benchmarks"  (or "[domain] pricing strategy" for non-SaaS)
4. "[domain] industry trends growth forecast"
5. "[domain] customer acquisition cost channels"
6. "[domain] [specific tech] adoption rate"     (if relevant)
7. "[domain] regulatory compliance requirements" (if relevant)
8. "[product type] unit economics benchmarks"    (if SaaS)
```

**Processing Steps:**
1. Read project context (PRD, arch.md, CLAUDE.md)
2. Extract: domain keywords, target audience, product type, tech stack
3. Run web searches (parallel where possible)
4. Synthesize findings into structured data per tab
5. Ask user to confirm/correct key findings (review gate)
6. Ask user for infrastructure costs if not in arch.md
7. Generate HTML with all 7 tabs
8. Save to `docs/toolkit/index.html`
9. Log sources to `docs/toolkit/sources.md`

**Output: 7-Tab HTML Dashboard**

| Tab | Content Generated | Data Sources | Interactive Elements |
|-----|-------------------|--------------|---------------------|
| Dashboard | Exec summary, key metrics, product positioning | PRD + synthesized research | Copy-to-clipboard summary |
| Market Analysis | TAM/SAM/SOM, segments, growth rate, trends | WebSearch queries 1, 4 | None (reference) |
| Competitive Landscape | 3-8 competitors table, positioning matrix, differentiation | WebSearch query 2 | Sortable/filterable table |
| Pricing & Economics | Tiers, cost structure, margins, unit economics | User input + WebSearch query 3, 8 | Sensitivity sliders, margin calculator |
| Go-to-Market | Channels, messaging, timeline, early adopter strategy | WebSearch queries 4, 5 | Launch checklist |
| Technical | Architecture summary, security, integrations, scale plan | arch.md + feature docs | Collapsible deep dives |
| Sales Tools | Calculator, talking points, objection handlers, elevator pitch | All above synthesized | Interactive deal calculator |

**Confidence Tagging:**
Every data point gets a confidence tag:
- `[Verified]` — Multiple reputable sources agree
- `[Estimated]` — Single source or industry benchmark applied
- `[Calculated]` — Derived from user's data + benchmarks
- `[User-Provided]` — Direct from user input

---

#### Mode: `/toolkit features [tier]`

**Purpose:** Scaffold product infrastructure into the user's app.

**Inputs:**
| Source | What It Reads | Why |
|--------|--------------|-----|
| `docs/arch.md` | Tech stack, existing routes, data model | Know what to generate |
| `docs/PRD.md` | Features, phases | Know what's already planned |
| User input | Which tier(s) to scaffold | Scope control |

**Tier Definitions:**

**T1: MVP (Every app needs this)**
| Component | What Gets Generated | DB | Routes |
|-----------|-------------------|-----|--------|
| KPI Dashboard | Key metrics cards from existing data model | — (uses existing tables) | `/admin` or `/admin/dashboard` |
| Settings System | User preferences, theme, profile | `user_settings` | `/settings/*` |
| Audit Log | Track important user/system actions | `audit_log` | `/admin/audit` |
| Version Display | Version in footer + settings page | `lib/version.ts` or equivalent | — |
| Health Endpoint | Simple `/api/health` for monitoring | — | `/api/health` |

**T2: Growth (After you have users)**
| Component | What Gets Generated | DB | Routes |
|-----------|-------------------|-----|--------|
| Analytics Dashboard | Usage trends, feature adoption, DAU/MAU | `analytics_events` | `/admin/analytics` |
| Cost Monitoring | API/infra spend tracking, cache performance | `operation_metrics`, `cache_metrics` | `/admin/monitoring` |
| A/B Testing | Experiments, variants, deterministic assignment | `experiments`, `variants`, `user_variants` | `/admin/experiments` |
| Notification Prefs | Email/push/in-app notification settings | `notification_preferences` | `/settings/notifications` |
| Error Tracking | Error aggregation and alerting | `error_log` | `/admin/errors` |

**T3: Enterprise (When selling to organizations)**
| Component | What Gets Generated | DB | Routes |
|-----------|-------------------|-----|--------|
| Multi-Tenant Admin | Tenant CRUD, data isolation | `tenants` + RLS policies | `/admin/tenants` |
| User Management | Invite, roles, deactivate | RBAC tables | `/admin/users` |
| RBAC System | Role-based route/feature guards | `roles`, `permissions`, `user_roles` | Middleware |
| Developer Portal | API key management, usage, docs | `api_keys`, `api_usage` | `/settings/developer` |
| Compliance | Data export, retention, GDPR controls | `data_exports`, `consent_log` | `/settings/privacy` |

**Output Options (based on detected stack):**

| Stack Detected | Output Type | What's Generated |
|----------------|-------------|------------------|
| Next.js + Supabase | Full scaffolding | Routes, components, API endpoints, DB migrations, RLS policies |
| Next.js + other DB | Partial scaffolding | Routes, components, API endpoints + DB spec doc |
| Other framework | Spec document | `docs/features/product-infrastructure.md` with detailed specs |
| Non-web app | Spec document | Same spec doc, web infrastructure sections marked N/A |

---

## Phase 2 Skills (P1-P2, Future)

### `/roadmap`

```yaml
---
name: roadmap
description: "Generate visual product roadmap from PRD phases and feature index"
argument-hint: "[quarter | month | sprint]"
allowed-tools: Read, Glob, Grep, Write
---
```

**What it does:**
- Reads PRD phases + arch.md feature index
- Generates a visual roadmap (HTML timeline or Mermaid diagram)
- Tracks: features by phase, dependencies, completion status
- Output: `docs/toolkit/roadmap.html` or Mermaid in markdown

---

### `/stakeholder-update`

```yaml
---
name: stakeholder-update
description: "Generate product status update from recent activity"
argument-hint: "[weekly | monthly | custom-range]"
allowed-tools: Read, Glob, Grep, Write, Bash
---
```

**What it does:**
- Reads git log for recent commits
- Reads arch.md version history for completed features
- Reads any updated feature docs
- Generates a structured status update:
  - What shipped this period
  - What's in progress
  - What's blocked
  - Key metrics (if monitoring data exists)
  - Next priorities
- Output: Markdown (copyable to email/Slack) or HTML

---

### `/metrics`

```yaml
---
name: metrics
description: "Define and review product metrics — KPIs, funnels, health indicators"
argument-hint: "[define | review | report]"
allowed-tools: Read, Glob, Grep, Write, Bash
---
```

**What it does:**
- `define`: Walk through metric definition (name, query, target, owner)
- `review`: Check current metrics against targets (reads from monitoring tables if T2 is scaffolded)
- `report`: Generate metrics report (HTML or markdown)
- Stores metric definitions in `docs/toolkit/metrics.yaml`

---

### `/pitch`

```yaml
---
name: pitch
description: "Generate pitch deck outline from Intelligence Hub data"
argument-hint: "[investor | partner | enterprise | internal]"
allowed-tools: Read, Glob, Grep, Write, WebSearch
---
```

**What it does:**
- Reads Intelligence Hub HTML (must run `/toolkit research` first)
- Generates pitch deck outline tailored to audience:
  - Investor: Problem, solution, market, traction, team, ask
  - Partner: Integration value, technical fit, mutual benefit
  - Enterprise: ROI, security, compliance, support
  - Internal: Status, roadmap, resource needs
- Output: Markdown outline + speaker notes (user creates slides from this)

---

### `/userstudy`

```yaml
---
name: userstudy
description: "Generate user research plan and interview script from PRD"
argument-hint: "[discovery | usability | feedback]"
allowed-tools: Read, Glob, Grep, Write, WebSearch
---
```

**What it does:**
- Reads PRD for user roles, pain points, features
- Generates:
  - Research plan (goals, methodology, sample size, timeline)
  - Interview script (intro, warm-up, core questions, probes, wrap-up)
  - Survey template (if quantitative)
  - Analysis framework (themes to look for)
- Output: Markdown docs in `docs/toolkit/research/`

---

## Skill Dependency Map

```
/toolkit research  ←── Required first (generates Intelligence Hub)
    ↓
/toolkit features  ←── Uses same context, optional
    ↓
/roadmap           ←── Reads PRD + arch.md (independent)
/metrics           ←── Better with T2 features scaffolded
/stakeholder-update ←── Better with git history + metrics
/pitch             ←── Requires Intelligence Hub data
/userstudy         ←── Independent (reads PRD only)
```

---

## Kit Structure (Planned)

```
claude-pm-kit/
├── CLAUDE.md                           # Project rules
├── README.md                           # Public docs
├── .claude/
│   └── skills/
│       └── toolkit/SKILL.md            # Phase 1: core skill
│       └── roadmap/SKILL.md            # Phase 2
│       └── stakeholder-update/SKILL.md # Phase 2
│       └── metrics/SKILL.md            # Phase 2
│       └── pitch/SKILL.md              # Phase 2
│       └── userstudy/SKILL.md          # Phase 2
├── docs/
│   ├── arch.md                         # Architecture
│   ├── PRD.md                          # This PRD (adapted)
│   ├── features/
│   │   ├── intelligence-hub.md         # Hub feature doc
│   │   └── feature-tiers.md            # Tiers feature doc
│   └── plans/                          # Research + decisions
└── templates/
    ├── toolkit-base.css                # Minimal CSS for HTML output
    └── calculator.js                   # Reusable pricing calculator logic
```
