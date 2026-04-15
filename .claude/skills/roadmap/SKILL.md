---
name: roadmap
description: "[PM Twin] Generate or update product roadmap from PRD phases and feature index."
argument-hint: "[quarter | month | sprint | update]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, Edit
---

# Roadmap — Product Roadmap Generator

Generate a visual product roadmap from PRD phases and arch.md feature index.

## Execution Steps

1. **Read PRD** — Extract phases, features, priorities (P0/P1/P2), timelines
2. **Read arch.md** — Feature index with current status (planned/in-progress/done)
3. **Read git log** — Recent commits to detect progress since last roadmap update
4. **Generate roadmap** — Organize by the requested view (quarter/month/sprint)
5. **Save** — `docs/toolkit/roadmap.md` (markdown) or `docs/toolkit/roadmap.html` (visual)

## Output Format

### Markdown (default)
```
## Roadmap — [Product Name]

### Sprint 1 (Current)
- [x] Feature A — done
- [ ] Feature B — in progress (60%)
- [ ] Feature C — planned

### Sprint 2
- [ ] Feature D — P0
- [ ] Feature E — P1

### Backlog
- Feature F — P2
- Feature G — P2
```

### HTML (if requested)
Timeline visualization with:
- Horizontal time axis (weeks/months/quarters)
- Feature cards positioned by phase
- Color coding by status (done/in-progress/planned)
- Dependencies shown as connecting lines

## Update Mode

When run with `update`:
1. Read existing roadmap
2. Compare with current arch.md feature index
3. Mark completed items, adjust timeline
4. Flag features that slipped or changed scope
5. Present diff to user for confirmation

## Important Rules

- **Reflect reality** — roadmap matches PRD + arch.md, not wishful thinking
- **Flag slippage** — if features are behind, say so clearly
- **Keep it current** — suggest running after each sprint/milestone
