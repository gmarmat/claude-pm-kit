---
name: metrics
description: "[PM Twin] Define, track, and review product KPIs — success metrics, funnels, health indicators."
argument-hint: "[define | review | report]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, Edit, Bash
---

# Metrics — KPI Definition & Tracking

Define what to measure, check current state, generate reports.

## Modes

| Argument | What It Does |
|----------|-------------|
| `define` | Walk through metric definition (name, query, target, owner) |
| `review` | Check current metrics against targets |
| `report` | Generate metrics report (markdown or HTML) |

## `/metrics define`

Interview the user to define key metrics:

1. **What matters most?** Revenue, users, engagement, retention, performance?
2. **For each metric:**
   - Name (e.g., "Monthly Active Users")
   - How to measure (e.g., "COUNT DISTINCT user_id FROM analytics_events WHERE created_at > now() - interval '30 days'")
   - Target (e.g., "100 MAU by month 3")
   - Current value (if known)
   - Owner (who is responsible)

Save to `docs/toolkit/metrics.yaml`:
```yaml
metrics:
  - name: Monthly Active Users
    query: "COUNT DISTINCT user_id FROM analytics_events WHERE ..."
    target: 100
    timeframe: "by 2026-07-01"
    current: null
    owner: "founder"
```

## `/metrics review`

**First:** Check if `docs/toolkit/metrics.yaml` exists. If not:
```
No metrics defined yet. Run /metrics define first to set up your KPIs.
```
**Stop if missing.** Do not proceed without metric definitions.

Read `metrics.yaml`, check each metric against target, present status:

```
Metric Health Check:

  Monthly Active Users:    ██████░░░░  62/100   (62%)  ⚠️ Behind pace
  Monthly Revenue:         ████████░░  $820/$1K (82%)  ✓ On track
  Churn Rate:              ██████████  2%/5%    (60%)  ✓ Better than target
```

## `/metrics report`

Generate a formatted report for stakeholders:
- Current values vs targets
- Trend (up/down/flat from last check)
- Commentary on each metric
- Save to `docs/toolkit/metrics-report-YYYY-MM-DD.md`

## Important Rules

- **Metrics must be measurable** — if it can't be queried, it's not a metric
- **Fewer is better** — 3-7 metrics, not 20. Focus on what drives decisions.
- **Connect to T2 monitoring** — if /toolkit features T2 is scaffolded, connect metrics to real data
