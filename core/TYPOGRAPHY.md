# Typography

## Type Scale

Use a consistent ratio between sizes. Recommended: **1.25 (minor third)**.

```
Display:  40px  — Page titles, hero text
H1:       32px  — Section headers
H2:       25.6px — Subsection headers  
H3:       20.5px — Group headers
Body:     16px  — Default reading text
Small:    12.8px — Captions, meta, timestamps
```

Never pick arbitrary sizes. Pick a base (16px) and multiply/divide by the ratio.

## Font Roles

| Role | Purpose | Style |
|------|---------|-------|
| **Display** | Hero titles, covers | Bold/Black weight, tight letter-spacing |
| **Heading** | Section structure | Semi-bold to Bold (600-700) |
| **Body** | Reading text | Regular (400), generous line-height |
| **Mono** | Code, data, technical | Fixed-width, slightly smaller |

## Line Height

| Context | Line height | Why |
|---------|-------------|-----|
| Headings | 1.1 – 1.25 | Tight = compact, authoritative |
| Body text | 1.5 – 1.6 | Readable, comfortable scanning |
| UI labels | 1.2 – 1.3 | Compact but legible |
| Code | 1.4 – 1.5 | Balance density and readability |

## Line Width

**60–75 characters per line** for body text. Wider = eyes lose the next line.

- Full-width pages need max-width on text containers.
- Notion: use non-full-width mode for long-form text.
- HTML: `max-width: 65ch` on text containers.

## Font Pairing Rules

- **Max 2 fonts** per project. One for headings, one for body.
- **Contrast in category**: Sans heading + Serif body, or vice versa.
- **Never pair similar fonts.** Two sans-serifs that look alike = visual confusion.

## Serif vs Sans vs Mono

| When | Use |
|------|-----|
| Professional docs, reports, long reads | Serif (Georgia, Garamond) |
| UI, dashboards, modern feel | Sans-serif (Inter, System) |
| Code, data tables, technical docs | Mono (JetBrains Mono, Fira Code) |
| Notion pages | Default (sans) for dashboards, Serif for articles |

## Weight as Hierarchy

Don't rely on size alone. Weight creates hierarchy within the same size:

```
700 (Bold)    — Titles, key metrics, CTAs
600 (Semi)    — Subheadings, labels
400 (Regular) — Body text, descriptions  
300 (Light)   — Secondary info, captions (only on large sizes)
```

**Never use Light (300) below 16px.** It becomes illegible.

## Letter Spacing

- **Headings**: -0.01em to -0.02em (slightly tighter)
- **Body**: 0 (default)
- **ALL CAPS labels**: +0.05em to +0.1em (must be wider)
- **Small text**: +0.01em (slight increase for readability)
