# HTML Adapter

Single-file HTML pages that look stunning. No build step, no framework.

## Structure

Every HTML page follows this order:
1. `@layer` declarations
2. CSS Reset
3. Design tokens (from TOKENS.md)
4. Layout primitives (from LAYOUT.md)
5. Component styles
6. Page-specific styles
7. HTML body
8. Minimal JS (if needed)

## CSS Reset (Required)

```css
@layer reset, tokens, layout, components, utilities;

@layer reset {
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { -webkit-text-size-adjust: none; text-size-adjust: none; }
  body { min-height: 100vh; line-height: 1.6; -webkit-font-smoothing: antialiased; }
  img, picture, video, canvas, svg { display: block; max-width: 100%; }
  input, button, textarea, select { font: inherit; }
  p, h1, h2, h3, h4, h5, h6 { overflow-wrap: break-word; }
  h1, h2, h3 { line-height: 1.2; text-wrap: balance; }
  p { text-wrap: pretty; }
  a { color: inherit; }
  table { border-collapse: collapse; width: 100%; }
}
```

## Complete Dashboard Template

Copy this entire file. It works immediately.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard</title>
<style>
@layer reset, tokens, layout, components, page;

@layer reset {
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body { min-height: 100vh; line-height: 1.6; -webkit-font-smoothing: antialiased; }
  img, svg { display: block; max-width: 100%; }
  input, button, textarea, select { font: inherit; }
  h1, h2, h3 { line-height: 1.2; text-wrap: balance; }
  p { text-wrap: pretty; }
  table { border-collapse: collapse; width: 100%; }
}

@layer tokens {
  :root {
    --font-sans: system-ui, -apple-system, sans-serif;
    --font-mono: ui-monospace, 'Cascadia Code', 'Source Code Pro', Menlo, Consolas, monospace;

    --space-2xs: 4px;  --space-xs: 8px;   --space-sm: 12px;
    --space-md: 16px;  --space-lg: 24px;  --space-xl: 32px;
    --space-2xl: 48px; --space-3xl: 64px;

    --radius-sm: 4px;  --radius-md: 8px;  --radius-lg: 12px;
    --radius-xl: 16px; --radius-full: 9999px;

    --ease-out: cubic-bezier(0.4, 0, 0.2, 1);

    /* Arctic palette (light) */
    --bg: oklch(0.975 0.003 240);
    --surface: oklch(1.0 0 0);
    --surface-raised: oklch(1.0 0 0);
    --border: oklch(0.91 0.005 240);
    --border-subtle: oklch(0.94 0.003 240);
    --text: oklch(0.15 0.01 260);
    --text-muted: oklch(0.50 0.01 260);
    --primary: oklch(0.55 0.22 260);
    --primary-hover: oklch(0.50 0.24 260);
    --accent: oklch(0.68 0.16 175);
    --success: oklch(0.55 0.18 155);
    --success-tint: oklch(0.95 0.03 155);
    --warning: oklch(0.65 0.16 80);
    --warning-tint: oklch(0.96 0.03 80);
    --error: oklch(0.58 0.22 25);
    --error-tint: oklch(0.96 0.03 25);
    --info: oklch(0.58 0.18 250);
    --info-tint: oklch(0.96 0.02 250);

    --shadow-sm: 0 1px 2px rgba(0,0,0,0.06), 0 1px 3px rgba(0,0,0,0.04);
    --shadow-md: 0 1px 2px rgba(0,0,0,0.06), 0 2px 4px rgba(0,0,0,0.04), 0 4px 8px rgba(0,0,0,0.03);
    --shadow-lg: 0 2px 4px rgba(0,0,0,0.06), 0 4px 8px rgba(0,0,0,0.05), 0 8px 16px rgba(0,0,0,0.04), 0 16px 32px rgba(0,0,0,0.03);
  }

  @media (prefers-color-scheme: dark) {
    :root {
      --bg: oklch(0.16 0.01 260);
      --surface: oklch(0.20 0.01 260);
      --surface-raised: oklch(0.24 0.01 260);
      --border: oklch(0.30 0.01 260);
      --border-subtle: oklch(0.25 0.01 260);
      --text: oklch(0.93 0.005 260);
      --text-muted: oklch(0.65 0.01 260);
      --primary: oklch(0.70 0.18 250);
      --primary-hover: oklch(0.65 0.20 250);
      --accent: oklch(0.75 0.15 160);
      --success: oklch(0.72 0.18 155);
      --success-tint: oklch(0.25 0.04 155);
      --warning: oklch(0.78 0.16 80);
      --warning-tint: oklch(0.28 0.04 80);
      --error: oklch(0.65 0.22 25);
      --error-tint: oklch(0.25 0.05 25);
      --info: oklch(0.70 0.15 250);
      --info-tint: oklch(0.25 0.04 250);
      --shadow-sm: 0 1px 2px rgba(0,0,0,0.2), 0 1px 3px rgba(0,0,0,0.15);
      --shadow-md: 0 1px 2px rgba(0,0,0,0.2), 0 2px 4px rgba(0,0,0,0.15), 0 4px 8px rgba(0,0,0,0.1);
      --shadow-lg: 0 2px 4px rgba(0,0,0,0.25), 0 4px 8px rgba(0,0,0,0.2), 0 8px 16px rgba(0,0,0,0.15), 0 16px 32px rgba(0,0,0,0.1);
    }
  }
}

@layer layout {
  .stack { display: flex; flex-direction: column; }
  .stack > * + * { margin-block-start: var(--stack-space, var(--space-md)); }
  .cluster { display: flex; flex-wrap: wrap; gap: var(--cluster-space, var(--space-sm)); align-items: center; }
  .center { max-inline-size: var(--center-width, 65ch); margin-inline: auto; padding-inline: var(--space-lg); }
  .auto-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(var(--grid-min, 250px), 100%), 1fr));
    gap: var(--space-lg);
  }
  .switcher { display: flex; flex-wrap: wrap; gap: var(--space-lg); }
  .switcher > * { flex-grow: 1; flex-basis: calc((var(--switcher-threshold, 400px) - 100%) * 999); }
  .sidebar-layout { display: flex; flex-wrap: wrap; gap: var(--space-xl); }
  .sidebar-layout > :first-child { flex-basis: 250px; flex-grow: 1; }
  .sidebar-layout > :last-child { flex-basis: 0; flex-grow: 999; min-inline-size: 60%; }
}

@layer components {
  body {
    font-family: var(--font-sans);
    background: var(--bg);
    color: var(--text);
  }

  /* Card */
  .card {
    background: var(--surface);
    border-radius: var(--radius-lg);
    padding: var(--space-lg);
    box-shadow: var(--shadow-md);
    transition: box-shadow 0.2s var(--ease-out), transform 0.2s var(--ease-out);
  }
  .card:hover {
    box-shadow: var(--shadow-lg);
    transform: translateY(-2px);
  }

  /* KPI Card */
  .kpi { text-align: center; padding: var(--space-xl) var(--space-lg); }
  .kpi-label {
    display: block;
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-muted);
    margin-block-end: var(--space-xs);
  }
  .kpi-value {
    display: block;
    font-size: clamp(1.75rem, 1.2rem + 1.5vw, 2.5rem);
    font-weight: 700;
    letter-spacing: -0.02em;
    font-variant-numeric: tabular-nums;
  }
  .kpi-change {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    font-size: 0.85rem;
    font-weight: 600;
    margin-block-start: var(--space-xs);
    padding: 2px 8px;
    border-radius: var(--radius-full);
  }
  .kpi-change.up { background: var(--success-tint); color: var(--success); }
  .kpi-change.down { background: var(--error-tint); color: var(--error); }

  /* Badges / Tags */
  .badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 2px 10px;
    border-radius: var(--radius-full);
    font-size: 0.8rem;
    font-weight: 600;
  }
  .badge-success { background: var(--success-tint); color: var(--success); }
  .badge-warning { background: var(--warning-tint); color: var(--warning); }
  .badge-error   { background: var(--error-tint); color: var(--error); }
  .badge-info    { background: var(--info-tint); color: var(--info); }

  /* Status dot */
  .status-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    display: inline-block;
  }
  .status-dot.active { background: var(--success); box-shadow: 0 0 0 3px var(--success-tint); }
  .status-dot.warning { background: var(--warning); box-shadow: 0 0 0 3px var(--warning-tint); }
  .status-dot.error { background: var(--error); box-shadow: 0 0 0 3px var(--error-tint); }

  /* Buttons */
  .btn {
    display: inline-flex;
    align-items: center;
    gap: var(--space-xs);
    padding: var(--space-xs) var(--space-md);
    border: none;
    border-radius: var(--radius-md);
    font-weight: 600;
    font-size: 0.875rem;
    cursor: pointer;
    transition: background 0.15s var(--ease-out), transform 0.1s var(--ease-out);
  }
  .btn:active { transform: scale(0.97); }
  .btn-primary { background: var(--primary); color: white; }
  .btn-primary:hover { background: var(--primary-hover); }
  .btn-ghost {
    background: transparent;
    color: var(--text-muted);
    border: 1px solid var(--border);
  }
  .btn-ghost:hover { background: var(--surface-raised); color: var(--text); }

  /* Table */
  .table-wrap { overflow-x: auto; border-radius: var(--radius-lg); border: 1px solid var(--border); }
  table th {
    text-align: left;
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-muted);
    padding: var(--space-sm) var(--space-md);
    background: var(--surface);
    border-bottom: 1px solid var(--border);
  }
  table td {
    padding: var(--space-sm) var(--space-md);
    border-bottom: 1px solid var(--border-subtle);
    font-size: 0.9rem;
  }
  table tr:last-child td { border-bottom: none; }
  table tr:hover td { background: color-mix(in srgb, var(--primary) 3%, transparent); }

  /* Section headers */
  .section-title {
    font-size: clamp(1.125rem, 0.9rem + 0.6vw, 1.5rem);
    font-weight: 700;
    letter-spacing: -0.02em;
  }
  .section-subtitle {
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-muted);
  }

  /* Sidebar nav */
  .nav-item {
    display: flex;
    align-items: center;
    gap: var(--space-xs);
    padding: var(--space-xs) var(--space-sm);
    border-radius: var(--radius-md);
    font-size: 0.9rem;
    color: var(--text-muted);
    text-decoration: none;
    transition: all 0.15s var(--ease-out);
  }
  .nav-item:hover { background: var(--surface-raised); color: var(--text); }
  .nav-item.active { background: color-mix(in srgb, var(--primary) 10%, transparent); color: var(--primary); font-weight: 600; }

  /* Focus */
  :focus-visible { outline: 2px solid var(--primary); outline-offset: 2px; }
  :focus:not(:focus-visible) { outline: none; }

  /* Links */
  a:not(.nav-item):not(.btn) {
    color: var(--primary);
    text-decoration: underline;
    text-underline-offset: 2px;
    text-decoration-color: color-mix(in srgb, var(--primary) 30%, transparent);
    transition: text-decoration-color 0.15s ease;
  }
  a:not(.nav-item):not(.btn):hover { text-decoration-color: var(--primary); }
}

@layer page {
  .page { padding: var(--space-xl); }
  .page-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-block-end: var(--space-2xl);
  }
  .page-title {
    font-size: clamp(1.75rem, 1.2rem + 1.5vw, 2.5rem);
    font-weight: 800;
    letter-spacing: -0.03em;
  }
  .page-description {
    color: var(--text-muted);
    margin-block-start: var(--space-2xs);
  }
}
</style>
</head>
<body>
  <div class="sidebar-layout" style="min-height: 100vh">
    <!-- Sidebar -->
    <nav class="stack" style="--stack-space: var(--space-2xs); padding: var(--space-lg); background: var(--surface); border-right: 1px solid var(--border-subtle);">
      <div style="font-weight: 800; font-size: 1.1rem; padding: var(--space-xs); margin-block-end: var(--space-md);">⚡ Acme</div>
      <a href="#" class="nav-item active">📊 Dashboard</a>
      <a href="#" class="nav-item">📋 Projects</a>
      <a href="#" class="nav-item">👥 Team</a>
      <a href="#" class="nav-item">⚙️ Settings</a>
    </nav>

    <!-- Main -->
    <main class="page stack" style="--stack-space: var(--space-2xl)">
      <!-- Header -->
      <div class="page-header">
        <div>
          <h1 class="page-title">Dashboard</h1>
          <p class="page-description">Overview of your project metrics</p>
        </div>
        <div class="cluster">
          <button class="btn btn-ghost">Export</button>
          <button class="btn btn-primary">+ New Project</button>
        </div>
      </div>

      <!-- KPI Cards -->
      <div class="switcher" style="--switcher-threshold: 600px">
        <div class="card kpi">
          <span class="kpi-label">Total Revenue</span>
          <span class="kpi-value">$48,290</span>
          <span class="kpi-change up">↑ 12.5%</span>
        </div>
        <div class="card kpi">
          <span class="kpi-label">Active Users</span>
          <span class="kpi-value">2,847</span>
          <span class="kpi-change up">↑ 8.1%</span>
        </div>
        <div class="card kpi">
          <span class="kpi-label">Conversion</span>
          <span class="kpi-value">3.24%</span>
          <span class="kpi-change down">↓ 0.4%</span>
        </div>
        <div class="card kpi">
          <span class="kpi-label">Avg Response</span>
          <span class="kpi-value">1.2s</span>
          <span class="kpi-change up">↑ 15%</span>
        </div>
      </div>

      <!-- Content Grid -->
      <div class="auto-grid" style="--grid-min: 350px">
        <!-- Recent Activity -->
        <div class="card stack" style="--stack-space: var(--space-md)">
          <div style="display:flex; justify-content:space-between; align-items:center">
            <h2 class="section-title">Recent Activity</h2>
            <a href="#" style="font-size:0.85rem">View all →</a>
          </div>
          <div class="table-wrap">
            <table>
              <thead><tr><th>Event</th><th>User</th><th>Status</th></tr></thead>
              <tbody>
                <tr><td>Deployment #847</td><td>Alice</td><td><span class="badge badge-success">✓ Live</span></td></tr>
                <tr><td>Build #846</td><td>Bob</td><td><span class="badge badge-warning">⏳ Pending</span></td></tr>
                <tr><td>PR Review #203</td><td>Carol</td><td><span class="badge badge-info">👁 Review</span></td></tr>
                <tr><td>Issue #189</td><td>Dave</td><td><span class="badge badge-error">✗ Failed</span></td></tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Team Status -->
        <div class="card stack" style="--stack-space: var(--space-md)">
          <h2 class="section-title">Team Status</h2>
          <div class="stack" style="--stack-space: var(--space-sm)">
            <div class="cluster" style="justify-content:space-between; padding: var(--space-xs) 0; border-bottom: 1px solid var(--border-subtle)">
              <div class="cluster"><span class="status-dot active"></span> Alice Chen</div>
              <span style="font-size:0.8rem; color:var(--text-muted)">Working on API</span>
            </div>
            <div class="cluster" style="justify-content:space-between; padding: var(--space-xs) 0; border-bottom: 1px solid var(--border-subtle)">
              <div class="cluster"><span class="status-dot active"></span> Bob Park</div>
              <span style="font-size:0.8rem; color:var(--text-muted)">Code review</span>
            </div>
            <div class="cluster" style="justify-content:space-between; padding: var(--space-xs) 0; border-bottom: 1px solid var(--border-subtle)">
              <div class="cluster"><span class="status-dot warning"></span> Carol Wu</div>
              <span style="font-size:0.8rem; color:var(--text-muted)">In meeting</span>
            </div>
            <div class="cluster" style="justify-content:space-between; padding: var(--space-xs) 0">
              <div class="cluster"><span class="status-dot error"></span> Dave Kim</div>
              <span style="font-size:0.8rem; color:var(--text-muted)">Offline</span>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</body>
</html>
```

## Quick Enhancements (Add to Any Template)

### Top Accent Bar
```css
body::before {
  content: '';
  display: block;
  height: 4px;
  background: linear-gradient(90deg, var(--primary), var(--accent));
  position: sticky;
  top: 0;
  z-index: 100;
}
```

### Subtle Background Texture
```css
body {
  background-image: radial-gradient(circle, var(--border-subtle) 1px, transparent 1px);
  background-size: 24px 24px;
}
```

### Scroll Progress Indicator
```css
.scroll-progress {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--primary);
  transform-origin: left;
  animation: grow linear;
  animation-timeline: scroll();
  z-index: 999;
}
@keyframes grow { from { transform: scaleX(0); } to { transform: scaleX(1); } }
```

### Reveal-on-Scroll Sections
```css
.reveal {
  animation: fade-up 0.6s cubic-bezier(0.4, 0, 0.2, 1) both;
  animation-timeline: view();
  animation-range: entry 0% entry 40%;
}
@keyframes fade-up { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
```

## Template Recipes

### Report / Document
Use: `Cover` + `Center` + `Stack` layout. Serif font. Generous margins.
```css
body { font-family: var(--font-serif); }
main { max-width: 65ch; margin-inline: auto; padding: var(--space-3xl) var(--space-lg); }
h1 { font-size: clamp(2rem, 1.5rem + 2vw, 3rem); margin-block-end: var(--space-lg); }
.meta { font-size: 0.85rem; color: var(--text-muted); border-block-start: 1px solid var(--border); padding-block-start: var(--space-md); }
```

### Landing Page
Use: `Cover` + `Switcher` + `Auto-Grid`. Bold hero with gradient background.
```css
.hero {
  min-height: 80vh;
  display: flex; flex-direction: column; justify-content: center; align-items: center;
  text-align: center;
  background: linear-gradient(135deg, oklch(0.97 0.01 80) 0%, oklch(0.98 0.005 240) 100%);
  padding: var(--space-4xl) var(--space-lg);
}
.hero h1 { font-size: clamp(2.5rem, 1.5rem + 4vw, 4.5rem); font-weight: 800; letter-spacing: -0.03em; }
.hero p { font-size: clamp(1rem, 0.8rem + 0.5vw, 1.25rem); color: var(--text-muted); max-width: 50ch; }
```

## Data Visualization

Add Chart.js via CDN for charts:
```html
<script src="https://cdn.jsdelivr.net/npm/chart.js@4"></script>
```

Style chart containers:
```css
.chart-container {
  position: relative;
  padding: var(--space-lg);
  background: var(--surface);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
}
```
