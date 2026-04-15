# PM Orchestration — Feature Doc

**Status:** Planned | **Skill:** `/pm`

## Overview

The orchestrator skill that ties everything together. Assesses project state, identifies gaps in the product lifecycle, and offers a structured plan to fill them. Can delegate to other Claude kits (project-kit, workspace-kit, rehab) when available.

## Three Modes

### `/pm setup`
Assess current state → classify → offer plan:
- **State A:** Fresh idea → guide through discovery, validation, scaffolding
- **State B:** Has PRD, no code → scaffold project, guide build
- **State C:** Has code, no docs → rehab, then add PM layer
- **State D:** Mature project → show status, recommend next action

### `/pm status`
Product maturity scorecard:
- Discovery (30%): PRD + research + Go/No-Go
- Planning (20%): arch.md + skills + roadmap + environment
- Development (20%): P0 feature completion %
- Productization (15%): Intelligence Hub + T1 + pre-launch checklist
- Launch (10%): deployed + domain + smoke test
- Growth (5%): metrics + updates + roadmap refresh

### `/pm next`
Single highest-impact recommendation based on maturity gaps.

## Kit Detection

PM Twin checks for other kits in order:
1. Sibling directories
2. Parent workspace
3. `~/.claude/kits/` global cache
4. Offers to fetch from GitHub (with user permission)

## Key Decisions

| Decision | Choice | Why |
|----------|--------|-----|
| Other kits required? | No — degrades gracefully | Independence is a core principle |
| Auto-fetch kits? | Ask first | User should know what's being installed |
| Persona enforcement | Via CLAUDE.md | PM Twin persona defined in project rules |
