# Typst Adapter

Modern typesetting for beautiful PDFs. Faster and simpler than LaTeX.

## Quick Start

```bash
# Install
brew install typst          # macOS
# or: cargo install typst-cli

# Compile
typst compile report.typ    # → report.pdf
typst watch report.typ      # auto-recompile on save
```

## Basics

```typst
// Document setup
#set page(paper: "a4", margin: 2cm)
#set text(font: "New Computer Modern", size: 11pt)
#set heading(numbering: "1.1")
#set par(justify: true)

// Content
= Report Title

== Introduction

This is body text with *bold*, _italic_, and `code`.

- Bullet point
- Another point
  - Nested

+ Numbered item
+ Second item
```

## Page Setup & Show Rules

```typst
// Professional report setup
#set page(
  paper: "a4",
  margin: (top: 3cm, bottom: 2.5cm, left: 2.5cm, right: 2cm),
  header: [
    #set text(8pt, fill: gray)
    Project Report — #datetime.today().display("[month repr:long] [year]")
    #line(length: 100%, stroke: 0.5pt + gray)
  ],
  footer: context [
    #set align(center)
    #set text(8pt)
    #counter(page).display("— 1 —")
  ],
)

// Heading style
#show heading.where(level: 1): it => {
  set text(16pt, weight: "bold", fill: rgb("#2563EB"))
  block(above: 1.5em, below: 0.8em)[#it]
}

#show heading.where(level: 2): it => {
  set text(13pt, weight: "semibold")
  block(above: 1.2em, below: 0.6em)[#it]
}
```

## Tables

```typst
#table(
  columns: (1fr, auto, auto, auto),
  align: (left, center, center, center),
  stroke: none,
  fill: (_, y) => if y == 0 { rgb("#2563EB").lighten(85%) },
  inset: 8pt,

  [*Feature*], [*Plan A*], [*Plan B*], [*Plan C*],
  [Storage],   [10 GB],    [50 GB],    [Unlimited],
  [Users],     [5],        [25],       [Unlimited],
  [Support],   [Email],    [Priority], [24/7],
  [Price],     [\$9/mo],   [\$29/mo],  [\$99/mo],
)
```

### Alternating Row Colors
```typst
fill: (_, y) => if calc.odd(y) { luma(245) }
```

## Images & Figures

```typst
#figure(
  image("chart.png", width: 80%),
  caption: [Monthly active users over time],
) <fig-users>

See @fig-users for the trend.
```

## Columns & Layout

```typst
// Two-column layout
#columns(2, gutter: 1.5em)[
  Left column content...
  #colbreak()
  Right column content...
]

// Grid for cards
#grid(
  columns: (1fr, 1fr, 1fr),
  gutter: 1em,
  rect(fill: luma(245), radius: 4pt, inset: 12pt)[*142*\ Tasks],
  rect(fill: luma(245), radius: 4pt, inset: 12pt)[*89%*\ Complete],
  rect(fill: luma(245), radius: 4pt, inset: 12pt)[*2.3s*\ Avg Time],
)
```

## Callout Boxes

```typst
#let tip(body) = block(
  fill: rgb("#DBEAFE"),
  stroke: rgb("#2563EB") + 0.5pt,
  radius: 4pt,
  inset: 12pt,
  width: 100%,
)[💡 *Tip:* #body]

#let warning(body) = block(
  fill: rgb("#FEF3C7"),
  stroke: rgb("#F59E0B") + 0.5pt,
  radius: 4pt,
  inset: 12pt,
  width: 100%,
)[⚠️ *Warning:* #body]

#tip[Use `typst watch` for live preview during editing.]
#warning[This operation cannot be undone.]
```

## Title Page

```typst
#page(margin: 0pt)[
  #rect(fill: rgb("#1E3A5F"), width: 100%, height: 100%)[
    #align(center + horizon)[
      #text(28pt, fill: white, weight: "bold")[Project Report]
      #v(0.5em)
      #text(14pt, fill: white.darken(20%))[Q1 2026 Review]
      #v(2em)
      #line(length: 30%, stroke: 1pt + white.darken(50%))
      #v(2em)
      #text(12pt, fill: white.darken(30%))[Prepared by Team Alpha]
      #v(0.3em)
      #text(10pt, fill: white.darken(40%))[#datetime.today().display("[month repr:long] [day], [year]")]
    ]
  ]
]
```

## Typst Universe Packages

Install from [typst.app/universe](https://typst.app/universe/):

```typst
#import "@preview/tablex:0.0.8": tablex     // Advanced tables
#import "@preview/cetz:0.2.0": canvas, draw // Diagrams & charts
#import "@preview/fletcher:0.4.0": *        // Flowcharts
```

**Useful packages:**
| Package | Purpose |
|---------|---------|
| `tablex` | Advanced tables with merged cells, custom borders |
| `cetz` | Charts, diagrams, plots (like TikZ for Typst) |
| `fletcher` | Flowcharts, node diagrams |
| `showybox` | Colored boxes, callouts |
| `modernpro-coverletter` | Professional cover letters |
| `charged-ieee` | IEEE paper format |

## Pandoc Integration

Convert Markdown → Typst → PDF:
```bash
pandoc input.md -o output.pdf --pdf-engine=typst
pandoc input.md -o output.typ    # generate .typ for manual tweaking
```

## Common Templates

### Report
Setup: A4, numbered headings, justified text, header/footer, TOC.

### Letter
Setup: sender info top-right, date, recipient, salutation, body, signature.

### Invoice
Setup: company header, client info, table with items/prices, total, payment terms.

### Resume
Setup: two-column grid, left sidebar (contact/skills), right main (experience/education).
