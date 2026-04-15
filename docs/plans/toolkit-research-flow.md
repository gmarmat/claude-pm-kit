# /toolkit research — Detailed Execution Flow

**Updated:** 2026-04-14

---

## Overview

This documents the exact step-by-step flow when a user runs `/toolkit research`. The skill generates a PM Intelligence Hub — a standalone HTML file with 7 tabs of researched, cited business intelligence.

---

## Step 1: Read Project Context

**Files read (in order):**
```
1. docs/PRD.md        → domain, users, value prop, features, phases, boundaries
2. docs/arch.md       → tech stack, data model, API routes, env vars, patterns
3. CLAUDE.md          → constraints, security model, naming conventions
4. docs/features/*.md → existing feature details (scan titles only)
```

**Extract and store:**
```
product_name:     [from PRD or arch.md header]
domain:           [e.g., "fitness tracking", "outage management", "job preparation"]
product_type:     [SaaS | marketplace | content | tool | hardware | service]
target_users:     [from PRD Target Users section]
value_prop:       [from PRD Executive Summary]
tech_stack:       [from arch.md Tech Stack table]
infra_services:   [from arch.md — hosting, DB, auth providers]
existing_features:[from arch.md Feature Index]
security_model:   [from CLAUDE.md or arch.md]
```

**If PRD is missing:** Stop. Tell user: "Run /toolkit research after you have a PRD. Use StartHere.md to create one."

**If arch.md is missing:** Warn but continue. Technical tab will be minimal.

---

## Step 2: Classify the Product

Based on extracted context, classify:

| Classification | Options | Affects |
|----------------|---------|---------|
| **Revenue model** | SaaS subscription, usage-based, freemium, marketplace commission, one-time purchase, ad-supported, open-source | Pricing tab |
| **Market type** | B2B, B2C, B2B2C, internal tool | Market + GTM tabs |
| **Stage** | Idea, MVP, launched, growth | All tabs (depth of analysis) |
| **Competitive density** | Blue ocean, emerging, crowded, commoditized | Competitive tab approach |

Present classification to user for confirmation:
```
I've analyzed your PRD. Here's how I'd classify your product:

  Product:  [name]
  Domain:   [domain]
  Type:     [SaaS / marketplace / etc.]
  Revenue:  [subscription / usage-based / etc.]
  Market:   [B2B / B2C / etc.]
  Stage:    [idea / MVP / launched]

Does this look right? Any corrections before I research?
```

---

## Step 3: Gather Cost Data

**If arch.md lists infrastructure:**
- Parse known services and estimate costs:

| Service | Estimated Monthly Cost |
|---------|----------------------|
| Supabase Free | $0 |
| Supabase Pro | $25-100 |
| Railway Hobby | $5 |
| Railway Pro | $20-200 |
| Vercel Free | $0 |
| Vercel Pro | $20 |
| OpenAI API | Usage-based (~$0.01-0.10/request) |
| Anthropic API | Usage-based (~$0.01-0.15/request) |
| Stripe | 2.9% + $0.30/transaction |
| Google Maps | $0.005-0.007/request |

**If costs unclear:** Ask user:
```
I need your infrastructure costs for the Pricing & Economics tab.
What do you spend (or expect to spend) monthly on:

1. Hosting/compute: $___
2. Database: $___
3. API services (AI, maps, search, etc.): $___
4. Auth/payment processing: $___
5. Other: $___

(Rough estimates are fine — I'll build sensitivity analysis around them)
```

---

## Step 4: Web Research

Run 5-8 web searches based on product classification. All searches include current year for freshness.

**Core searches (always run):**

| # | Query Template | Tab Fed |
|---|---------------|---------|
| 1 | `"[domain] market size revenue TAM 2025 2026"` | Market Analysis |
| 2 | `"[domain] [product_type] competitors alternatives"` | Competitive |
| 3 | `"[domain] pricing models [revenue_model] benchmarks"` | Pricing |
| 4 | `"[domain] industry trends growth forecast 2026"` | Market + GTM |
| 5 | `"[domain] customer acquisition channels [market_type]"` | Go-to-Market |

**Conditional searches (run if relevant):**

| # | Condition | Query Template | Tab Fed |
|---|-----------|---------------|---------|
| 6 | B2B or regulated | `"[domain] compliance regulations requirements"` | Technical |
| 7 | SaaS | `"[product_type] SaaS unit economics benchmarks gross margin"` | Pricing |
| 8 | Marketplace | `"[domain] marketplace take rate commission benchmarks"` | Pricing |

**For each search result:**
- Extract key data points
- Note source URL, domain, and retrieval date
- Tag confidence: Verified / Estimated / Calculated
- Prefer: .gov, .org, major publications (Forbes, TechCrunch, Gartner), industry reports
- Deprioritize: random blogs, SEO content farms, outdated (>2 years)

---

## Step 5: Deep Dive Key Pages (Optional)

If search results reference specific high-value pages (industry reports, competitor pricing pages, market research):

```
WebFetch(url, "Extract: market size, growth rate, key players, pricing data, 
              and any quantitative metrics. Note the publication date.")
```

Limit to 3-5 fetches to keep execution time reasonable.

---

## Step 6: Synthesize Research

Organize findings into tab structures:

### Dashboard Tab Data
```
- Product name + one-line description
- 4-6 KPI cards: TAM, target segment size, avg competitor price, estimated margin, key differentiator
- Strategic positioning statement (2-3 sentences)
- Quick navigation links to other tabs
```

### Market Analysis Tab Data
```
- TAM / SAM / SOM (with calculation methodology + sources)
- Market segments table (segment, size, growth, relevance)
- Industry trends (3-5 trends with implications)
- Growth forecast (if found)
- Confidence: tag each number
```

### Competitive Landscape Tab Data
```
- Competitors table: name, type (direct/indirect/substitute), pricing, key features, market position
- Positioning matrix: 2 axes relevant to this domain
- Differentiation analysis: what this product does differently
- Switching cost assessment
```

### Pricing & Economics Tab Data
```
- Competitor pricing benchmarks (table)
- Recommended tiers (3 tiers: starter/pro/enterprise or similar)
- Cost structure breakdown (from Step 3)
- Margin analysis per tier
- Sensitivity variables (what changes margins most)
- Calculator inputs: customer count, tier, add-ons
```

### Go-to-Market Tab Data
```
- Launch channels ranked by fit (organic, paid, partnerships, content, communities)
- Messaging framework (headline, subhead, 3 key benefits)
- Timeline: pre-launch, launch, post-launch phases
- Early adopter strategy
- Metrics to track (CAC, conversion rate, activation)
```

### Technical Tab Data
```
- Architecture summary (from arch.md)
- Tech stack table
- Security model highlights
- Scalability notes
- Integration points
- Infrastructure cost breakdown
```

### Sales Tools Tab Data
```
- Elevator pitch (30-second, 60-second versions)
- Calculator: tier × customers × months = revenue, minus costs = margin
- Objection handlers (5-8 common objections with responses)
- Key talking points (3-5)
- Case study template (fill in after first customer)
```

---

## Step 7: User Review Gate

**Present research summary before generating HTML:**

```
Here's what I found. Review before I generate the Intelligence Hub:

MARKET
  TAM: $X.XB [Verified — Source: Gartner 2025]
  Growth: X% CAGR [Estimated — Source: Forbes]
  Key segments: [list]

COMPETITORS (found X)
  [Name 1] — [pricing] — [key differentiator]
  [Name 2] — [pricing] — [key differentiator]
  [Name 3] — [pricing] — [key differentiator]

PRICING RECOMMENDATION
  Starter: $XX/mo (based on competitor avg $XX and your costs of $XX/mo)
  Pro: $XX/mo
  Enterprise: Custom

GO-TO-MARKET
  Primary channels: [top 3]
  Estimated CAC: $XX [Estimated]

Anything to correct or add before I generate?
```

User can:
- Confirm → proceed to HTML generation
- Correct → update data, re-present
- Add context → incorporate, re-present
- Add competitors → skill searches for them specifically

---

## Step 8: Generate HTML

Generate self-contained HTML file with:

**Structure:**
```html
<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Product Name] — PM Intelligence Hub</title>
  <style>
    /* Minimal CSS — tabs, cards, tables, calculator, print styles */
    /* Uses CSS custom properties for easy theming */
    /* Responsive grid for cards */
    /* Collapsible sections via <details> */
    /* Print: hide nav, expand all sections */
  </style>
</head>
<body>
  <header>
    <h1>[Product Name]</h1>
    <p>PM Intelligence Hub • Generated [date] • v1.0</p>
    <button onclick="toggleTheme()">🌓</button>
    <button onclick="window.print()">Print</button>
  </header>

  <nav id="tabs">
    <button data-tab="dashboard" class="active">Dashboard</button>
    <button data-tab="market">Market</button>
    <button data-tab="competitive">Competitive</button>
    <button data-tab="pricing">Pricing</button>
    <button data-tab="gtm">Go-to-Market</button>
    <button data-tab="technical">Technical</button>
    <button data-tab="sales">Sales Tools</button>
  </nav>

  <main>
    <section id="dashboard">...</section>
    <section id="market">...</section>
    <section id="competitive">...</section>
    <section id="pricing">
      <!-- Interactive calculator here -->
    </section>
    <section id="gtm">...</section>
    <section id="technical">...</section>
    <section id="sales">
      <!-- Deal calculator here -->
    </section>
  </main>

  <footer>
    Generated by /toolkit research • [source count] sources cited
    <br>Data as of [date] — re-run /toolkit research to refresh
  </footer>

  <script>
    // Tab navigation with URL state
    // Theme toggle (light/dark)
    // Pricing calculator
    // Deal calculator
    // Copy-to-clipboard for exec summary
    // Collapsible source sections
    // Utility: formatCurrency(), formatNumber(), formatPercent()
  </script>
</body>
</html>
```

**Key patterns:**
- No external CSS/JS dependencies except Chart.js (embedded or CDN)
- All data is hardcoded in the HTML (no API calls at runtime)
- URL state sync: `?tab=pricing` deep-links to specific tab
- Print media query: hides nav, expands all sections, single-column layout
- Dark mode: CSS custom properties swap on `data-theme` attribute
- Confidence tags rendered as colored badges: green (Verified), yellow (Estimated), blue (Calculated), gray (User-Provided)

---

## Step 9: Save Output

```
docs/toolkit/index.html      ← The Intelligence Hub
docs/toolkit/sources.md       ← All sources with URLs, dates, confidence
docs/toolkit/research-log.md  ← Raw research notes (what was searched, what was found)
```

**Update arch.md:** Add toolkit to feature index if not already there.

**Tell user:**
```
Intelligence Hub generated: docs/toolkit/index.html

Open in browser:  open docs/toolkit/index.html  (Mac)
                  start docs/toolkit/index.html  (Windows)
                  xdg-open docs/toolkit/index.html  (Linux)

[X] sources cited across 7 tabs
[X] data points tagged with confidence levels

To refresh data, run /toolkit research again.
To add product infrastructure, run /toolkit features.
```

---

## Error Handling

| Scenario | Response |
|----------|----------|
| No PRD found | Stop. Direct user to create one via StartHere.md |
| Web search returns no results for a query | Skip that data point, note gap in output, suggest user provide data manually |
| Web search returns outdated data only | Use it but tag as `[Dated — YYYY]` with warning |
| User provides no cost data | Use industry benchmarks from web research, tag as `[Estimated]` |
| Product is too niche for market data | Note limitation, focus on adjacent market data, suggest user conduct primary research |
| HTML generation fails (too large) | Split into multiple files with shared nav |

---

## Quality Checklist

Before saving HTML, verify:

- [ ] All 7 tabs have content (even if minimal)
- [ ] Every data point has a confidence tag
- [ ] Every sourced claim has a citation in the collapsible sources section
- [ ] Calculator works (test with sample inputs)
- [ ] Dark mode toggle works
- [ ] Print layout is clean (no broken tables)
- [ ] No personal data, API keys, or secrets in output
- [ ] Product name and domain are correct throughout
- [ ] Sources.md is complete and matches inline citations
