---
name: pitch
description: "[PM Twin] Generate pitch materials from Intelligence Hub data — investor, partner, enterprise, or internal audiences."
argument-hint: "[investor | partner | enterprise | internal]"
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Write, WebSearch
---

# Pitch — Pitch Material Generator

Generate pitch deck outlines and speaker notes from Intelligence Hub data.

## Prerequisites (Check Before Running)

Before generating any pitch materials, verify these exist:

1. **Check** `docs/toolkit/index.html` — if missing, tell the user:
   ```
   Intelligence Hub not found. Run /toolkit research first — I need
   market data, competitive analysis, and pricing to build pitch materials.
   ```
2. **Check** `docs/PRD.md` — if missing, tell the user:
   ```
   No PRD found. Run /pm setup to create one, or add your PRD at docs/PRD.md.
   ```

**Stop and show the message above if either prerequisite is missing.** Do not attempt to generate pitch materials without data.

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
- **Cite Intelligence Hub** — all market/competitive claims reference the Hub with confidence tags
- **Speaker notes are key** — the outline is for slides, the notes are for the presenter
- **Mark as confidential** — generated pitch materials may contain sensitive business intelligence. Add header: "CONFIDENTIAL — do not commit to public repos"
- **Write only to docs/toolkit/** — never modify application code
- **Check existing first** — read previous pitch docs before generating to avoid contradicting earlier versions
