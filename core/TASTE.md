# Taste — Visual Design Tactics

Not theory. Tactics that make things look good instantly.

## Hierarchy Without Size

Size alone is lazy. Use **weight**, **color**, and **spacing** together:

```
✅ Good:  Label (12px, 600, muted) + Value (14px, 700, primary)
❌ Bad:   Label (14px, 400) + Value (24px, 400) — size doing all the work
```

- **Bold > Big.** A 14px bold label beats a 20px regular one.
- **Muted > Smaller.** Gray at 14px is less prominent than black at 12px.
- **ALL-CAPS + letter-spacing** for labels: `text-transform: uppercase; font-size: 0.75rem; letter-spacing: 0.05em; color: var(--text-muted);`

## Fewer Borders, More Depth

Borders add noise. Replace them:

| Instead of | Use |
|-----------|-----|
| `border: 1px solid #ddd` | `box-shadow: 0 1px 3px rgba(0,0,0,0.08)` |
| Border between sections | Background color change |
| Border around cards | Shadow + border-radius |
| Horizontal rule | Generous spacing (48px+) |

When you DO use borders, make them subtle: `border: 1px solid color-mix(in srgb, var(--text) 8%, transparent)`

## Multi-Layer Shadows

One shadow = flat. Multiple = realistic depth:

```css
/* Resting card */
--shadow-card: 
  0 1px 2px rgba(0,0,0,0.06),
  0 2px 4px rgba(0,0,0,0.04),
  0 4px 8px rgba(0,0,0,0.03);

/* Elevated/hover */
--shadow-elevated:
  0 2px 4px rgba(0,0,0,0.06),
  0 4px 8px rgba(0,0,0,0.05),
  0 8px 16px rgba(0,0,0,0.04),
  0 16px 32px rgba(0,0,0,0.03);

/* Floating (modals, dropdowns) */
--shadow-floating:
  0 4px 8px rgba(0,0,0,0.08),
  0 8px 16px rgba(0,0,0,0.06),
  0 16px 32px rgba(0,0,0,0.05),
  0 24px 48px rgba(0,0,0,0.04);
```

## Color Tactics

### Tinted Status Backgrounds
Never use raw colors as backgrounds. Tint them:

```css
/* ✅ Correct — soft tinted backgrounds */
.status-success { background: color-mix(in srgb, #10b981 8%, white); color: #047857; }
.status-warning { background: color-mix(in srgb, #f59e0b 10%, white); color: #92400e; }
.status-error   { background: color-mix(in srgb, #ef4444 8%, white); color: #b91c1c; }
.status-info    { background: color-mix(in srgb, #3b82f6 8%, white); color: #1d4ed8; }

/* ❌ Wrong — raw saturated backgrounds */
.status-error { background: #ef4444; color: white; }
```

### Accent Like Seasoning
- 60% neutral (backgrounds, surfaces)
- 30% supporting (borders, secondary text, muted elements)
- 10% accent (CTAs, active states, key highlights)

### Warm + Cool Balance
Mix warm and cool tones. Pure cool = clinical. Pure warm = dated.
- Warm background (`oklch(0.985 0.002 80)`) + cool accent (`oklch(0.55 0.2 260)`) = sophisticated
- Use warm grays for text, cool grays for borders

## Spacing Tactics

### Asymmetric Whitespace
Don't center everything. Offset creates visual interest:
- More space above sections than below
- Left-heavy content with right breathing room
- Generous top padding on first section (96px+), tight between related items (8-12px)

### Spacing Groups
Tight spacing = related. Wide spacing = separate:
```
Related items:    8px gap
Section content: 16px gap  
Between sections: 48px gap
Major sections:   96px gap
```

## Card Design

```css
.card {
  background: var(--surface);
  border-radius: 12px;
  padding: 24px;
  box-shadow: var(--shadow-card);
  transition: box-shadow 0.2s ease, transform 0.2s ease;
}
.card:hover {
  box-shadow: var(--shadow-elevated);
  transform: translateY(-2px);
}
```

- Padding: 24px minimum (32px for spacious feel)
- Border-radius: 12px (8px minimum, 16px for larger cards)
- Never put a card inside a card (nesting kills clarity)

## Typography Tactics

- **Headlines:** Tight letter-spacing (-0.02em), tight line-height (1.1-1.2)
- **Body:** Generous line-height (1.6), max-width 65ch
- **Labels:** ALL-CAPS, 0.75rem, letter-spacing 0.05em, muted color
- **Numbers/metrics:** Tabular nums, bold, larger than surrounding text
- **Code:** Slightly smaller (0.9em), different background tint

## Don't Use Grey on Colored Backgrounds

On white backgrounds, grey text = less contrast = de-emphasized. Good.
On colored backgrounds, grey text looks WRONG. It clashes.

**Two fixes:**
```css
/* Option 1: White text with reduced opacity */
.on-colored-bg .secondary-text {
  color: rgba(255, 255, 255, 0.7);
}

/* Option 2: Same-hue lighter color */
.on-blue-bg .secondary-text {
  color: oklch(0.85 0.08 250); /* lighter blue, not grey */
}
```

The principle: reduce **contrast**, not add grey. Match the hue of the background.

## Accent Borders — Instant Visual Flair

No design talent needed. A colored stripe transforms bland UI:

```css
/* Top accent bar on entire page */
body::before {
  content: '';
  display: block;
  height: 4px;
  background: linear-gradient(90deg, var(--primary), var(--accent));
}

/* Left accent on cards/alerts */
.alert {
  border-left: 4px solid var(--primary);
  padding-left: var(--space-md);
}

/* Active nav item */
.nav-item.active {
  border-left: 3px solid var(--primary);
  padding-left: calc(var(--space-sm) - 3px); /* compensate border width */
}

/* Top accent on card */
.featured-card {
  border-top: 3px solid var(--accent);
}
```

## Icons — Don't Blow Them Up

Icons designed at 16-24px look chunky at 48px+. Instead:

```css
/* Enclose small icons in a colored shape */
.icon-wrap {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: var(--radius-lg);
  background: var(--info-tint);
  color: var(--info);
}
.icon-wrap svg {
  width: 24px;
  height: 24px;
}
```

The icon stays at its intended size. The shape fills the space.

## Button Hierarchy — Not Every Button Needs a Background

```css
/* Primary: solid, high contrast — ONE per section max */
.btn-primary {
  background: var(--primary);
  color: white;
  border: none;
  font-weight: 600;
}

/* Secondary: outline, visible but not dominant */
.btn-secondary {
  background: transparent;
  color: var(--primary);
  border: 1px solid var(--border);
}

/* Tertiary: link-style, discoverable but quiet */
.btn-tertiary {
  background: transparent;
  color: var(--text-muted);
  border: none;
  padding: 0;
  text-decoration: underline;
  text-underline-offset: 2px;
}

/* Destructive: only red when it's the PRIMARY action */
.btn-danger {
  background: var(--error);
  color: white;
}
/* If destructive is secondary, DON'T make it red: */
.btn-danger-secondary {
  background: transparent;
  color: var(--text-muted);
  border: 1px solid var(--border);
}
```

## Empty States — The Forgotten Screen

Empty states are where users land first. Make them beautiful:

```css
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: var(--space-4xl) var(--space-lg);
  color: var(--text-muted);
}
.empty-state .icon-wrap {
  width: 64px; height: 64px;
  border-radius: 50%;
  margin-block-end: var(--space-lg);
}
.empty-state h3 {
  color: var(--text);
  margin-block-end: var(--space-xs);
}
.empty-state p {
  max-width: 40ch;
  margin-block-end: var(--space-lg);
}
```

## Visual Polish Checklist

Before calling any page "done":
- [ ] No raw borders — shadows or spacing instead
- [ ] Multi-layer shadows on elevated elements
- [ ] Hover states with transform + shadow change
- [ ] Tinted status colors (not raw)
- [ ] Consistent spacing scale (no arbitrary values)
- [ ] Labels are ALL-CAPS + letter-spaced + muted
- [ ] Max-width on text (65ch)
- [ ] System font stack (no external font loading)
- [ ] Focus-visible styles for accessibility
- [ ] Transitions on interactive elements (0.2s ease)
