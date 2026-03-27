---
name: design-system
description: Mise en page et design de documents, pages et projets. Regles de design (typographie, couleurs, hierarchie visuelle, layout patterns) et recettes concretes par plateforme. Use when creating or formatting Notion pages (covers, icons, callouts, columns, dividers, toggle sections, synced blocks), building HTML dashboards or web pages, generating PDFs with Typst, writing GitHub Markdown (alerts, Mermaid, badges). Triggers on mise en page, layout, formatage, rendre beau, design de page, page Notion, dashboard, outils de design, belle page, projet Notion, template de page. Provides design RULES and RECIPES, NOT image generation.
metadata: {"openclaw":{"emoji":"🎨"}}
---

# Design System v2

Opinionated design system that produces **stunning** output. Not design theory — concrete, copy-paste recipes.

## Architecture

```
core/          → Design taste + modern techniques (load relevant files)
adapters/      → Platform execution with full templates (load ONE)
```

## Core Files

| File | Purpose | Load when |
|------|---------|-----------|
| `core/READABILITY.md` | Information architecture for humans — scanning, hierarchy, structure | **Every task** (this is the foundation) |
| `core/TASTE.md` | Visual design tactics — the "why it looks good" rules | Every visual task |
| `core/MODERN-CSS.md` | Modern CSS features (clamp, :has, container queries, nesting) | Any HTML/CSS output |
| `core/POLISH.md` | Micro-interactions, shadows, transitions, glassmorphism | Making things look polished |
| `core/TOKENS.md` | Colors, fonts, spacing, shadows — complete token system | Building from scratch |
| `core/LAYOUT.md` | Composable layout primitives (Stack, Cluster, Grid, Sidebar) | Page structure decisions |
| `core/AUTO-CONTEXT.md` | Auto-enrich empty headings with web-searched context | Skeleton docs with headings but no body text |

## Adapters

| Target | Adapter | Core files to load |
|--------|---------|-------------------|
| HTML dashboard/page | `adapters/HTML.md` | All core files |
| Notion page/database | `adapters/NOTION.md` | TASTE + TOKENS + LAYOUT |
| PDF report/document | `adapters/TYPST.md` | TASTE + TOKENS |
| GitHub README/docs | `adapters/GITHUB-MARKDOWN.md` | TASTE only |

## Principles

1. **Every CSS value must be intentional.** No arbitrary numbers.
2. **Copy-paste ready.** No `/* add styles here */` placeholders.
3. **Opinionated defaults.** Don't ask — pick the better option.
4. **Polish is not optional.** Transitions, shadows, hover states are baseline.
5. **System fonts first.** Zero layout shift, instant render.
