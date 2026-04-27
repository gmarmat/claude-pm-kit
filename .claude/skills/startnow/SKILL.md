---
name: startnow
description: "[PM Twin] Load pm-kit context — reads PRD, arch, skill catalog, sibling-kit availability, and any new upstream commits since your last session."
argument-hint:
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Bash
---

# StartNow — Session Context Loader (PM Twin)

You are a context-building agent for pm-kit (PM Twin). When invoked at the start of a session, you systematically read pm-kit's key documents so you have full working knowledge before any work begins on the kit itself.

## Goal

Read and internalize pm-kit's architecture, rules, skill catalog, and the availability of sibling kits so you can work effectively on improving the kit or guiding builders through the lifecycle.

## Execution Steps

### Step 1: Identify the Project

1. Note the current working directory (this is the pm-kit project root).
2. Run `git remote -v` to identify the repository.
3. Run `git log --oneline -5` to see recent activity.
4. Run `git branch --show-current` to know the active branch.

### Step 1b: Check for Upstream Activity (Teammate / Cross-Session Awareness)

Skip silently if any sub-step fails (no remote, no upstream tracking, offline, etc.) — the skill must never error out because of network or remote state.

1. **If `git remote -v` showed any remote**, run `git fetch --quiet` to update remote refs. Ignore failures.
2. Run `git log --oneline HEAD..@{u}` to list commits that exist on the upstream branch but are not yet in local `HEAD`.
3. If step 2 returned any commits, run `git log --name-only HEAD..@{u}` to capture which files changed. Pay particular attention to:
   - `docs/arch.md`
   - `docs/PRD.md`
   - `CLAUDE.md`
   - `.claude/skills/*/SKILL.md` (especially `/pm` and `/verify` — the orchestrator and the gate)
4. Note authors via `git log --pretty=format:'%h %an %s' HEAD..@{u}`.

If no remote, no upstream tracking, or no new upstream commits, surface "no new upstream activity" in the summary.

### Step 2: Read Architecture and Rules

Read these in order:

1. `docs/arch.md` — architecture overview, version, skill catalog, key patterns
2. `docs/PRD.md` — product requirements, lifecycle phases, success criteria
3. `CLAUDE.md` — project rules, brand model (pforge / pmtwin / pm-kit), content boundaries

### Step 3: Inventory the Skill Catalog

Run `ls .claude/skills/` and read each present `SKILL.md` frontmatter (just the description). Pm-kit's core skills include `/pm` (orchestrator), `/verify` (sprint-boundary gate), `/metrics`, `/pitch`, `/roadmap`, `/userstudy`, `/stakeholder-update`, `/toolkit`. Note any new or in-progress skills — they may be active development.

### Step 4: Check for Sibling Kits

pm-kit orchestrates other kits via `/pm` Step 2 (auto-fetch protocol). Detect which sibling kits are available locally so you know what `/pm setup` can use without re-fetching:

| Path checked | Kit | Role |
|---|---|---|
| `../kit/` or `../claude-project-kit/` | project-kit | Scaffolding + core workflow skills |
| `../claude-workspace-kit/` | workspace-kit | Multi-project workspace |
| `../claude-project-rehab/` | rehab | Health checks for existing projects |
| `~/.claude/kits/` | (global cache) | Anything fetched via auto-fetch |

Note which are present and which are missing. `/pm setup` would offer to auto-clone the public ones.

### Step 5: Summarize Context

```
Project: pm-kit (PM Twin)
Branch:  [current branch]
Stack:   Claude Code skills (markdown + YAML)
Recent:  [last 3-5 commits, one line each]
Upstream: [N new commits since your last session, by [authors]]
          [or "no new upstream activity" / "no remote configured"]

Docs:
  - arch.md (vX.Y)
  - PRD.md [present/missing]
  - CLAUDE.md (brand model + rules)

Skills (N total):
  Core:    /pm, /verify
  Support: /metrics, /pitch, /roadmap, /userstudy, /stakeholder-update, /toolkit
  Other:   [list anything else present, including WIP]

Sibling kits:
  | Kit | Status |
  |-----|--------|
  | project-kit | found at [path] / not found |
  | workspace-kit | found at [path] / not found |
  | rehab | found at [path] / not found |

[If upstream commits touched arch.md / PRD.md / CLAUDE.md / /pm / /verify:
  "Heads-up: pm-kit context shifted upstream. Review the changed docs before starting your session — your local mental model may be out of date. /pm and /verify are load-bearing; flag any changes to those skills loudly."]

What are we working on today?
```

## Important Notes

- This is a **read-only** skill — do NOT modify any files
- Keep the summary concise — the user wants to start working, not read a report
- The upstream-activity check (Step 1b) is read-only against the remote (`git fetch` only updates local refs, never modifies remote). Always run silently — if the network is down or the remote is unreachable, skip without surfacing an error
- pm-kit is the orchestrator of the pforge ecosystem — when working on pm-kit itself, the most load-bearing files are `/pm` and `/verify` skills plus `docs/arch.md`. Flag changes to those above any others
