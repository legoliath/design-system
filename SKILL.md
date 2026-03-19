---
name: design-system
description: >
  Mise en page et design de documents, pages, et projets. Contient les règles de design (typographie,
  couleurs, hiérarchie visuelle, layout patterns) et des recettes concrètes par plateforme.
  Use when: (1) mise en page Notion — covers, icons, callouts colorés, columns, dividers, toggle
  sections, synced blocks, (2) mise en page HTML — dashboards, pages web, CSS moderne, (3) mise en
  page PDF via Typst — rapports, factures, documents pro, (4) mise en page GitHub Markdown — README,
  docs, alerts, Mermaid, badges. Triggers: mise en page, layout, formatage, formater une page,
  structurer une page, rendre beau, design de page, page Notion, dashboard, présentation visuelle,
  structure de document, template de page, améliorer le look, page de projet. Ce skill fournit des
  RÈGLES et RECETTES de design, PAS de la génération d'images. NOT for: génération d'images (utiliser
  nano-banana-pro ou wan), contenu texte sans souci visuel, backend code.
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
