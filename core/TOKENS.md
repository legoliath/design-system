# Tokens — Design Token System

Complete, opinionated token system. Copy-paste into any project.

## Font Stacks (System Fonts — Zero Load Time)

```css
:root {
  /* Primary UI font */
  --font-sans: system-ui, -apple-system, sans-serif;
  
  /* Humanist — warmer, more personality */
  --font-humanist: Seravek, 'Gill Sans Nova', Ubuntu, Calibri, 'DejaVu Sans', source-sans-pro, sans-serif;
  
  /* Neo-Grotesque — clean, modern */
  --font-neo: Inter, Roboto, 'Helvetica Neue', 'Arial Nova', 'Nimbus Sans', Arial, sans-serif;
  
  /* Serif — editorial, long-form */
  --font-serif: Charter, 'Bitstream Charter', 'Sitka Text', Cambria, serif;
  
  /* Monospace — code, data */
  --font-mono: ui-monospace, 'Cascadia Code', 'Source Code Pro', Menlo, Consolas, 'DejaVu Sans Mono', monospace;
}
```

**When to use which:**
- `--font-sans` → Default for everything (UI, dashboards)
- `--font-humanist` → Friendly tone (landing pages, onboarding)
- `--font-neo` → Technical/clean (SaaS, developer tools)
- `--font-serif` → Editorial (articles, reports, documentation)
- `--font-mono` → Code, data tables, terminal-style

## Spacing Scale

```css
:root {
  --space-2xs: 4px;
  --space-xs:  8px;
  --space-sm:  12px;
  --space-md:  16px;
  --space-lg:  24px;
  --space-xl:  32px;
  --space-2xl: 48px;
  --space-3xl: 64px;
  --space-4xl: 96px;
}
```

**Usage guide:**
- `2xs/xs` → Icon gaps, inline spacing
- `sm/md` → Component internal padding
- `lg/xl` → Card padding, section spacing
- `2xl/3xl` → Between major sections
- `4xl` → Hero spacing, page-level separation

## Border Radius

```css
:root {
  --radius-sm:   4px;
  --radius-md:   8px;
  --radius-lg:   12px;
  --radius-xl:   16px;
  --radius-2xl:  24px;
  --radius-full: 9999px;  /* pill shape */
}
```

- Buttons/badges: `--radius-md`
- Cards: `--radius-lg`
- Large cards/modals: `--radius-xl`
- Tags/pills: `--radius-full`

## Shadow Scale

```css
:root {
  --shadow-xs:
    0 1px 2px rgba(0,0,0,0.05);
  
  --shadow-sm:
    0 1px 2px rgba(0,0,0,0.06),
    0 1px 3px rgba(0,0,0,0.04);
  
  --shadow-md:
    0 1px 2px rgba(0,0,0,0.06),
    0 2px 4px rgba(0,0,0,0.04),
    0 4px 8px rgba(0,0,0,0.03);
  
  --shadow-lg:
    0 2px 4px rgba(0,0,0,0.06),
    0 4px 8px rgba(0,0,0,0.05),
    0 8px 16px rgba(0,0,0,0.04),
    0 16px 32px rgba(0,0,0,0.03);
  
  --shadow-xl:
    0 4px 8px rgba(0,0,0,0.08),
    0 8px 16px rgba(0,0,0,0.06),
    0 16px 32px rgba(0,0,0,0.05),
    0 24px 48px rgba(0,0,0,0.04);
}
```

## Animation Tokens

```css
:root {
  --ease-out:    cubic-bezier(0.4, 0, 0.2, 1);
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
  
  --duration-fast:   0.1s;
  --duration-normal: 0.2s;
  --duration-slow:   0.35s;
}
```

---

## Complete Palettes

### 🌙 Midnight (Dark, Sophisticated)

```css
:root[data-theme="midnight"], .theme-midnight {
  --bg:            oklch(0.16 0.01 260);
  --surface:       oklch(0.20 0.01 260);
  --surface-raised:oklch(0.24 0.01 260);
  --border:        oklch(0.30 0.01 260);
  --border-subtle: oklch(0.25 0.01 260);
  --text:          oklch(0.93 0.005 260);
  --text-muted:    oklch(0.65 0.01 260);
  
  --primary:       oklch(0.70 0.18 250);
  --primary-hover: oklch(0.65 0.20 250);
  --accent:        oklch(0.75 0.15 160);
  
  --success:       oklch(0.72 0.18 155);
  --success-tint:  oklch(0.25 0.04 155);
  --warning:       oklch(0.78 0.16 80);
  --warning-tint:  oklch(0.28 0.04 80);
  --error:         oklch(0.65 0.22 25);
  --error-tint:    oklch(0.25 0.05 25);
  --info:          oklch(0.70 0.15 250);
  --info-tint:     oklch(0.25 0.04 250);
}
```

### 🌅 Dawn (Warm, Inviting)

```css
:root[data-theme="dawn"], .theme-dawn {
  --bg:            oklch(0.97 0.008 70);
  --surface:       oklch(0.995 0.003 70);
  --surface-raised:oklch(1.0 0 0);
  --border:        oklch(0.90 0.01 70);
  --border-subtle: oklch(0.93 0.008 70);
  --text:          oklch(0.20 0.02 50);
  --text-muted:    oklch(0.55 0.02 50);
  
  --primary:       oklch(0.55 0.2 260);
  --primary-hover: oklch(0.50 0.22 260);
  --accent:        oklch(0.65 0.2 25);
  
  --success:       oklch(0.55 0.18 155);
  --success-tint:  oklch(0.95 0.03 155);
  --warning:       oklch(0.65 0.18 70);
  --warning-tint:  oklch(0.95 0.04 70);
  --error:         oklch(0.55 0.22 25);
  --error-tint:    oklch(0.95 0.04 25);
  --info:          oklch(0.55 0.18 250);
  --info-tint:     oklch(0.95 0.03 250);
}
```

### ❄️ Arctic (Clean, Minimal)

```css
:root[data-theme="arctic"], .theme-arctic, :root {
  --bg:            oklch(0.975 0.003 240);
  --surface:       oklch(1.0 0 0);
  --surface-raised:oklch(1.0 0 0);
  --border:        oklch(0.91 0.005 240);
  --border-subtle: oklch(0.94 0.003 240);
  --text:          oklch(0.15 0.01 260);
  --text-muted:    oklch(0.50 0.01 260);
  
  --primary:       oklch(0.55 0.22 260);
  --primary-hover: oklch(0.50 0.24 260);
  --accent:        oklch(0.68 0.16 175);
  
  --success:       oklch(0.55 0.18 155);
  --success-tint:  oklch(0.95 0.03 155);
  --warning:       oklch(0.65 0.16 80);
  --warning-tint:  oklch(0.96 0.03 80);
  --error:         oklch(0.58 0.22 25);
  --error-tint:    oklch(0.96 0.03 25);
  --info:          oklch(0.58 0.18 250);
  --info-tint:     oklch(0.96 0.02 250);
}
```

### Auto Dark/Light

```css
/* Default: Arctic (light) */
:root { /* Arctic tokens above */ }

/* Auto dark mode: Midnight */
@media (prefers-color-scheme: dark) {
  :root {
    /* Midnight tokens above */
  }
}
```

## Full Color Scales (Refactoring UI Method)

Don't pick 5 colors. Pick 1 base per color, then generate 9 shades (100-900).
Use the edges (100 for tinted bg, 900 for text), then fill in between.

```css
:root {
  /* Blue scale — primary */
  --blue-50:  oklch(0.97 0.02 250);
  --blue-100: oklch(0.93 0.04 250);
  --blue-200: oklch(0.86 0.08 250);
  --blue-300: oklch(0.76 0.12 250);
  --blue-400: oklch(0.66 0.17 250);
  --blue-500: oklch(0.55 0.22 250);  /* ← base: good button color */
  --blue-600: oklch(0.48 0.20 250);
  --blue-700: oklch(0.40 0.17 250);
  --blue-800: oklch(0.33 0.13 250);
  --blue-900: oklch(0.25 0.10 250);  /* ← text on blue-50 bg */

  /* Green scale — success */
  --green-50:  oklch(0.97 0.02 155);
  --green-100: oklch(0.93 0.04 155);
  --green-200: oklch(0.85 0.10 155);
  --green-300: oklch(0.75 0.15 155);
  --green-400: oklch(0.65 0.18 155);
  --green-500: oklch(0.55 0.18 155);
  --green-600: oklch(0.48 0.16 155);
  --green-700: oklch(0.40 0.13 155);
  --green-800: oklch(0.33 0.10 155);
  --green-900: oklch(0.25 0.08 155);

  /* Red scale — error/danger */
  --red-50:  oklch(0.97 0.02 25);
  --red-100: oklch(0.93 0.04 25);
  --red-200: oklch(0.86 0.08 25);
  --red-300: oklch(0.76 0.14 25);
  --red-400: oklch(0.66 0.19 25);
  --red-500: oklch(0.58 0.22 25);
  --red-600: oklch(0.50 0.20 25);
  --red-700: oklch(0.42 0.17 25);
  --red-800: oklch(0.35 0.13 25);
  --red-900: oklch(0.28 0.10 25);

  /* Yellow/Amber scale — warning */
  --amber-50:  oklch(0.98 0.02 80);
  --amber-100: oklch(0.95 0.04 80);
  --amber-200: oklch(0.88 0.10 80);
  --amber-300: oklch(0.80 0.14 80);
  --amber-400: oklch(0.72 0.16 80);
  --amber-500: oklch(0.65 0.16 80);
  --amber-600: oklch(0.55 0.14 80);
  --amber-700: oklch(0.45 0.12 80);
  --amber-800: oklch(0.38 0.09 80);
  --amber-900: oklch(0.30 0.07 80);

  /* Grey scale (cool-tinted, not pure grey) */
  --grey-50:  oklch(0.98 0.003 260);
  --grey-100: oklch(0.96 0.004 260);
  --grey-200: oklch(0.92 0.005 260);
  --grey-300: oklch(0.87 0.006 260);
  --grey-400: oklch(0.71 0.007 260);
  --grey-500: oklch(0.55 0.008 260);
  --grey-600: oklch(0.45 0.009 260);
  --grey-700: oklch(0.37 0.010 260);
  --grey-800: oklch(0.27 0.010 260);
  --grey-900: oklch(0.18 0.010 260);
}
```

**Usage pattern:**
- `*-50` / `*-100` → tinted backgrounds (alerts, badges, tags)
- `*-200` / `*-300` → borders, dividers on tinted sections
- `*-400` / `*-500` → icons, interactive elements, buttons
- `*-600` / `*-700` → hover states, active states
- `*-800` / `*-900` → text on light backgrounds

**Never pick ONE hex.** Always build a scale. The scales let you create tinted alerts, subtle badges, contextual backgrounds — the things that make UI look "designed".

## Open Props (Optional Enhancement)

For projects that want even more tokens, add Open Props via CDN:

```html
<link rel="stylesheet" href="https://unpkg.com/open-props">
```

This gives you 400+ design tokens. Use alongside our custom tokens — they complement each other.
