---
name: design-system
description: >
  Modular design system that gives AI agents visual design taste for creating beautiful documents,
  pages, and layouts across multiple platforms. Use when: (1) creating or formatting Notion pages
  with visual impact (covers, icons, callouts, columns, colors), (2) building HTML dashboards or
  web pages with modern CSS, (3) generating professional PDFs with Typst, (4) writing visually
  rich GitHub Markdown (alerts, Mermaid diagrams, badges). Triggers on requests involving layout,
  formatting, visual design, making things "look good", page aesthetics, document styling,
  dashboards, or any mention of visual presentation quality. NOT for: pure content writing
  without visual concerns, data processing, or backend code.
---

# Design System

Modular skill: **core** (design taste) + **adapters** (platform execution).

## Architecture

```
core/          → Universal design rules (always load relevant files)
adapters/      → Platform-specific execution (load ONE per task)
tokens/        → Semantic design tokens (load when building from scratch)
```

## Routing

Detect the target platform, then load:

1. **Always**: relevant `core/` files for the task
2. **One adapter**: based on output target

| Target | Adapter | Core files to load |
|--------|---------|-------------------|
| Notion page/database | `adapters/NOTION.md` | DESIGN-PRINCIPLES + COLOR + LAYOUT-PATTERNS |
| HTML dashboard/page | `adapters/HTML.md` | All core files |
| PDF report/document | `adapters/TYPST.md` | DESIGN-PRINCIPLES + TYPOGRAPHY + LAYOUT-PATTERNS |
| GitHub README/docs | `adapters/GITHUB-MARKDOWN.md` | DESIGN-PRINCIPLES + TYPOGRAPHY |

## Core Files

| File | Load when |
|------|-----------|
| `core/DESIGN-PRINCIPLES.md` | Every visual task |
| `core/TYPOGRAPHY.md` | Text-heavy output, PDFs, web pages |
| `core/COLOR.md` | Choosing colors, palettes, theming |
| `core/LAYOUT-PATTERNS.md` | Page structure, dashboards, multi-section layouts |

## Design Tokens

Load `tokens/tokens.json` when building from scratch and needing consistent values (colors, spacing, sizing). Tokens use semantic names with descriptions — use the description to pick the right token.

## Principles

- **Beauty serves clarity.** Decoration without purpose is noise.
- **Maximize platform potential.** Use every feature available, not just the basics.
- **Consistency > novelty.** Reuse patterns, colors, spacing across a project.
- **The squint test.** If you blur the page, structure should still be visible.
