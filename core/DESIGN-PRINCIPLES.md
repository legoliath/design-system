# Design Principles

Universal rules for visual design. Apply regardless of platform.

## Visual Hierarchy

Control what the eye sees first through **size, weight, color, position**.

```
MOST IMPORTANT     ← Largest, boldest, highest contrast
  ├── Secondary    ← Medium size, less weight
  │   ├── Details  ← Smaller, muted color
  │   └── Meta     ← Smallest, gray/subdued
  └── Actions      ← Color contrast (accent/primary)
```

- **One focal point per view.** If everything screams, nothing does.
- **Size jumps matter.** A 2px difference is invisible. Use minimum 1.25x ratio between levels.
- **Position = importance.** Top-left (LTR) is seen first. Put key info there.

## Whitespace

Whitespace is not empty — it's a design tool.

- **Group related items** with tight spacing (4-8px).
- **Separate sections** with generous spacing (24-48px).
- **Margins > borders** for separation. Borders add visual noise.
- **Padding inside containers** should be consistent (16-24px default).
- When in doubt, **add more whitespace**, not less.

## Contrast

Not just color contrast — contrast in **every dimension**:

| Dimension | Low contrast (flat) | High contrast (clear) |
|-----------|--------------------|-----------------------|
| Size | 14px vs 16px | 14px vs 24px |
| Weight | 400 vs 500 | 400 vs 700 |
| Color | gray vs dark gray | gray vs black |
| Density | wall of text | text + breathing room |

## Rhythm & Repetition

- **Use a spacing scale** (4, 8, 16, 24, 48px). Never arbitrary values.
- **Repeat patterns.** If section 1 has icon + title + body, all sections should.
- **Consistent element sizing.** All cards same height. All icons same size.
- **Vertical rhythm.** Maintain consistent line-height multiples.

## Alignment

- **Left-align by default.** Center only for short text (titles, CTAs).
- **Use invisible grids.** Elements should align to the same vertical/horizontal lines.
- **Indent = relationship.** Nested content should be visually nested.

## Progressive Disclosure

- **Most important info visible immediately.**
- **Details on demand** (toggles, expandable sections, hover states).
- **Summarize, then elaborate.** Lead with the conclusion.

## The Squint Test

Blur your eyes or zoom out to 25%. Check:
- [ ] Can you identify the page structure?
- [ ] Is there a clear focal point?
- [ ] Are sections visually separated?
- [ ] Does it feel balanced (not top-heavy or lopsided)?

If the answer is no, the layout needs work before the content does.
