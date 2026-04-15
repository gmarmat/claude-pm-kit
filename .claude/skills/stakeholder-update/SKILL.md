---
name: stakeholder-update
description: "[PM Twin] Generate product status update from recent activity — git history, feature progress, metrics."
argument-hint: "[weekly | monthly | custom]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, Bash
---

# Stakeholder Update — Status Report Generator

Generate a structured product status update from real project data.

## Data Sources

| Source | What It Provides |
|--------|-----------------|
| `git log` | Recent commits, features shipped, contributors |
| `docs/arch.md` | Feature index with status (planned/in-progress/done) |
| `docs/toolkit/roadmap.md` | Sprint progress, upcoming work |
| `docs/toolkit/metrics.yaml` | KPI current vs target |
| `docs/toolkit/index.html` | Intelligence Hub link (for context) |

## Execution Steps

1. **Determine timeframe** — weekly (7 days), monthly (30 days), or custom range
2. **Read git log** — `git log --oneline --since="[date]"` for commits in range
3. **Categorize commits** — features shipped, bugs fixed, docs updated, infrastructure
4. **Read arch.md** — feature index for overall progress
5. **Read metrics** — current values if metrics.yaml exists
6. **Generate report**

## Output Format

```markdown
# Product Update — [Product Name]
**Period:** [start] to [end] | **Generated:** [date]

## What Shipped
- Feature A: [1 sentence description]
- Feature B: [1 sentence description]
- Bug fix: [what was fixed]

## Key Metrics
| Metric | Current | Target | Trend |
|--------|---------|--------|-------|
| MAU    | 62      | 100    | ↑ +15 |

## In Progress
- Feature C (60% complete — expected [date])
- Feature D (started — expected [date])

## Up Next
- [Next sprint items from roadmap]

## Risks & Blockers
- [Any flagged issues]

## Links
- [Intelligence Hub](docs/toolkit/index.html)
- [Roadmap](docs/toolkit/roadmap.md)
```

Save to `docs/toolkit/updates/YYYY-MM-DD-[period].md`

## Output Options

- **Markdown** (default) — copy-paste to email, Slack, Notion
- **HTML** — formatted version for browser viewing
- **Clipboard** — copy to clipboard for immediate pasting

## Important Rules

- **Only report real data** — never fabricate metrics or progress
- **Git log is the source of truth** — features shipped = commits merged
- **Flag slippage honestly** — if something slipped, say so with context
- **Keep it short** — stakeholders scan, they don't read. Tables over paragraphs.
