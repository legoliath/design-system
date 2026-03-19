# HTML Adapter

Modern CSS for dashboards, web pages, and rich documents. Single-file HTML when possible (inline CSS, no build step).

## Modern CSS Features (2025+)

### Container Queries — Responsive Components
Components respond to their container, not the viewport:
```css
.card-container { container-type: inline-size; }
@container (min-width: 400px) {
  .card { flex-direction: row; }
}
```

### CSS Nesting — Clean Selectors
```css
.dashboard {
  display: grid;
  & .card {
    padding: var(--space-md);
    & h3 { margin-bottom: var(--space-sm); }
  }
}
```

### :has() — Parent Selectors
```css
.card:has(.status--error) { border-left: 4px solid var(--color-error); }
.form:has(:invalid) .submit { opacity: 0.5; }
```

### View Transitions
```css
@view-transition { navigation: auto; }
::view-transition-old(main) { animation: fade-out 0.2s; }
::view-transition-new(main) { animation: fade-in 0.2s; }
```

### Scroll-Driven Animations
```css
.progress-bar {
  animation: grow linear;
  animation-timeline: scroll();
}
```

## Dashboard Layout Pattern

```css
:root {
  --color-primary: #2563EB;
  --color-accent: #F59E0B;
  --color-success: #10B981;
  --color-warning: #F59E0B;
  --color-error: #EF4444;
  --color-bg: #F9FAFB;
  --color-surface: #FFFFFF;
  --color-text: #111827;
  --color-muted: #6B7280;
  --color-border: #E5E7EB;
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 48px;
  --radius: 8px;
  --shadow: 0 1px 3px rgba(0,0,0,0.1);
}

body {
  font-family: system-ui, -apple-system, sans-serif;
  background: var(--color-bg);
  color: var(--color-text);
  line-height: 1.5;
  margin: 0;
}

.dashboard {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: auto 1fr;
  min-height: 100vh;
}

.sidebar {
  background: var(--color-surface);
  border-right: 1px solid var(--color-border);
  padding: var(--space-lg);
}

.main { padding: var(--space-xl) var(--space-lg); }

.kpi-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--space-md);
}

.card {
  background: var(--color-surface);
  border-radius: var(--radius);
  padding: var(--space-lg);
  box-shadow: var(--shadow);
}
```

## KPI Card Component
```html
<div class="card kpi">
  <span class="kpi-label">Total Users</span>
  <span class="kpi-value">12,847</span>
  <span class="kpi-change positive">+12.3%</span>
</div>
```
```css
.kpi-label { font-size: 0.8rem; color: var(--color-muted); text-transform: uppercase; letter-spacing: 0.05em; }
.kpi-value { font-size: 2rem; font-weight: 700; display: block; }
.kpi-change { font-size: 0.85rem; font-weight: 600; }
.kpi-change.positive { color: var(--color-success); }
.kpi-change.negative { color: var(--color-error); }
```

## Charts (Lightweight)

### Chart.js (via CDN)
```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<canvas id="chart" width="400" height="200"></canvas>
<script>
new Chart(document.getElementById('chart'), {
  type: 'bar',
  data: { labels: ['Mon','Tue','Wed','Thu','Fri'],
          datasets: [{ label: 'Tasks', data: [12,19,3,5,8],
                       backgroundColor: '#2563EB' }] },
  options: { responsive: true, plugins: { legend: { display: false } } }
});
</script>
```

### Pure CSS Bar Chart (no JS)
```css
.bar-chart { display: flex; align-items: flex-end; gap: 4px; height: 150px; }
.bar { background: var(--color-primary); border-radius: 4px 4px 0 0; min-width: 30px; transition: height 0.3s; }
.bar:hover { background: var(--color-accent); }
```

## Dark Mode
```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #111827;
    --color-surface: #1F2937;
    --color-text: #F9FAFB;
    --color-muted: #9CA3AF;
    --color-border: #374151;
  }
}
```

## Responsive Patterns

### Stack on Mobile
```css
.dashboard {
  grid-template-columns: 1fr;
  @media (min-width: 768px) { grid-template-columns: 250px 1fr; }
}
```

### Responsive Table
```css
@media (max-width: 600px) {
  table, thead, tbody, th, td, tr { display: block; }
  td::before { content: attr(data-label); font-weight: 700; }
}
```

## Status Indicators
```css
.status { display: inline-flex; align-items: center; gap: 6px; font-size: 0.85rem; font-weight: 500; }
.status::before { content: ''; width: 8px; height: 8px; border-radius: 50%; }
.status--active::before { background: var(--color-success); }
.status--warning::before { background: var(--color-warning); }
.status--error::before { background: var(--color-error); }
```

## Single-File Template
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dashboard</title>
  <style>/* CSS vars + layout + components here */</style>
</head>
<body>
  <div class="dashboard">
    <nav class="sidebar"><!-- Nav items --></nav>
    <main class="main">
      <h1>Dashboard Title</h1>
      <div class="kpi-grid"><!-- KPI cards --></div>
      <section class="card"><!-- Content --></section>
    </main>
  </div>
</body>
</html>
```

Keep everything in one file for portability. Only split when the page exceeds ~500 lines.
