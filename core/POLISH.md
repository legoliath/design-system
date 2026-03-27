# Polish — Micro-Interactions & Visual Refinement

The 20% effort that creates 80% of the "wow" factor.

## Transitions

**Default for everything interactive:**
```css
/* Standard easing — use this everywhere */
--ease-out: cubic-bezier(0.4, 0, 0.2, 1);
--ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);

/* Apply to interactive elements */
.interactive {
  transition: all 0.2s var(--ease-out);
}
```

**Never animate without easing.** `linear` = robotic. `ease-out` = natural.

## Hover States

### Cards
```css
.card {
  transition: transform 0.2s var(--ease-out), box-shadow 0.2s var(--ease-out);
}
.card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-elevated);
}
.card:active {
  transform: translateY(0);
  box-shadow: var(--shadow-card);
}
```

### Buttons
```css
.btn {
  transition: background 0.15s var(--ease-out), transform 0.1s var(--ease-out);
}
.btn:hover {
  background: color-mix(in srgb, var(--primary) 85%, black);
}
.btn:active {
  transform: scale(0.97);
}
```

### Links
```css
a {
  color: var(--primary);
  text-decoration: underline;
  text-underline-offset: 2px;
  text-decoration-color: color-mix(in srgb, var(--primary) 30%, transparent);
  transition: text-decoration-color 0.15s ease;
}
a:hover {
  text-decoration-color: var(--primary);
}
```

## Glassmorphism

```css
.glass {
  background: color-mix(in srgb, var(--surface) 70%, transparent);
  backdrop-filter: blur(12px) saturate(180%);
  -webkit-backdrop-filter: blur(12px) saturate(180%);
  border: 1px solid color-mix(in srgb, white 20%, transparent);
  border-radius: 12px;
}
```

Use for: floating nav bars, modals, sidebars over content.

## Gradient Backgrounds

### Subtle Page Gradient
```css
body {
  background:
    linear-gradient(135deg, oklch(0.97 0.01 80) 0%, oklch(0.98 0.005 240) 100%);
  min-height: 100vh;
}
```

### Mesh-Style Gradient (multiple radials)
```css
.hero-bg {
  background:
    radial-gradient(ellipse at 20% 50%, oklch(0.92 0.04 280 / 0.3) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 20%, oklch(0.92 0.04 200 / 0.2) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 80%, oklch(0.92 0.04 330 / 0.15) 0%, transparent 50%),
    var(--bg);
}
```

### Gradient Text
```css
.gradient-text {
  background: linear-gradient(135deg, var(--primary), var(--accent));
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
```

## Glow Effects

```css
/* Button glow */
.btn-glow {
  box-shadow:
    0 0 0 1px var(--primary),
    0 0 12px color-mix(in srgb, var(--primary) 25%, transparent),
    0 0 24px color-mix(in srgb, var(--primary) 10%, transparent);
}

/* Status dot glow */
.status-dot {
  width: 8px; height: 8px; border-radius: 50%;
  background: var(--success);
  box-shadow: 0 0 0 3px color-mix(in srgb, var(--success) 20%, transparent);
}
```

## Animated Status Dot

```css
.status-live {
  width: 8px; height: 8px; border-radius: 50%;
  background: var(--success);
  position: relative;
}
.status-live::after {
  content: '';
  position: absolute;
  inset: -3px;
  border-radius: 50%;
  border: 2px solid var(--success);
  animation: pulse 2s ease-out infinite;
}
@keyframes pulse {
  0%   { opacity: 1; transform: scale(1); }
  100% { opacity: 0; transform: scale(2); }
}
```

## Loading Skeleton

```css
.skeleton {
  background: linear-gradient(
    90deg,
    var(--surface) 25%,
    color-mix(in srgb, var(--surface) 80%, var(--text-muted)) 50%,
    var(--surface) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s ease-in-out infinite;
  border-radius: 8px;
}
@keyframes shimmer {
  0%   { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

/* Usage */
.skeleton-text { height: 1em; width: 80%; }
.skeleton-title { height: 1.5em; width: 60%; }
.skeleton-avatar { height: 40px; width: 40px; border-radius: 50%; }
```

## Focus Styles

```css
/* Visible focus ring — accessible and beautiful */
:focus-visible {
  outline: 2px solid var(--primary);
  outline-offset: 2px;
  border-radius: 4px;
}

/* Remove default outline for mouse users */
:focus:not(:focus-visible) {
  outline: none;
}
```

## Scroll Shadows (Pure CSS)

Indicates scrollable content without JS:

```css
.scroll-container {
  overflow-y: auto;
  background:
    linear-gradient(var(--surface) 30%, transparent) center top,
    linear-gradient(transparent, var(--surface) 70%) center bottom,
    radial-gradient(farthest-side at 50% 0, rgba(0,0,0,0.12), transparent) center top,
    radial-gradient(farthest-side at 50% 100%, rgba(0,0,0,0.12), transparent) center bottom;
  background-repeat: no-repeat;
  background-size: 100% 40px, 100% 40px, 100% 12px, 100% 12px;
  background-attachment: local, local, scroll, scroll;
}
```

## Smooth Counters (CSS @property)

```css
@property --num {
  syntax: '<integer>';
  initial-value: 0;
  inherits: false;
}

.counter {
  --num: 0;
  transition: --num 1.5s ease-out;
  counter-reset: num var(--num);
}
.counter::after {
  content: counter(num);
}

/* Trigger: set --num via inline style or class */
.counter.visible { --num: 847; }
```

## Animated Gradient Border

```css
.gradient-border {
  position: relative;
  border-radius: 12px;
  padding: 24px;
  background: var(--surface);
}
.gradient-border::before {
  content: '';
  position: absolute;
  inset: -1px;
  border-radius: inherit;
  background: linear-gradient(135deg, var(--primary), var(--accent), var(--primary));
  background-size: 200% 200%;
  z-index: -1;
  animation: gradient-spin 3s linear infinite;
}
@keyframes gradient-spin {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

## Ripple Effect on Click (Pure CSS)

```css
.btn-ripple {
  position: relative;
  overflow: hidden;
}
.btn-ripple::after {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at var(--ripple-x, 50%) var(--ripple-y, 50%), rgba(255,255,255,0.3) 0%, transparent 60%);
  opacity: 0;
  transition: opacity 0.5s ease;
}
.btn-ripple:active::after {
  opacity: 1;
  transition: opacity 0s;
}
```

## Subtle Background Texture

Flat backgrounds feel dead. Add barely-visible texture:

```css
/* Dot pattern */
.textured-bg {
  background-image: radial-gradient(circle, var(--border-subtle) 1px, transparent 1px);
  background-size: 24px 24px;
}

/* Grid lines */
.grid-bg {
  background-image:
    linear-gradient(var(--border-subtle) 1px, transparent 1px),
    linear-gradient(90deg, var(--border-subtle) 1px, transparent 1px);
  background-size: 48px 48px;
}

/* Noise texture (CSS only, no image) */
.noise-bg {
  position: relative;
}
.noise-bg::before {
  content: '';
  position: absolute;
  inset: 0;
  opacity: 0.03;
  background: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  pointer-events: none;
}
```

## Smooth Reveal on Scroll (CSS only)

```css
@keyframes fade-up {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.reveal {
  animation: fade-up 0.6s var(--ease-out) both;
  animation-timeline: view();
  animation-range: entry 0% entry 40%;
}
```

## Tooltip (Pure CSS)

```css
[data-tooltip] {
  position: relative;
}
[data-tooltip]::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: calc(100% + 8px);
  left: 50%;
  transform: translateX(-50%) translateY(4px);
  padding: 4px 10px;
  border-radius: var(--radius-md);
  background: var(--grey-900, #1a1a2e);
  color: white;
  font-size: 0.75rem;
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.15s ease, transform 0.15s ease;
}
[data-tooltip]:hover::after {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}
```

## Progress Bar

```css
.progress-track {
  height: 8px;
  background: var(--grey-200, #e5e7eb);
  border-radius: var(--radius-full);
  overflow: hidden;
}
.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--primary), var(--accent));
  border-radius: inherit;
  transition: width 0.6s var(--ease-out);
}
```

## Avatars with Ring

```css
.avatar {
  width: 40px; height: 40px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid var(--surface);
  box-shadow: 0 0 0 2px var(--primary);
}

/* Stacked avatar group */
.avatar-group {
  display: flex;
}
.avatar-group .avatar {
  margin-inline-start: -12px;
}
.avatar-group .avatar:first-child {
  margin-inline-start: 0;
}
```

## Dark Mode Considerations

```css
/* Shadows need more opacity in dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --shadow-card:
      0 1px 2px rgba(0,0,0,0.2),
      0 2px 4px rgba(0,0,0,0.15),
      0 4px 8px rgba(0,0,0,0.1);
    
    --shadow-elevated:
      0 2px 4px rgba(0,0,0,0.25),
      0 4px 8px rgba(0,0,0,0.2),
      0 8px 16px rgba(0,0,0,0.15),
      0 16px 32px rgba(0,0,0,0.1);
  }
  
  /* Glassmorphism is darker */
  .glass {
    background: color-mix(in srgb, var(--surface) 50%, transparent);
  }
}
```
