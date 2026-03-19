# Color

## Semantic Naming

Never reference raw hex values. Use semantic names that describe **purpose**, not appearance.

| Token | Use for | NOT for |
|-------|---------|---------|
| `primary` | Main actions, active states, links | Random decoration |
| `accent` | Highlights, badges, attention | Body text |
| `success` | Completed, positive, approved | Unrelated green things |
| `warning` | Caution, pending, needs attention | Decoration |
| `error` | Failed, destructive, blocked | Emphasis (use bold) |
| `neutral` | Text, borders, backgrounds, dividers | Everything else |

## The 60-30-10 Rule

```
60% — Neutral/background    (whites, light grays, dark backgrounds)
30% — Secondary/structure    (medium tones, borders, cards)
10% — Accent/primary         (CTAs, highlights, key elements)
```

Breaking this ratio makes designs feel chaotic or flat.

## Ready-to-Use Palettes

### 🏢 Professional (Dark + Blue)
```json
{
  "primary": "#2563EB",
  "accent": "#F59E0B",
  "success": "#10B981",
  "warning": "#F59E0B",
  "error": "#EF4444",
  "bg": "#FFFFFF",
  "surface": "#F9FAFB",
  "border": "#E5E7EB",
  "text": "#111827",
  "textMuted": "#6B7280"
}
```

### 🎨 Creative (Warm + Vibrant)
```json
{
  "primary": "#7C3AED",
  "accent": "#F97316",
  "success": "#22C55E",
  "warning": "#EAB308",
  "error": "#DC2626",
  "bg": "#FFFBF5",
  "surface": "#FEF3E2",
  "border": "#E8D5C4",
  "text": "#1C1917",
  "textMuted": "#78716C"
}
```

### 🖤 Minimal (Monochrome + Accent)
```json
{
  "primary": "#18181B",
  "accent": "#2563EB",
  "success": "#16A34A",
  "warning": "#CA8A04",
  "error": "#DC2626",
  "bg": "#FFFFFF",
  "surface": "#FAFAFA",
  "border": "#E4E4E7",
  "text": "#09090B",
  "textMuted": "#71717A"
}
```

## Accessibility

**WCAG AA minimum contrast ratios:**

| Element | Ratio | Example |
|---------|-------|---------|
| Body text | 4.5:1 | #6B7280 on #FFFFFF = ✅ 4.6:1 |
| Large text (18px+) | 3:1 | Headers can use lighter colors |
| UI components | 3:1 | Buttons, icons, borders |

**Quick check:** If you squint and can't read it, contrast is too low.

## Platform Color Maps

### Notion (10 colors + 10 backgrounds)
| Semantic | Notion color | Notion background |
|----------|-------------|-------------------|
| Primary/Info | `blue` | `blue_background` |
| Success | `green` | `green_background` |
| Warning | `orange` / `yellow` | `orange_background` / `yellow_background` |
| Error | `red` | `red_background` |
| Neutral | `gray` | `gray_background` |
| Accent | `purple` | `purple_background` |
| Warm highlight | `pink` / `brown` | `pink_background` / `brown_background` |

### HTML
Full spectrum via CSS. Use CSS custom properties for theming:
```css
:root {
  --color-primary: #2563EB;
  --color-accent: #F59E0B;
}
```

### GitHub Markdown
Limited to alert types: NOTE (blue), TIP (green), IMPORTANT (purple), WARNING (yellow), CAUTION (red).

## Color Don'ts

- ❌ Red text for non-error content
- ❌ More than 3-4 colors on one page (excluding neutrals)
- ❌ Color as the ONLY differentiator (accessibility: add icons/labels)
- ❌ Saturated backgrounds with text on top (use tinted/muted backgrounds)
- ❌ Different blues for the same purpose across pages
