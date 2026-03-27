# Modern CSS — Browser-Ready Features

Everything here works in all modern browsers (2024+). No polyfills needed.

## Fluid Typography with clamp()

Stop using breakpoints for font sizes. One line, perfectly fluid:

```css
/* Display heading: 2rem at 320px → 3.5rem at 1200px */
.display { font-size: clamp(2rem, 1rem + 3vw, 3.5rem); }

/* H1: scales from 1.75rem to 2.5rem */
h1 { font-size: clamp(1.75rem, 1.2rem + 1.5vw, 2.5rem); }

/* H2 */
h2 { font-size: clamp(1.375rem, 1rem + 1vw, 1.875rem); }

/* H3 */
h3 { font-size: clamp(1.125rem, 0.9rem + 0.6vw, 1.5rem); }

/* Body — stays readable */
body { font-size: clamp(0.95rem, 0.9rem + 0.2vw, 1.125rem); }

/* Small text */
.small { font-size: clamp(0.75rem, 0.7rem + 0.15vw, 0.875rem); }
```

## Container Queries

Components respond to their container, not the viewport:

```css
.card-wrapper { container-type: inline-size; }

.card { display: grid; gap: 16px; }

@container (min-width: 400px) {
  .card { grid-template-columns: 120px 1fr; }
}

@container (min-width: 600px) {
  .card { grid-template-columns: 180px 1fr auto; }
}
```

## :has() — The Parent Selector

Style parents based on their children:

```css
/* Card with error status gets red border */
.card:has(.status--error) { border-left: 3px solid var(--error); }

/* Form with invalid inputs dims submit */
.form:has(:invalid) .submit-btn { opacity: 0.5; pointer-events: none; }

/* Section with no content collapses */
.section:has(:empty) { display: none; }

/* Nav item with active link */
.nav-item:has(a[aria-current="page"]) { background: var(--surface-raised); }
```

## Native CSS Nesting

No preprocessor needed:

```css
.dashboard {
  display: grid;
  gap: var(--space-lg);

  & .header {
    display: flex;
    justify-content: space-between;
    align-items: center;

    & h1 { margin: 0; }
    & .actions { display: flex; gap: var(--space-sm); }
  }

  & .card {
    background: var(--surface);
    border-radius: 12px;
    padding: var(--space-lg);

    &:hover { box-shadow: var(--shadow-elevated); }
    & .card-title { font-weight: 600; }
  }
}
```

## color-mix() — Dynamic Tints

Create tinted variants without new variables:

```css
/* 10% tinted backgrounds */
.bg-primary-tint { background: color-mix(in srgb, var(--primary) 10%, white); }
.bg-error-tint   { background: color-mix(in srgb, var(--error) 8%, white); }

/* Hover darkening */
.btn:hover { background: color-mix(in srgb, var(--primary) 85%, black); }

/* Subtle borders from text color */
.divider { border-color: color-mix(in srgb, var(--text) 10%, transparent); }
```

## @layer — Cascade Control

```css
@layer reset, tokens, layout, components, utilities;

@layer reset {
  *, *::before, *::after { box-sizing: border-box; margin: 0; }
}

@layer tokens {
  :root { /* design tokens here */ }
}

@layer components {
  .card { /* component styles */ }
}

@layer utilities {
  .sr-only { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0,0,0,0); }
}
```

## text-wrap: balance / pretty

```css
/* Headlines: balanced line lengths */
h1, h2, h3 { text-wrap: balance; }

/* Body paragraphs: avoid orphans */
p { text-wrap: pretty; }
```

## Logical Properties

Future-proof for RTL/LTR:

```css
/* ✅ Modern */
.element {
  margin-inline: auto;
  padding-block: 16px;
  padding-inline: 24px;
  border-inline-start: 3px solid var(--primary);
}

/* ❌ Old way */
.element {
  margin-left: auto; margin-right: auto;
  padding-top: 16px; padding-bottom: 16px;
}
```

## oklch() Color Space

Perceptually uniform — colors of the same lightness actually LOOK the same brightness:

```css
:root {
  /* Same perceived lightness across hues */
  --red:    oklch(0.65 0.2 25);
  --orange: oklch(0.65 0.18 55);
  --green:  oklch(0.65 0.18 145);
  --blue:   oklch(0.65 0.2 260);
  --purple: oklch(0.65 0.2 300);
}
```

## Subgrid

Child grids align to parent grid tracks:

```css
.grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }

.grid-item {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3; /* align header, body, footer across cards */
}
```

## Scroll-Driven Animations

```css
/* Progress bar tied to scroll position */
.progress {
  position: fixed; top: 0; left: 0; right: 0; height: 3px;
  background: var(--primary);
  transform-origin: left;
  animation: grow-progress linear;
  animation-timeline: scroll();
}

@keyframes grow-progress {
  from { transform: scaleX(0); }
  to   { transform: scaleX(1); }
}
```

## @property — Typed Custom Properties

```css
@property --gradient-angle {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}

.animated-gradient {
  --gradient-angle: 0deg;
  background: conic-gradient(from var(--gradient-angle), var(--primary), var(--accent), var(--primary));
  transition: --gradient-angle 0.5s ease;
}
.animated-gradient:hover { --gradient-angle: 180deg; }
```
