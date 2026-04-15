# PM Twin — Full Product Lifecycle

**Updated:** 2026-04-14

---

## The Core Insight

Real product managers don't start with code. They start with research, validation, and gates. Most builders skip ALL of this and jump straight to building. The PM Twin enforces the same discipline a $200K/year PM would — but as a digital peer available to anyone.

```
What builders do:           What a PM does first:
                            
"I have an idea" ──────►    1. Is this a real problem?
       │                    2. Who has this problem?
       │                    3. How big is the market?
       │                    4. Who else is solving it?
       │                    5. Can we win? Why us?
       │                    6. How does it make money?
       │                    7. What's the MVP scope?
       │                    8. Go / No-Go decision
       ▼                           │
  Start coding              THEN start coding
  (skip everything)                │
       │                           ▼
       ▼                    Build → Launch → Grow
  "Why doesn't              with data, strategy,
   anyone use this?"         and a plan
```

---

## The 6 Phases

### Phase 0: Discovery & Validation (Before ANY code)

**PM Twin acts as:** Strategic advisor / market researcher

**User says:** "I want to build a fitness tracking app"

**PM Twin does:**

```
STEP 1: Problem Interview (5-10 min conversation)
─────────────────────────────────────────────────
  "Let me understand this before we build anything."
  
  • Who specifically has this problem?
  • How do they solve it today?
  • What's broken about current solutions?
  • Why would someone switch to yours?
  • How did you discover this problem? (lived experience? observation? data?)
  • What's your unfair advantage? (domain expertise? audience? tech?)

STEP 2: Market Research (automated)
────────────────────────────────────
  • WebSearch: market size, TAM/SAM/SOM
  • WebSearch: industry trends, growth rate
  • WebSearch: adjacent markets, tailwinds
  
  → Present findings:
    "The fitness app market is $15.2B (2025), growing 8.5% CAGR.
     However, the 'workout logging' segment is mature and crowded.
     The opportunity I see is in [niche the user described]."

STEP 3: Competitive Landscape (automated)
──────────────────────────────────────────
  • WebSearch: direct competitors
  • WebSearch: indirect alternatives
  • WebFetch: competitor pricing pages
  
  → Present competitive matrix:
    | Competitor | Pricing | Users | Strength | Weakness |
    |------------|---------|-------|----------|----------|
    | Strava     | Free/$8 | 100M  | Social   | Not gym  |
    | Strong     | Free/$5 | 5M    | Gym UX   | No social|
    | ...        | ...     | ...   | ...      | ...      |
    
    "Your differentiation is [X]. No competitor does this well."

STEP 4: Feasibility Check (automated + conversation)
──────────────────────────────────────────────────────
  • What tech stack fits this? (recommend based on requirements)
  • What will infrastructure cost? (estimate from stack)
  • How long to build MVP? (estimate from feature scope)
  • What external APIs/services needed? (maps, AI, payments, etc.)
  
  → "Estimated MVP: 3-4 weeks with Claude Code.
     Stack recommendation: Next.js + Supabase + Railway.
     Infra cost: ~$25/month at launch, scales to ~$100 at 1K users."

STEP 5: Business Model (conversation + research)
──────────────────────────────────────────────────
  • Revenue model: subscription, freemium, usage-based, ads?
  • Pricing benchmarks from competitor research
  • Unit economics estimation
  • Cost structure projection
  
  → "Based on competitors ($5-15/mo range) and your infra costs ($25/mo),
     I'd recommend freemium with $7.99/mo pro tier.
     Break-even at ~4 paying users. Gross margin: 92% at 100 users."

STEP 6: Go / No-Go Gate
─────────────────────────
  Present summary scorecard:
  
  | Factor            | Score | Notes                           |
  |-------------------|-------|---------------------------------|
  | Problem clarity   | 8/10  | Clear pain point, lived experience |
  | Market size       | 7/10  | $15B but crowded                |
  | Competition       | 6/10  | Many players, niche is open     |
  | Differentiation   | 8/10  | Unique angle on [X]             |
  | Feasibility       | 9/10  | Standard stack, 3-4 week MVP    |
  | Business model    | 7/10  | Proven model, good unit economics|
  | ─────────────     | ───── | ─────────────────────────────── |
  | **Overall**       | **7.5/10** | **Recommend: GO**          |
  
  "Based on my research, this is worth building. The market is large,
   your differentiation is real, and the economics work.
   
   Main risk: crowded space. Mitigation: focus on [niche] and nail the UX.
   
   Ready to proceed? Or want to explore a different angle?"

GATE: User must explicitly say GO before PM Twin proceeds to Phase 1.
      If NO-GO: PM Twin helps pivot or refine the idea. Loop back to Step 1.
```

**Output from Phase 0:**
- `docs/toolkit/discovery.md` — Full research log with sources
- `docs/toolkit/go-no-go.md` — Scorecard + decision rationale
- User's confidence that this is worth building (or a pivot decision)

---

### Phase 1: Plan & Scaffold (PRD-first, then architecture)

**PM Twin acts as:** Product planner / technical architect

```
STEP 1: PRD Creation (PM Twin interviews, then writes)
───────────────────────────────────────────────────────
  NOT a blank template. PM Twin writes the PRD from the Phase 0 research:
  
  • Pre-fills: problem statement, target users, value prop (from discovery)
  • Pre-fills: competitive context, pricing model (from research)
  • Pre-fills: boundaries (ALWAYS/ASK/NEVER) based on constraints discussed
  • Asks user to confirm/edit each section
  • Iterates 2-3 rounds until PRD is solid
  
  → Save: docs/PRD.md (pre-filled, not a template)

STEP 2: Architecture Decisions (PM Twin uses /advise)
──────────────────────────────────────────────────────
  For each major technical decision:
  • Stack selection (if not already decided in Phase 0)
  • Auth model (magic links? OAuth? API keys?)
  • Database design (relational? document? graph?)
  • Hosting strategy (serverless? containers? edge?)
  • Third-party integrations
  
  Each decision goes through /advise: research → options → recommend → user decides
  
  → Save: docs/plans/YYYY-MM-DD-[decision].md (for each decision)

STEP 3: Project Scaffold (PM Twin uses project-kit)
─────────────────────────────────────────────────────
  • Checks for workspace-kit → sets up workspace if needed
  • Fetches project-kit if not local
  • Runs StartHere.md phases:
    - Environment check (detect + install CLIs)
    - PRD is already written (skip interview — just confirm)
    - Scaffold arch.md from PRD + architecture decisions
    - Customize skills
    - Design system (ask user)
  • Sets up git repo + GitHub remote
  
  → Output: Fully scaffolded project, ready to build

STEP 4: Environment Setup (PM Twin detects + guides)
──────────────────────────────────────────────────────
  • Detect required services from arch.md stack
  • Check CLIs: supabase, railway, vercel, gh, stripe, etc.
  • Guide account creation with direct signup URLs
  • Verify authentication: run check commands
  • Create initial resources:
    - Supabase project (if Supabase stack)
    - Railway project (if Railway hosting)
    - GitHub repo (if not created)
  
  → Output: All services authenticated and linked

STEP 5: Roadmap (PM Twin creates from PRD)
───────────────────────────────────────────
  • Read PRD phases + features
  • Create prioritized roadmap:
    Sprint 1: [P0 features — core value]
    Sprint 2: [P0 features — supporting]
    Sprint 3: [P1 features — growth]
    ...
  
  → Save: docs/toolkit/roadmap.md
```

**Gate:** User confirms roadmap before building starts.

---

### Phase 2: Build (PM Twin advises, user builds)

**PM Twin acts as:** Development advisor / quality gate

```
EACH SPRINT/FEATURE:
─────────────────────
  PM Twin: "Sprint 1, Feature 1: [name]
            Spec: docs/features/[name].md
            Acceptance criteria: [from PRD]
            
            Start with /startnow to load context."
  
  User builds using project-kit skills:
    /startnow → /advise (if needed) → build → test → commit → /updatenow
  
  PM Twin checks quality:
    • "Did you test in the browser?"
    • "Does this match the acceptance criteria?"
    • "Run /audit before moving to the next feature"
  
  After each feature:
    PM Twin updates roadmap progress:
    "Sprint 1: ██████░░░░ 60% — Feature 1 ✓, Feature 2 in progress"
```

**PM Twin nudges (not enforces):**
- Uncommitted changes for > 30 minutes → "Commit what you have"
- Skipped /updatenow → "Docs are getting stale — run /updatenow"
- Building P1 before P0 is done → "P0 Feature X isn't done yet. Finish MVP first?"
- No tests written → "Consider adding tests for [critical path]"

---

### Phase 3: Productize (PM Twin's core new value)

**PM Twin acts as:** Business strategist / PM toolkit builder

```
STEP 1: Intelligence Hub (/toolkit research)
──────────────────────────────────────────────
  • Refreshes Phase 0 research with current data
  • Generates 7-tab HTML dashboard
  • Interactive pricing calculator
  • All sources cited
  
  → Output: docs/toolkit/index.html

STEP 2: Production Infrastructure (/toolkit features)
──────────────────────────────────────────────────────
  • Scaffold T1: KPI dashboard, settings, audit log, health endpoint
  • Recommend T2 when user has first users
  
  → Output: New routes, components, migrations

STEP 3: Pre-Launch Checklist
─────────────────────────────
  PM Twin generates and walks through:
  
  | Category | Check | Status |
  |----------|-------|--------|
  | Security | /audit security passed | ☐ |
  | Security | No secrets in code | ☐ |
  | Security | RLS on all tables | ☐ |
  | Performance | Page load < 3s | ☐ |
  | Performance | API response < 500ms | ☐ |
  | Legal | Privacy policy page | ☐ |
  | Legal | Terms of service page | ☐ |
  | Analytics | Basic usage tracking | ☐ |
  | Monitoring | Health endpoint | ☐ |
  | Monitoring | Error alerting | ☐ |
  | Content | Landing page copy | ☐ |
  | Content | Meta tags / OG images | ☐ |
  | DNS | Custom domain ready | ☐ |
```

---

### Phase 4: Launch (PM Twin deploys)

**PM Twin acts as:** DevOps / launch coordinator

```
STEP 1: Deploy Infrastructure
───────────────────────────────
  Based on arch.md stack:
  
  IF Supabase:
    • Verify Supabase project exists
    • Run pending migrations
    • Verify RLS policies applied
    • Set environment variables
  
  IF Railway:
    • Create Railway project (or link existing)
    • Set environment variables
    • Deploy from git
    • Generate domain
    • Verify health endpoint responds
  
  IF Vercel:
    • Link project (vercel link)
    • Set environment variables
    • Deploy (vercel --prod)
    • Verify deployment

STEP 2: Domain & DNS
─────────────────────
  • Generate Railway/Vercel domain (free subdomain)
  • Ask: "Do you have a custom domain?"
    → Yes: guide DNS configuration
    → No: "Ship with the free domain. Add custom later."

STEP 3: Smoke Test
───────────────────
  • Hit health endpoint
  • Test auth flow (if auth exists)
  • Verify DB connectivity
  • Check public pages load
  
  → Report:
    "Deployment successful.
     URL: https://your-app.up.railway.app
     Health: ✓ 200 OK
     Auth: ✓ login/signup working
     DB: ✓ connected, RLS active
     
     Your app is live."

STEP 4: Post-Launch
────────────────────
  • Update Intelligence Hub with live URL
  • Generate initial /stakeholder-update
  • Set up monitoring baseline
  • Create "launch day" git tag
```

---

### Phase 5: Grow (PM Twin stays as ongoing peer PM)

**PM Twin acts as:** Growth advisor / ongoing PM

```
ONGOING CAPABILITIES:
─────────────────────

  Weekly:
    /pm status        → Product maturity scorecard
    /pm next          → Highest-impact next action
  
  As needed:
    /toolkit research → Refresh market data (competitor raised? market shifted?)
    /toolkit features → Add T2/T3 infrastructure as product matures
    /stakeholder-update → Status reports from git history
    /metrics          → Define, track, review KPIs
    /roadmap          → Update roadmap as priorities shift
  
  When pitching:
    /pitch investor   → Pitch deck outline from Intelligence Hub
    /pitch partner    → Partnership proposal
  
  When researching:
    /userstudy        → User research plan + interview script
    /advise [topic]   → Any product decision
```

---

## Phase Summary

| Phase | PM Twin Role | Key Output | Kits Used | Gate |
|-------|-------------|------------|-----------|------|
| **0. Discovery** | Market researcher | Research log + Go/No-Go scorecard | pm-kit only | User says GO |
| **1. Plan** | Product planner | PRD + arch.md + scaffolded project + environment | project-kit, workspace-kit | User confirms roadmap |
| **2. Build** | Dev advisor | Working app with docs | project-kit skills | Acceptance criteria met |
| **3. Productize** | Business strategist | Intelligence Hub + production infra + pre-launch checklist | pm-kit | Checklist complete |
| **4. Launch** | DevOps coordinator | Deployed app + live URL | pm-kit + MCP tools | Smoke test passes |
| **5. Grow** | Ongoing PM | Metrics, roadmap, stakeholder updates, pitch materials | pm-kit | Ongoing |

---

## What Makes This Different from Everything Else

| Tool | What It Does | Gap |
|------|-------------|-----|
| Claude Code | Writes code | No PM methodology |
| project-kit | Scaffolds projects | Starts at code, skips discovery |
| ChatPRD | Generates PRDs | Just a template, no research |
| Lean Canvas tools | Business model canvas | Static, no code integration |
| Vercel/Railway | Deploys apps | Just deployment, no PM workflow |
| **PM Twin** | **Full lifecycle: discover → validate → plan → build → productize → launch → grow** | **None — this is the gap** |

The PM Twin is the first tool that connects **product thinking** to **product building** in one continuous workflow. It doesn't just help you write code faster — it helps you build the **right thing** and launch it properly.

---

## The Tagline

> **PM Twin: Your digital peer product manager.**
> From idea to launch — with research, strategy, and discipline at every step.

---

## Conversation Examples (Top-Down Path)

### Example 1: Completely New Idea

```
User: I want to build a tool that helps landlords manage maintenance requests

PM Twin: Great — let me help you think through this as a product before we write
any code. I'll research the market, analyze competitors, and validate the business
model. Then we'll build it properly.

Let's start with discovery. A few questions:

1. Are you a landlord yourself, or how did you encounter this problem?
2. How many properties are we talking? 1-5 units? 50+? 500+?
3. What do landlords use today for maintenance? (spreadsheets, email, existing apps?)

[... 5-10 min PM interview ...]

PM Twin: Based on our conversation and my research:

  Market: Property management software is a $22B market (2025)
  Segment: Small landlords (1-50 units) are underserved — most tools target enterprise
  Competitors: Buildium ($55/mo), TenantCloud (free/$12), Avail ($0/$5/unit)
  Gap: No tool does AI-powered maintenance triage for small landlords
  Revenue: $15-25/mo per landlord, freemium for < 5 units
  
  Go/No-Go Score: 8.1/10 — RECOMMEND GO
  
  Shall I proceed with planning?
```

### Example 2: Existing Messy Project

```
User: I already built a recipe app but it's a mess. Can you help me turn it into a real product?

PM Twin: Let me assess what you have first.

  [Reads codebase]
  
  Project Health:
    Code:          exists (Next.js + Prisma)
    PRD:           ✗ missing
    Architecture:  ✗ no arch.md
    Skills:        ✗ none
    Tests:         ✗ none
    Docs:          ✗ none
    PM artifacts:  ✗ none
  
  I'd recommend starting with a rehab to get the project to standard,
  then we'll do discovery and productize it.
  
  Plan:
    1. Run rehab (7-pillar scoring + fixes) — ~30 min
    2. Discovery interview (market research for recipe apps) — ~15 min
    3. Write PRD from your existing features + research — ~15 min
    4. Generate Intelligence Hub — ~10 min
    5. Add production infrastructure — ~10 min
    6. Deploy properly — ~10 min
  
  Start with step 1?
```

### Example 3: Just Wants Research

```
User: I'm not ready to build yet. I just want to research if a pet care marketplace is viable.

PM Twin: Perfect — that's exactly the right instinct. Let's do a proper discovery
before committing to building anything.

  [Runs Phase 0 only: problem interview → market research → competitive analysis
   → feasibility → business model → Go/No-Go]

  → Saves everything to docs/toolkit/discovery.md
  → Presents Go/No-Go scorecard
  
  "Research complete. All findings saved. You can come back anytime
   and run /pm setup to start building if you decide to proceed."
```
