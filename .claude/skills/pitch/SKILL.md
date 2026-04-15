---
name: pitch
description: "[PM Twin] Generate pitch materials from Intelligence Hub data — investor, partner, enterprise, or internal audiences."
argument-hint: "[investor | partner | enterprise | internal]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, WebSearch
---

# Pitch — Pitch Material Generator

Generate pitch deck outlines and speaker notes from Intelligence Hub data.

## Prerequisites

- `docs/toolkit/index.html` must exist (run `/toolkit research` first)
- `docs/PRD.md` must exist

## Audience Templates

### `/pitch investor`
1. Problem (from PRD pain points)
2. Solution (from PRD value prop)
3. Market Size (from Intelligence Hub Market tab — TAM/SAM/SOM)
4. Competition (from Intelligence Hub Competitive tab)
5. Business Model (from Intelligence Hub Pricing tab)
6. Traction (from git history, feature completion, deployments)
7. Team (user provides)
8. The Ask (user provides)

### `/pitch partner`
1. Your Product (from PRD)
2. Integration Value (from Intelligence Hub Technical tab)
3. Mutual Benefit (synthesized)
4. Technical Fit (from arch.md)
5. Next Steps

### `/pitch enterprise`
1. Problem & ROI (from PRD + pricing data)
2. Security & Compliance (from CLAUDE.md + arch.md)
3. Integration (from Technical tab)
4. Support & SLA
5. Pricing (from Intelligence Hub)

### `/pitch internal`
1. Status Update (from git log + roadmap)
2. Metrics (from /metrics if available)
3. Roadmap (from /roadmap if available)
4. Resource Needs
5. Risks & Mitigations

## Output

- `docs/toolkit/pitch-[audience].md` — Slide-by-slide outline with speaker notes
- Each slide: title, 3-5 bullet points, speaker notes (what to say)
- Data points reference Intelligence Hub sources

## Important Rules

- **Never fabricate traction** — only reference real data (git history, actual metrics)
- **Cite Intelligence Hub** — all market/competitive claims reference the Hub
- **Speaker notes are key** — the outline is for slides, the notes are for the presenter
