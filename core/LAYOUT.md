# Layout — Composable Primitives

Inspired by Every Layout. Intrinsic, composable, no breakpoints needed.

## The Stack

Vertical spacing between elements. The most-used primitive.

```css
.stack { display: flex; flex-direction: column; }
.stack > * + * { margin-block-start: var(--stack-space, var(--space-md)); }
```

```html
<div class="stack" style="--stack-space: var(--space-lg)">
  <h2>Title</h2>
  <p>Paragraph one</p>
  <p>Paragraph two</p>
</div>
```

**Use for:** Any vertical list of content — page sections, form fields, card contents.

## The Cluster

Horizontal wrapping with consistent gap. Adapts to available space.

```css
.cluster {
  display: flex;
  flex-wrap: wrap;
  gap: var(--cluster-space, var(--space-sm));
  align-items: center;
}
```

```html
<div class="cluster">
  <span class="tag">Design</span>
  <span class="tag">CSS</span>
  <span class="tag">Layout</span>
</div>
```

**Use for:** Tags, badges, button groups, metadata (author + date + reading time).

## The Sidebar

Content area + sidebar. Sidebar has fixed ideal width, content fills remaining space. Stacks vertically when too narrow.

```css
.sidebar-layout {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-xl);
}
.sidebar-layout > :first-child {
  flex-basis: 250px;
  flex-grow: 1;
}
.sidebar-layout > :last-child {
  flex-basis: 0;
  flex-grow: 999;
  min-inline-size: 60%;
}
```

```html
<div class="sidebar-layout">
  <nav>Sidebar navigation</nav>
  <main>Main content area</main>
</div>
```

**Use for:** Dashboard layouts, docs with sidebar nav, settings pages.

## The Switcher

Row layout that switches to column when container is too narrow. No media queries.

```css
.switcher {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-lg);
}
.switcher > * {
  flex-grow: 1;
  flex-basis: calc((var(--switcher-threshold, 400px) - 100%) * 999);
}
```

```html
<div class="switcher" style="--switcher-threshold: 500px">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
</div>
```

**Use for:** KPI cards, feature comparison, side-by-side content.

## The Center

Centered content with max-width. The simplest primitive.

```css
.center {
  max-inline-size: var(--center-width, 65ch);
  margin-inline: auto;
  padding-inline: var(--space-lg);
}
```

**Use for:** Article text, form containers, any reading-width content.

## The Cover

Full-viewport height with centered content + optional header/footer.

```css
.cover {
  display: flex;
  flex-direction: column;
  min-block-size: 100vh;
  padding: var(--space-lg);
}
.cover > * { margin-block: var(--space-md); }
.cover > :first-child:not(.cover-center) { margin-block-start: 0; }
.cover > :last-child:not(.cover-center)  { margin-block-end: 0; }
.cover > .cover-center { margin-block: auto; }
```

```html
<div class="cover">
  <header>Logo</header>
  <div class="cover-center">
    <h1>Hero Content</h1>
    <p>Vertically and horizontally centered.</p>
  </div>
  <footer>Footer info</footer>
</div>
```

**Use for:** Landing pages, hero sections, login screens, error pages.

## The Grid

Auto-responsive grid. No breakpoints — items wrap based on available space.

```css
.auto-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(var(--grid-min, 250px), 100%), 1fr));
  gap: var(--space-lg);
}
```

```html
<div class="auto-grid" style="--grid-min: 300px">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
  <div class="card">Card 4</div>
</div>
```

**Use for:** Card grids, image galleries, KPI dashboards, any repeating items.

## The Frame

Aspect-ratio container for media. Prevents layout shift.

```css
.frame {
  aspect-ratio: var(--frame-ratio, 16/9);
  overflow: hidden;
  border-radius: var(--radius-lg);
}
.frame > img, .frame > video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

**Use for:** Image containers, video embeds, avatar containers (with `--frame-ratio: 1`).

## The Reel

Horizontal scrolling strip. For content that overflows.

```css
.reel {
  display: flex;
  gap: var(--space-md);
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  scroll-padding: var(--space-md);
  -webkit-overflow-scrolling: touch;
}
.reel > * {
  flex-shrink: 0;
  scroll-snap-align: start;
}
.reel::-webkit-scrollbar { height: 6px; }
.reel::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
```

**Use for:** Horizontal card lists, image carousels, tab bars, timeline entries.

## Combining Primitives

The power is in composition:

```html
<!-- Dashboard = Sidebar + Grid + Stack -->
<div class="sidebar-layout">
  <nav class="stack">
    <a href="#">Dashboard</a>
    <a href="#">Settings</a>
  </nav>
  <main class="stack" style="--stack-space: var(--space-2xl)">
    <!-- KPI row -->
    <div class="switcher">
      <div class="card">KPI 1</div>
      <div class="card">KPI 2</div>
      <div class="card">KPI 3</div>
    </div>
    <!-- Content grid -->
    <div class="auto-grid">
      <div class="card">Chart</div>
      <div class="card">Table</div>
    </div>
  </main>
</div>
```
