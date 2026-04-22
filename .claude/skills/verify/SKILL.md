---
name: verify
description: "[PM Twin] Sprint-boundary verification gate — runs every feature in the sprint through qa-feature, runs the sprint's end-to-end journey flows, aggregates evidence, and gates the next sprint."
argument-hint: "[sprint N | current | all | status] [--strict]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, Edit, Bash, AskUserQuestion
---

# Verify — Sprint-Boundary Gate

The methodology rule: **no sprint crosses into the next without verified evidence.** This skill is the gate. It does not generate tests — it orchestrates `/qa-feature` per feature in the sprint's scope, then runs the sprint's journey flows end-to-end, then writes the evidence report that unblocks the next sprint.

## When to Run

- **Automatically** at the end of each sprint, called by the Phase 2 Build loop in `/pm`
- **Manually** when the user wants to close a sprint early: `/verify sprint 2`
- **Regression** before a phase transition: `/verify all`
- **Status check** any time: `/verify status`

## Modes

| Argument | What It Does |
|----------|-------------|
| `sprint [N]` | Verify sprint N — scope = features listed for that sprint in `docs/toolkit/sprint-plan.md` |
| `current` | Verify the sprint marked `in_progress` in sprint-plan.md |
| `all` | Re-run verification for every sprint — regression mode |
| `status` | Report which sprints are verified, pending, or failed — no test execution |
| *(none)* | Ask the user which sprint to verify |

## Flags

| Flag | Behavior |
|------|----------|
| `--strict` | Hard gate — exit non-zero if any feature or integration flow fails. Blocks user from proceeding. |
| *(default)* | Soft gate — surface failures loudly in the report, ask the user whether to proceed |

Default is soft. Flaky browser tests should not block momentum; they should surface. Users opt into strict mode when they want CI-like behavior.

## Prerequisites (check in order, halt on miss)

1. **`docs/toolkit/sprint-plan.md`** exists and lists the sprint being verified
2. **`docs/toolkit/journey-flows.md`** exists — source of integration tests
3. **`docs/arch.md`** feature index — tells us which features are `done` in the sprint's scope
4. **Playwright installed** — delegate to `/qa-feature` to install on miss
5. **App dev server reachable** — check the port from `package.json` dev script

If any prereq missing, tell the user what's missing and stop. Do not proceed.

## Execution Steps

### Step 1 — Load sprint scope

Read `docs/toolkit/sprint-plan.md` and extract for the target sprint:

- Feature list (e.g. `login`, `dashboard-home`, `invite-flow`)
- Journey flows covered (e.g. `Flow 1 — Onboarding`, `Flow 2 — Dashboard`)
- Acceptance criteria per feature (from PRD references)

If the sprint has any feature not yet marked `done` in `docs/arch.md` feature index, halt with:
*"Sprint N has [feature] still in-progress. Verify runs only on completed features. Mark it done in arch.md or redefine the sprint scope."*

### Step 2 — Per-feature QA loop

For each feature in sprint scope:

1. Check `docs/toolkit/qa/[feature].md` — is there a prior PASS within the current commit range?
   - If yes, skip (cached). Record as "cached-pass" in the report.
   - If no, or if feature files changed since last run, continue.
2. Invoke `/qa-feature [feature]` — let it do test generation + run + self-heal (3 attempts, as defined in that skill)
3. Collect the per-feature result: pass/fail, screenshots, assertion count

Do not run features in parallel — they share the dev server.

### Step 3 — Sprint-scoped integration run

After per-feature QA, run the sprint's journey flows **end to end**. This is different from per-feature tests because it stitches multiple features together the way a real user would.

For each journey flow listed in the sprint:

1. Generate (or reuse from a prior run) a Playwright test at `e2e/sprint-[N]/[flow-slug].spec.ts`
2. The test walks the flow in full, touching every feature in sprint scope
3. Screenshot waypoints: entry, each major decision point, exit — full-page captures to `e2e/screenshots/sprint-[N]/`
4. Assert on the flow's success condition (from journey-flows.md)

Integration tests do NOT self-heal. If they fail, the failure is meaningful — sprint scope is wrong or features don't compose. Report and halt this step.

### Step 4 — Aggregate evidence

Write `docs/toolkit/qa/sprint-[N]/report.md`:

```markdown
# Sprint [N] — Verification Report
**Generated:** YYYY-MM-DD HH:MM · **Commit:** abc123 · **Mode:** [soft | strict]

## Summary
- Features verified: X/Y
- Integration flows: A/B passed
- Overall: [PASS | FAIL | PARTIAL]

## Features

| Feature | Result | Assertions | Screenshots | Notes |
|---------|:------:|:----------:|-------------|-------|
| [name]  | PASS   | N          | [link]      | — |
| [name]  | FAIL   | N          | [link]      | [1-line reason] |

## Integration Flows

| Flow | Result | Waypoints | Screenshots | Notes |
|------|:------:|:---------:|-------------|-------|
| [Flow 1 — Onboarding] | PASS | 6/6 | [link] | — |

## Evidence Gallery
- Per-feature: `docs/toolkit/qa/[feature].md`
- Screenshots: `e2e/screenshots/sprint-[N]/`
- Test files: `e2e/sprint-[N]/`
```

Copy screenshots into `docs/toolkit/qa/sprint-[N]/screenshots/` so the evidence is self-contained under `docs/toolkit/`. Keep the original `e2e/screenshots/` tree untouched for the Playwright reporter.

### Step 4b — Update the master index (shareable one-link overview)

Write or update `docs/toolkit/qa/index.md` — a single rolling report that covers every sprint. This is the link the user shares with stakeholders, investors, or anyone asking "does the product work?"

```markdown
# QA Evidence — [Product Name]
**Updated:** YYYY-MM-DD HH:MM · **Latest commit:** abc123

## Sprint Status

| Sprint | Name | Status | Verified | Features | Flows | Report |
|:------:|------|:------:|----------|:--------:|:-----:|--------|
| 1 | Auth + Spine | verified | 2026-04-12 | 3/3 | 1/1 | [→ sprint 1](sprint-1/report.md) |
| 2 | Primary workflow | verified_with_warnings | 2026-04-16 | 3/4 | 2/2 | [→ sprint 2](sprint-2/report.md) |
| 3 | Secondary + admin | in_progress | — | 2/5 | — | — |
| 4 | Polish + export | planned | — | 0/3 | — | — |

## Overall Health
- **Sprints verified:** 2/4
- **Features verified:** 6/15
- **Integration flows passed:** 3/4
- **Open failures:** 1 (sprint 2: [feature] — see sprint-2 report)

## Recent Activity
- 2026-04-16 — Sprint 2 verified (partial, 1 warning)
- 2026-04-12 — Sprint 1 verified (clean)
```

This page is deliberately short and table-first so a non-technical reader can scan it in under a minute. Every sprint link points to the full per-sprint report.

### Step 5 — Update sprint plan status

In `docs/toolkit/sprint-plan.md`, update the sprint entry:

| Status before | Event | Status after |
|--------------|-------|-------------|
| `in_progress` | All features + flows PASS | `verified` |
| `in_progress` | Any feature or flow FAIL, soft mode | `verified_with_warnings` |
| `in_progress` | Any feature or flow FAIL, strict mode | `blocked` |

Append: verified-on date, commit SHA, report link.

### Step 6 — Gate decision and handoff

Present to the user:

```
Sprint [N] verification — [PASS | PARTIAL | FAIL]

Features:      [X/Y passed]
Integration:   [A/B passed]
Evidence:      docs/toolkit/qa/sprint-[N]/report.md
Screenshots:   docs/toolkit/qa/sprint-[N]/screenshots/

[If PASS]       Next: sprint [N+1] unlocked. Run /pm next to continue.
[If PARTIAL]    Proceed to sprint [N+1]? Failures are documented. Recommended: fix before continuing if [critical feature name] is in the failure list.
[If FAIL]       Blocked. Fix the failures above, then re-run /verify sprint [N].
```

For PARTIAL in soft mode, ASK the user explicitly before updating sprint-plan.md to allow the next sprint to start. Never auto-proceed past a failure.

### Step 7 — `all` mode only

If invoked with `all`, run Steps 1–6 for each sprint in order. Stop on the first sprint that fails in strict mode. In soft mode, continue and report a regression matrix at the end:

```
| Sprint | Previous | Current | Delta |
|--------|:--------:|:-------:|-------|
| 1      | PASS     | PASS    | — |
| 2      | PASS     | FAIL    | Regression in [feature] — [reason] |
| 3      | —        | PASS    | New |
```

### Step 8 — `status` mode only

Read sprint-plan.md and print:

```
Sprint 1 — verified    (2026-04-12, commit abc123)
Sprint 2 — verified    (2026-04-15, commit def456)
Sprint 3 — in_progress (3/5 features done)
Sprint 4 — planned
```

No test execution. Under 10 lines.

## What NEVER Happens

- Never run against production data or real credentials — integration tests use `e2e/fixtures/seed.ts` only
- Never auto-advance the sprint plan past a failure — user must approve in soft mode
- Never commit screenshot PNGs — keep them gitignored; the markdown report references them by path
- Never modify application source — only the test files under `e2e/`
- Never bypass a failing integration test by skipping it — surface it
- Never run `playwright install` without user consent — delegate to `/qa-feature` which already has that gate

## What ALWAYS Happens

- Always copy evidence into `docs/toolkit/qa/sprint-[N]/` so the report is self-contained
- Always record the commit SHA at verification time — the report must be reproducible
- Always tag each per-feature result as `fresh-pass`, `cached-pass`, `self-healed-pass`, or `fail` — the user needs to know the confidence level
- Always write the report even on failure — the failure log is part of the evidence

## Integration With Other Skills

| Skill | Relationship |
|-------|--------------|
| `/pm setup` Phase 2 Build | Calls `/verify sprint [N]` at each sprint boundary (see pm.SKILL.md Step 10) |
| `/qa-feature` | Delegate — verify invokes per-feature QA rather than re-implementing |
| `/pm status` | Reads sprint-plan.md status fields to report verification coverage |
| `/stakeholder-update` | Pulls sprint verification results as evidence in status reports |
| `/toolkit hero` | Can reuse verified screenshots as hero imagery (ask the user first) |

## Design Notes

- **Scope by sprint, not by phase.** A phase boundary verification would re-test everything — expensive and slow. Sprint scope keeps runs fast and evidence focused.
- **Soft gate default.** Hard gates + flaky e2e = user learns to bypass. Soft surfacing keeps discipline without friction.
- **Journey flows are the test spec.** No LLM-generated tests at integration level. The flows the user confirmed in Step 9 of `/pm` are the acceptance criteria.
- **Evidence lives in docs/toolkit/.** That directory is already the PM artifact home — reports, screenshots, and status all belong there.
