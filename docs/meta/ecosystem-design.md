# Claude Kit Ecosystem — The PM Twin Architecture

**Updated:** 2026-04-14 | **Version:** 0.2

---

## The Big Idea

The PM kit isn't kit #4 in a list. It's a **digital PM twin** — an always-available peer product manager that orchestrates all the other kits to help you build a real product, not just an app.

```
┌─────────────────────────────────────────────────────────────────┐
│                        PM TWIN (claude-pm-kit)                  │
│                                                                 │
│   Your digital peer product manager. Always available.          │
│   Thinks about your product strategically. Uses the other       │
│   kits as tools to execute.                                     │
│                                                                 │
│   ┌───────────────┐  ┌───────────────┐  ┌───────────────┐      │
│   │ project-kit   │  │ workspace-kit │  │ project-rehab │      │
│   │ (bootstrap)   │  │ (organize)    │  │ (fix)         │      │
│   │               │  │               │  │               │      │
│   │ PRD, arch,    │  │ multi-project │  │ 7-pillar      │      │
│   │ skills,       │  │ structure,    │  │ scoring,      │      │
│   │ design system │  │ shared skills │  │ gap analysis   │      │
│   └───────────────┘  └───────────────┘  └───────────────┘      │
│           ▲                  ▲                  ▲                │
│           │                  │                  │                │
│           └──────── PM Twin fetches, installs, orchestrates ────┘
│                                                                 │
│   PLUS its own capabilities:                                    │
│   • Market research & competitive analysis                      │
│   • Pricing & unit economics                                    │
│   • Go-to-market strategy                                       │
│   • Production infrastructure (KPIs, analytics, admin)          │
│   • Roadmap, metrics, pitch, stakeholder updates                │
└─────────────────────────────────────────────────────────────────┘
```

---

## Two Entry Points

### Entry Point A: Bottom-Up (Learn the tools, then combine)

The natural teaching order. Introduce one kit at a time:

```
1. project-kit    → "Here's how to start a project properly"
2. workspace-kit  → "Here's how to manage multiple projects"
3. rehab          → "Here's how to fix an existing project"
4. pm-kit         → "Here's your PM twin — it uses all of the above"
```

**Best for:** Content, tutorials, onboarding articles. Each kit has a clear standalone story.

### Entry Point B: Top-Down (Start with PM, it handles the rest)

The power-user path. The PM twin is the only thing you interact with:

```
User: "I have an idea for a fitness app"

PM Twin:
  1. Checks: Do you have a workspace? → No → Fetches workspace-kit, sets up ai-projects/
  2. Checks: Do you have a project? → No → Fetches project-kit, runs StartHere.md
  3. Guides you through PRD creation (as a PM would — asking the right questions)
  4. Checks: Supabase installed? Railway? → Guides environment setup
  5. Scaffolds architecture → You build core features
  6. Runs /toolkit research → Market analysis, competitors, pricing
  7. Runs /toolkit features → Production infrastructure
  8. Continues as your peer PM → roadmap, metrics, pitch, stakeholder updates
```

**Best for:** Users who want the full experience. "Give me a PM and let me build."

---

## How PM Twin Orchestrates

### Step 1: Assess Current State

When a user first invokes the PM twin (e.g., `/pm` or `/pmtwin`), it assesses:

```
┌─ ENVIRONMENT CHECK ──────────────────────────────────────┐
│                                                          │
│  Workspace:                                              │
│    ✗ No ai-projects/ structure found                     │
│    → Offer to set up via workspace-kit                   │
│                                                          │
│  Project:                                                │
│    ✗ No docs/PRD.md found                                │
│    → Offer to scaffold via project-kit OR create inline  │
│                                                          │
│  Project Health:                                         │
│    ? Existing code but no arch.md, no CLAUDE.md          │
│    → Offer to run rehab first                            │
│                                                          │
│  PM Artifacts:                                           │
│    ✗ No docs/toolkit/ (Intelligence Hub)                 │
│    ✗ No production infrastructure (admin, analytics)     │
│    → These are what PM Twin will create                  │
│                                                          │
│  Dependencies (kits):                                    │
│    project-kit:   ✗ not found locally                    │
│                   → clone from github.com/gmarmat/...    │
│    workspace-kit: ✗ not found locally                    │
│                   → clone from github.com/gmarmat/...    │
│    rehab:         ✗ not found locally                    │
│                   → clone from github.com/gmarmat/...    │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

### Step 2: Fill Gaps

Based on assessment, the PM twin offers a plan:

```
Here's what I recommend to get your product set up properly:

  1. [5 min]  Set up workspace structure (workspace-kit)
  2. [15 min] Create your PRD (I'll interview you like a PM would)
  3. [10 min] Scaffold project (project-kit: arch.md, skills, design system)
  4. [5 min]  Set up dev environment (detect + install tools)
  5. [you]    Build core features (I'll be here for /advise, /l3)
  6. [10 min] Generate Intelligence Hub (/toolkit research)
  7. [10 min] Scaffold production infrastructure (/toolkit features)

Want to start from step 1, or jump to where you are?
```

### Step 3: Act as Peer PM Throughout

The PM twin doesn't just set things up and leave. It stays as a peer PM:

| Situation | What PM Twin Does |
|-----------|-------------------|
| User starts a new feature | Asks: "Does this align with the PRD? Which phase is this?" |
| User is about to deploy | Suggests: "Run /audit first. Also, have you updated the Intelligence Hub?" |
| User hasn't committed in a while | Nudges: "You have 5 uncommitted files. Commit after each sub-task." |
| User asks "should I add X?" | Responds as a PM: "Let's check the PRD scope. Is this P0, P1, or P2?" |
| User wants to pitch | Generates pitch materials from Intelligence Hub data |
| User has been building for weeks | Suggests: "Time for a /stakeholder-update. Here's what shipped." |

---

## The 4 Kits — Revised Role Descriptions

| Kit | Old Role | **New Role (PM Twin Model)** |
|-----|----------|------------------------------|
| **project-kit** | Standalone bootstrap tool | **PM Twin's scaffolding engine** — called by PM twin to set up projects |
| **workspace-kit** | Standalone workspace organizer | **PM Twin's workspace engine** — called by PM twin to organize multi-project setups |
| **project-rehab** | Standalone project fixer | **PM Twin's diagnostic engine** — called by PM twin to assess and fix existing projects |
| **pm-kit** | Another tool in the chain | **The orchestrator** — the PM twin itself. Entry point for the full experience. |

**Each kit still works independently.** The PM twin adds an orchestration layer on top. Users who just want project-kit can use it alone. Users who want the full PM experience start with the PM twin.

---

## Kit Dependency Resolution

When PM twin needs another kit:

```
1. Check: Is kit available locally?
   → Look in parent directories, sibling folders, or ~/.claude/kits/
   
2. If not: Can we clone it?
   → gh repo clone gmarmat/claude-project-kit (public repos)
   → Prompt user with URL for private repos
   
3. If no git/gh: Manual fallback
   → "Download claude-project-kit from github.com/gmarmat/claude-project-kit
      and place it at [path]"
   
4. Cache location for fetched kits:
   → ~/.claude/kits/claude-project-kit/
   → ~/.claude/kits/claude-workspace-kit/
   → ~/.claude/kits/claude-project-rehab/
```

**Important:** PM twin never modifies the source kits. It copies files FROM them INTO the user's project.

---

## The PM Twin Persona

The PM twin isn't just a set of skills — it's a **persona** that Claude adopts when working with PM kit skills. This persona:

| Trait | How It Manifests |
|-------|-----------------|
| **Strategic thinker** | Always connects tasks to business goals, not just technical requirements |
| **Question-asker** | Challenges assumptions: "Who is this for? Why now? What's the alternative?" |
| **Research-driven** | Never guesses — always researches before recommending |
| **Structured** | Uses frameworks: TAM/SAM/SOM, RICE prioritization, competitive matrices |
| **Presentation-aware** | Outputs are always stakeholder-ready, not just developer-readable |
| **Pragmatic** | Knows when to say "ship it" vs "research more" — optimizes for learning |
| **Metrics-oriented** | Defines success criteria upfront, tracks progress against them |

**This persona is defined in the PM kit's CLAUDE.md** — it shapes how Claude responds when PM kit skills are active.

---

## Golden Use Case: Top-Down Flow (Detailed)

```
User: "I want to build a fitness tracking app"

PM TWIN: Let me help you think through this as a product, not just an app.

─── DISCOVERY (PM Twin asks questions) ───────────────────────

  "Who specifically is this for? Gym-goers, runners, yoga practitioners?"
  "What's the core problem? Tracking workouts, nutrition, progress, motivation?"
  "What exists today that they use? What's broken about those solutions?"
  "How would you make money? Subscription, freemium, one-time?"
  "What's your unfair advantage? Domain expertise, unique data, specific audience?"

  → User answers over 2-3 rounds

─── SETUP (PM Twin orchestrates) ─────────────────────────────

  PM Twin: "Great. Let me set up your project properly."
  
  1. Checks for workspace-kit → fetches if needed → sets up ai-projects/
  2. Checks for project-kit → fetches if needed
  3. Creates project: ai-projects/fitness-tracker/
  4. Generates PRD from discovery conversation
     (not a blank template — pre-filled from the PM conversation)
  5. Runs StartHere.md phases 1-5 (environment, PRD confirm, arch, skills)
  6. Detects stack needs: "PRD mentions Supabase → checking CLI..."
  7. First commit: "Initial project setup with PRD and architecture"

─── BUILD (PM Twin advises, user builds) ─────────────────────

  PM Twin: "Architecture is ready. Here's your feature roadmap from the PRD:
  
    P0 (MVP):
    1. User auth (magic links)
    2. Workout logging (CRUD)
    3. Progress dashboard
    
    P1 (Growth):
    4. Social sharing
    5. AI workout suggestions
    
    Start with feature 1. Run /advise if you need architecture guidance."
  
  User builds features using project-kit skills:
    /startnow → /advise → build → /updatenow → commit

─── PRODUCTIZE (PM Twin's core value) ────────────────────────

  PM Twin: "Core features are built. Time to make this a product.
            Running /toolkit research..."
  
  1. Reads PRD + arch.md for context
  2. Web searches: fitness app market, competitors, pricing, trends
  3. Generates Intelligence Hub (docs/toolkit/index.html)
     - Market: $15B fitness app market, 8% CAGR
     - Competitors: Strava, Nike Run Club, Strong, Fitbod
     - Pricing: Freemium with $9.99/mo pro tier (competitor avg: $12/mo)
     - GTM: Reddit fitness communities, Instagram fitness influencers
     - Technical: architecture summary from arch.md
     - Sales: elevator pitch, objection handlers
  
  PM Twin: "Intelligence Hub generated. Open docs/toolkit/index.html.
            Want me to scaffold production infrastructure? (/toolkit features)"
  
  2. Scaffolds T1: KPI dashboard, settings, audit log
  3. Suggests T2 when user has first users

─── ONGOING (PM Twin stays as peer PM) ───────────────────────

  Week 3: "You've shipped 5 features. Run /stakeholder-update?"
  Week 5: "10 users signed up. Time for T2? (analytics, monitoring)"
  Week 8: "Your competitor just raised Series A. Want me to refresh
           the competitive analysis in the Intelligence Hub?"
  Week 12: "You're pitching an investor. Run /pitch investor?"
```

---

## Revised Ecosystem Architecture

```
                    ┌──────────────────────────────┐
                    │         USER                  │
                    │   "I want to build X"         │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
              ┌─────────────────────────────────────────┐
              │            PM TWIN                       │
              │     (claude-pm-kit)                       │
              │                                          │
              │  Entry point: /pm or /pmtwin              │
              │  Persona: Peer Product Manager            │
              │                                          │
              │  Core skills:                             │
              │    /toolkit research  (Intelligence Hub)  │
              │    /toolkit features  (Infra scaffolding) │
              │    /roadmap          (Product roadmap)    │
              │    /metrics          (KPI definition)     │
              │    /pitch            (Pitch materials)    │
              │    /stakeholder-update (Status reports)   │
              │    /userstudy        (User research)      │
              │                                          │
              │  Orchestration:                           │
              │    /pm setup    (assess + fill gaps)      │
              │    /pm status   (where am I?)             │
              │    /pm next     (what should I do next?)  │
              │                                          │
              └────┬──────────┬──────────────┬──────────┘
                   │          │              │
          ┌────────▼───┐ ┌───▼────────┐ ┌───▼──────────┐
          │project-kit │ │workspace-kit│ │project-rehab │
          │            │ │             │ │              │
          │ Bootstrap  │ │ Organize    │ │ Diagnose     │
          │ PRD→arch→  │ │ multi-      │ │ 7-pillar     │
          │ skills→    │ │ project     │ │ score→fix    │
          │ design     │ │ structure   │ │              │
          └────────────┘ └─────────────┘ └──────────────┘
          
          Each works independently. PM Twin adds orchestration.
```

---

## PM Twin Orchestration Skills

These are **new skills unique to the PM kit** that manage the other kits:

### `/pm setup` — Assess and fill gaps

```
Reads current state → identifies what's missing → offers a plan:

  "You have code but no PRD. Let me help you write one."
  "You have a PRD but no architecture doc. Let me scaffold one."
  "You don't have a workspace structure. Want me to set one up?"
  "Your project could use a rehab. Want me to run a health check?"
  "You're ready for the Intelligence Hub. Want me to research your market?"
```

### `/pm status` — Where am I in the product lifecycle?

```
Checks all artifacts and presents a maturity scorecard:

  Project Setup:      ██████████ 100%  (PRD, arch, skills, CLAUDE.md)
  Core Features:      ████████░░  80%  (8/10 P0 features built)
  PM Intelligence:    ██░░░░░░░░  20%  (Hub exists but pricing tab empty)
  Infrastructure:     ████░░░░░░  40%  (T1 done, T2 not started)
  Launch Readiness:   ███░░░░░░░  30%  (no GTM execution, no metrics)
  
  Next recommended action: Complete pricing tab in Intelligence Hub
```

### `/pm next` — What should I do next?

```
Based on current state, recommends the single highest-impact action:

  "Your P0 features are done but you have no market research.
   Run /toolkit research before building P1 features.
   Why: Understanding the market might change your P1 priorities."
```

---

## How Each Kit Gets Discovered

| Scenario | PM Twin Behavior |
|----------|-----------------|
| **No kits installed** | PM twin works standalone. Generates PRD inline, scaffolds basic structure without project-kit. Mentions kits exist for full experience. |
| **project-kit local** | Uses it for scaffolding. Doesn't re-clone. |
| **workspace-kit local** | Uses it for multi-project structure. |
| **rehab local** | Uses it for health checks on existing code. |
| **All kits local** | Full orchestration — the golden path. |
| **No internet** | Works with local context only. Skips web research (warns user). Skips kit fetching (tells user to install manually). |

**Kit discovery order:**
```
1. Current directory (is this inside a kit-standard project?)
2. Parent directories (is there a workspace with kits?)
3. Sibling directories (are kits next to this project?)
4. ~/.claude/kits/ (global cache)
5. GitHub (fetch if not found locally)
```

---

## What the PM Kit Repo Contains

```
claude-pm-kit/
├── CLAUDE.md                              # PM Twin persona + rules
├── README.md                              # Public docs — what, why, how
├── LICENSE                                # MIT
├── .claude/
│   └── skills/
│       ├── toolkit/SKILL.md               # /toolkit research + features
│       ├── pm/SKILL.md                    # /pm setup + status + next (orchestrator)
│       ├── roadmap/SKILL.md               # /roadmap (Phase 2)
│       ├── stakeholder-update/SKILL.md    # /stakeholder-update (Phase 2)
│       ├── metrics/SKILL.md               # /metrics (Phase 2)
│       ├── pitch/SKILL.md                 # /pitch (Phase 2)
│       └── userstudy/SKILL.md             # /userstudy (Phase 2)
├── docs/
│   ├── arch.md                            # PM kit architecture
│   ├── PRD.md                             # PM kit PRD
│   ├── features/
│   │   ├── intelligence-hub.md            # Hub feature doc
│   │   ├── feature-tiers.md              # Tiers feature doc
│   │   └── pm-orchestration.md           # Orchestration feature doc
│   ├── plans/                             # Research + decisions
│   └── meta/
│       ├── ecosystem.md                   # How kits connect (this doc, cleaned up)
│       └── pm-persona.md                  # PM Twin persona definition
└── templates/
    ├── toolkit-base.css                   # Minimal CSS for HTML output
    └── calculator.js                      # Reusable pricing calculator logic
```

---

## Naming Decision

| Option | Pros | Cons |
|--------|------|------|
| `claude-pm-kit` | Matches trilogy pattern, clear | "PM" might not resonate with non-PMs |
| `claude-pm-twin` | Captures the "peer PM" concept | Breaks naming pattern |
| `claude-product-kit` | Broader appeal | Confusable with project-kit |

**Decision:** Repo name = `claude-pm-kit`, but the **concept/persona** is called **"PM Twin"** in docs and UI. The skill entry point is `/pm`.

```
Repo:     claude-pm-kit
Concept:  PM Twin
Skill:    /pm (orchestrator) + /toolkit (core work)
Tagline:  "Your digital peer product manager"
```

---

## Independence vs Integration

**Hard rule:** Every kit works alone. No kit fails if another isn't installed.

| Layer | Independent | Integrated (via PM Twin) |
|-------|-------------|--------------------------|
| project-kit | User runs StartHere.md manually | PM Twin runs it, pre-fills PRD from PM conversation |
| workspace-kit | User sets up folders manually | PM Twin sets up structure, places project correctly |
| rehab | User runs scoring manually | PM Twin runs health check, recommends rehab if score < 7 |
| pm-kit | User runs /toolkit manually | PM Twin orchestrates full lifecycle |

**The integration is optional and additive.** It never changes how the individual kits work. It just automates the "when to use which kit" decision.

---

## Open Questions (Revised)

| # | Question | Options | Leaning |
|---|----------|---------|---------|
| 1 | Should `/pm setup` auto-clone kits from GitHub? | Yes (auto) / Ask first / Manual only | Ask first — user should know what's being installed |
| 2 | Where do fetched kits live? | `~/.claude/kits/` (global) / sibling dirs / inside project | `~/.claude/kits/` for global reuse |
| 3 | Should PM Twin have its own `/startnow`? | Yes / No (use project-kit's) | Yes — `/pm status` IS its startnow |
| 4 | Public or private repo? | Public / Private | Public — the PM methodology is the selling point |
| 5 | Should PM Twin work without other kits at all? | Full standalone / Degraded mode / Require at least project-kit | Degraded mode — works but recommends kits for full experience |
| 6 | How opinionated should the PM persona be? | Advisory (options) / Directive (recommendations) / Adaptive (match user) | Adaptive — directive for beginners, advisory for experienced PMs |
