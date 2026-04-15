# Intelligence Hub HTML Specification

**Updated:** 2026-04-14

---

## Design Principles

1. **Self-contained** — Single HTML file, opens in any browser, works offline after generation
2. **No framework** — Vanilla HTML + CSS + JS. Chart.js is the only library (embedded).
3. **Themeable** — CSS custom properties for light/dark mode
4. **Print-ready** — Media queries for clean PDF export
5. **Accessible** — Semantic HTML, keyboard navigation, ARIA labels on interactive elements
6. **Generic** — No company branding, no hardcoded colors. Neutral professional palette.

---

## CSS Architecture

### Custom Properties (Root)

```css
:root {
  /* Neutral palette — no brand colors */
  --hub-bg: #ffffff;
  --hub-bg-secondary: #f8f9fa;
  --hub-bg-tertiary: #f0f1f3;
  --hub-text: #1a1a2e;
  --hub-text-secondary: #6b7280;
  --hub-text-muted: #9ca3af;
  --hub-border: #e5e7eb;
  --hub-accent: #2563eb;
  --hub-accent-light: #dbeafe;
  --hub-success: #059669;
  --hub-success-light: #d1fae5;
  --hub-warning: #d97706;
  --hub-warning-light: #fef3c7;
  --hub-danger: #dc2626;
  --hub-danger-light: #fee2e2;
  --hub-info: #0891b2;
  --hub-info-light: #cffafe;

  /* Spacing */
  --hub-space-xs: 0.25rem;
  --hub-space-sm: 0.5rem;
  --hub-space-md: 1rem;
  --hub-space-lg: 1.5rem;
  --hub-space-xl: 2rem;

  /* Typography */
  --hub-font: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --hub-font-mono: 'SF Mono', 'Fira Code', 'Consolas', monospace;
  --hub-radius: 8px;
  --hub-shadow: 0 1px 3px rgba(0,0,0,0.1);
  --hub-shadow-lg: 0 4px 12px rgba(0,0,0,0.1);
}

[data-theme="dark"] {
  --hub-bg: #0f172a;
  --hub-bg-secondary: #1e293b;
  --hub-bg-tertiary: #334155;
  --hub-text: #f1f5f9;
  --hub-text-secondary: #94a3b8;
  --hub-text-muted: #64748b;
  --hub-border: #334155;
  --hub-accent: #3b82f6;
  --hub-accent-light: #1e3a5f;
  --hub-success: #10b981;
  --hub-success-light: #064e3b;
  --hub-warning: #f59e0b;
  --hub-warning-light: #78350f;
  --hub-danger: #ef4444;
  --hub-danger-light: #7f1d1d;
  --hub-info: #22d3ee;
  --hub-info-light: #164e63;
  --hub-shadow: 0 1px 3px rgba(0,0,0,0.3);
  --hub-shadow-lg: 0 4px 12px rgba(0,0,0,0.3);
}
```

---

## Component Patterns

### KPI Card
```html
<div class="hub-kpi-card">
  <div class="hub-kpi-label">Total Addressable Market</div>
  <div class="hub-kpi-value">$4.2B</div>
  <div class="hub-kpi-delta hub-kpi-delta--up">+12% YoY</div>
  <div class="hub-kpi-source">
    <span class="hub-confidence hub-confidence--verified">Verified</span>
  </div>
</div>
```

### Confidence Badge
```html
<span class="hub-confidence hub-confidence--verified">Verified</span>
<span class="hub-confidence hub-confidence--estimated">Estimated</span>
<span class="hub-confidence hub-confidence--calculated">Calculated</span>
<span class="hub-confidence hub-confidence--user">User-Provided</span>
```

```css
.hub-confidence {
  font-size: 0.7rem;
  padding: 2px 6px;
  border-radius: 4px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.hub-confidence--verified  { background: var(--hub-success-light); color: var(--hub-success); }
.hub-confidence--estimated { background: var(--hub-warning-light); color: var(--hub-warning); }
.hub-confidence--calculated { background: var(--hub-accent-light); color: var(--hub-accent); }
.hub-confidence--user      { background: var(--hub-bg-tertiary); color: var(--hub-text-secondary); }
```

### Data Table
```html
<table class="hub-table">
  <thead>
    <tr><th>Competitor</th><th>Pricing</th><th>Key Feature</th><th>Market Position</th></tr>
  </thead>
  <tbody>
    <tr><td>CompA</td><td>$29/mo</td><td>AI-powered</td><td>Market leader</td></tr>
  </tbody>
</table>
```

### Collapsible Source Section
```html
<details class="hub-sources">
  <summary>Sources & References (X citations)</summary>
  <ul>
    <li>
      <a href="URL" target="_blank" rel="noopener">Source Title</a>
      — Retrieved 2026-04-14
      <span class="hub-confidence hub-confidence--verified">Verified</span>
    </li>
  </ul>
</details>
```

### Interactive Calculator
```html
<div class="hub-calculator">
  <h3>Pricing Calculator</h3>
  <div class="hub-calc-inputs">
    <label>
      Customers
      <input type="range" id="calc-customers" min="100" max="100000" value="1000" step="100">
      <output id="calc-customers-val">1,000</output>
    </label>
    <label>
      Tier
      <select id="calc-tier">
        <option value="starter">Starter</option>
        <option value="pro">Pro</option>
        <option value="enterprise">Enterprise</option>
      </select>
    </label>
  </div>
  <div class="hub-calc-results">
    <div class="hub-kpi-card">
      <div class="hub-kpi-label">Monthly Revenue</div>
      <div class="hub-kpi-value" id="calc-revenue">$0</div>
    </div>
    <div class="hub-kpi-card">
      <div class="hub-kpi-label">Monthly Cost</div>
      <div class="hub-kpi-value" id="calc-cost">$0</div>
    </div>
    <div class="hub-kpi-card">
      <div class="hub-kpi-label">Gross Margin</div>
      <div class="hub-kpi-value" id="calc-margin">0%</div>
    </div>
  </div>
</div>
```

### Sensitivity Slider
```html
<div class="hub-sensitivity">
  <label>
    Infrastructure Cost (±30%)
    <input type="range" id="sens-infra" min="-30" max="30" value="0">
    <output id="sens-infra-val">0%</output>
  </label>
  <div class="hub-sensitivity-impact" id="sens-impact">
    Margin: 85% → <strong>85%</strong>
  </div>
</div>
```

### Tab Navigation
```html
<nav class="hub-tabs" role="tablist">
  <button role="tab" aria-selected="true" data-tab="dashboard">Dashboard</button>
  <button role="tab" aria-selected="false" data-tab="market">Market</button>
  <!-- ... -->
</nav>
```

```css
.hub-tabs {
  display: flex;
  gap: var(--hub-space-xs);
  border-bottom: 2px solid var(--hub-border);
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}
.hub-tabs button {
  padding: var(--hub-space-sm) var(--hub-space-md);
  border: none;
  background: none;
  color: var(--hub-text-secondary);
  cursor: pointer;
  white-space: nowrap;
  border-bottom: 2px solid transparent;
  margin-bottom: -2px;
  transition: color 0.2s, border-color 0.2s;
}
.hub-tabs button[aria-selected="true"] {
  color: var(--hub-accent);
  border-bottom-color: var(--hub-accent);
  font-weight: 600;
}
```

---

## JavaScript Architecture

```javascript
(function() {
  'use strict';

  // === Tab Navigation ===
  function initTabs() {
    const tabs = document.querySelectorAll('[role="tab"]');
    const panels = document.querySelectorAll('[role="tabpanel"]');

    // Read initial tab from URL
    const params = new URLSearchParams(window.location.search);
    const initialTab = params.get('tab') || 'dashboard';

    tabs.forEach(tab => {
      tab.addEventListener('click', () => switchTab(tab.dataset.tab));
      tab.addEventListener('keydown', handleTabKeyboard);
    });

    switchTab(initialTab);
  }

  function switchTab(tabId) {
    // Update buttons
    document.querySelectorAll('[role="tab"]').forEach(t => {
      t.setAttribute('aria-selected', t.dataset.tab === tabId);
    });
    // Update panels
    document.querySelectorAll('[role="tabpanel"]').forEach(p => {
      p.hidden = p.id !== tabId;
    });
    // Update URL
    const url = new URL(window.location);
    url.searchParams.set('tab', tabId);
    window.history.replaceState({}, '', url);
  }

  // === Theme Toggle ===
  function toggleTheme() {
    const html = document.documentElement;
    const current = html.getAttribute('data-theme');
    html.setAttribute('data-theme', current === 'dark' ? 'light' : 'dark');
    localStorage.setItem('hub-theme', html.getAttribute('data-theme'));
  }

  // === Utilities ===
  function formatCurrency(n) {
    return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD', maximumFractionDigits: 0 }).format(n);
  }
  function formatNumber(n) {
    return new Intl.NumberFormat('en-US').format(n);
  }
  function formatPercent(n) {
    return new Intl.NumberFormat('en-US', { style: 'percent', minimumFractionDigits: 1 }).format(n / 100);
  }

  // === Copy to Clipboard ===
  function copyExecSummary() {
    const summary = document.getElementById('exec-summary-text').innerText;
    navigator.clipboard.writeText(summary).then(() => {
      const btn = document.getElementById('copy-btn');
      btn.textContent = 'Copied!';
      setTimeout(() => btn.textContent = 'Copy Summary', 2000);
    });
  }

  // === Calculator ===
  // Pricing data injected by skill at generation time:
  // const PRICING = { starter: { monthly: X }, pro: { monthly: X }, enterprise: { monthly: X } };
  // const COSTS = { base: X, perCustomer: X, ... };

  function updateCalculator() {
    const customers = parseInt(document.getElementById('calc-customers').value);
    const tier = document.getElementById('calc-tier').value;
    document.getElementById('calc-customers-val').textContent = formatNumber(customers);

    const revenue = PRICING[tier].monthly;
    const cost = COSTS.base + (COSTS.perCustomer * customers);
    const margin = ((revenue - cost) / revenue) * 100;

    document.getElementById('calc-revenue').textContent = formatCurrency(revenue);
    document.getElementById('calc-cost').textContent = formatCurrency(cost);
    document.getElementById('calc-margin').textContent = formatPercent(margin);
    document.getElementById('calc-margin').className =
      'hub-kpi-value ' + (margin > 70 ? 'hub-text-success' : margin > 40 ? 'hub-text-warning' : 'hub-text-danger');
  }

  // === Init ===
  document.addEventListener('DOMContentLoaded', () => {
    initTabs();

    // Restore theme
    const saved = localStorage.getItem('hub-theme');
    if (saved) document.documentElement.setAttribute('data-theme', saved);

    // Bind calculators
    document.querySelectorAll('.hub-calculator input, .hub-calculator select')
      .forEach(el => el.addEventListener('input', updateCalculator));

    // Init charts if Chart.js loaded
    if (typeof Chart !== 'undefined') initCharts();
  });

  // Expose to global
  window.toggleTheme = toggleTheme;
  window.copyExecSummary = copyExecSummary;
})();
```

---

## Print Styles

```css
@media print {
  .hub-tabs, .hub-header-actions, footer { display: none; }
  [role="tabpanel"] { display: block !important; page-break-inside: avoid; }
  [role="tabpanel"]::before {
    content: attr(aria-label);
    display: block;
    font-size: 1.5rem;
    font-weight: 700;
    margin: 2rem 0 1rem;
    border-bottom: 2px solid #000;
    padding-bottom: 0.5rem;
  }
  .hub-sources { display: block; }
  .hub-sources[open] summary ~ * { display: block; }
  .hub-calculator input[type="range"] { display: none; }
  body { font-size: 11pt; color: #000; background: #fff; }
}
```

---

## Responsive Breakpoints

```css
/* Mobile: stack everything */
@media (max-width: 640px) {
  .hub-kpi-grid { grid-template-columns: 1fr; }
  .hub-tabs { flex-wrap: nowrap; font-size: 0.85rem; }
  .hub-table { font-size: 0.8rem; }
  .hub-calc-results { grid-template-columns: 1fr; }
}

/* Tablet: 2-col grids */
@media (min-width: 641px) and (max-width: 1024px) {
  .hub-kpi-grid { grid-template-columns: repeat(2, 1fr); }
  .hub-calc-results { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop: 3-4 col grids */
@media (min-width: 1025px) {
  .hub-kpi-grid { grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); }
  .hub-calc-results { grid-template-columns: repeat(3, 1fr); }
}
```

---

## Chart.js Integration

Embed Chart.js (~200KB minified) directly in the HTML to enable offline viewing:

```html
<script>
  // Chart.js v4.x minified source embedded here at generation time
  // Alternatively: <script src="https://cdn.jsdelivr.net/npm/chart.js@4"></script>
</script>
```

**Charts used:**
| Tab | Chart Type | Data |
|-----|-----------|------|
| Dashboard | Doughnut | Revenue split by tier |
| Market | Bar | Market segments by size |
| Pricing | Line | Margin at different customer counts |
| Sales Tools | Line | 3-year revenue projection (conservative/moderate/aggressive) |

---

## File Size Budget

| Component | Estimated Size |
|-----------|---------------|
| HTML structure | ~20KB |
| Embedded CSS | ~8KB |
| Embedded JS (app logic) | ~5KB |
| Chart.js (embedded) | ~200KB |
| Content (7 tabs) | ~30-50KB |
| **Total** | **~260-280KB** |

If Chart.js CDN is used instead: **~60-80KB** (but requires internet).

**Recommendation:** Embed Chart.js for offline capability. 280KB is small for a full dashboard.

---

## Accessibility Checklist

- [ ] All interactive elements have `role` attributes
- [ ] Tabs use `role="tab"`, `role="tablist"`, `role="tabpanel"`
- [ ] Tab panels have `aria-labelledby` pointing to their tab button
- [ ] Calculator inputs have associated `<label>` elements
- [ ] Color is not the only indicator (confidence badges have text + color)
- [ ] Focus styles are visible (outline on all interactive elements)
- [ ] Print version includes all content (no hidden sections)
- [ ] `lang="en"` on `<html>` element
- [ ] Tables have `<thead>` and `<th>` with `scope` attributes
