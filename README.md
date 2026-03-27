# 🎨 OpenClaw Design System

Mise en page et design de documents, pages et projets. Provides design RULES and RECIPES, NOT image generation.

![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue) ![Status](https://img.shields.io/badge/Status-Active-green)

## Overview

This design system focuses on practical, copy-paste ready recipes for creating visually stunning and well-structured documents, pages, and projects. It provides concrete rules for typography, colors, visual hierarchy, and layout patterns across various platforms, making it an invaluable tool for formatting Notion pages, building HTML dashboards, generating PDFs with Typst, and writing GitHub Markdown.

## Core Principles

1.  **Intentional Design**: Every design value is carefully considered, avoiding arbitrary numbers.
2.  **Ready-to-Use**: Provides complete, copy-paste ready solutions without placeholders.
3.  **Opinionated Defaults**: Automatically selects the best design options.
4.  **Inherent Polish**: Includes micro-interactions, shadows, and transitions as baseline.
5.  **Performance-Optimized**: Prioritizes system fonts for zero layout shift and instant rendering.

## Core Files (Design Rules)

These files encapsulate the fundamental design philosophy and modern techniques:

| File | Purpose | When to Load |
|---|---|---|
| `core/READABILITY.md` | Information architecture for human scanning, hierarchy, and structure. | **Every task** (foundational) |
| `core/TASTE.md` | Visual design tactics and rules for aesthetic appeal. | Every visual task |
| `core/MODERN-CSS.md` | Features like `clamp`, `:has`, container queries, and nesting for HTML/CSS. | Any HTML/CSS output |
| `core/POLISH.md` | Micro-interactions, shadows, transitions, and glassmorphism for refinement. | Polishing visual elements |
| `core/TOKENS.md` | Complete token system for colors, fonts, spacing, and shadows. | Building from scratch |
| `core/LAYOUT.md` | Composable layout primitives (Stack, Cluster, Grid, Sidebar) for page structure. | Page structure decisions |
| `core/AUTO-CONTEXT.md` | Auto-enriches empty headings with web-searched context. | Skeleton documents with headings only |

## Adapters (Platform-Specific Recipes)

These adapters provide full templates and execution details for specific platforms:

| Target Platform | Adapter File | Recommended Core Files to Load |
|---|---|---|
| HTML dashboard/web page | `adapters/HTML.md` | All core files |
| Notion page/database | `adapters/NOTION.md` | `TASTE` + `TOKENS` + `LAYOUT` |
| PDF report/document (Typst) | `adapters/TYPST.md` | `TASTE` + `TOKENS` |
| GitHub README/documentation | `adapters/GITHUB-MARKDOWN.md` | `TASTE` only |

## Installation

> [!NOTE]
> This design system operates as an OpenClaw skill.

Integrate the skill files into your OpenClaw workspace. The system is designed to be leveraged by an agent for formatting tasks.

## Usage

Simply instruct your OpenClaw agent to format a document, design a page, or apply specific layout rules. The agent will then consult the relevant core files and adapters to generate the desired output.

For example, to format a Notion page, the agent would load `TASTE.md`, `TOKENS.md`, and `LAYOUT.md` from the `core/` directory and apply the patterns described in `adapters/NOTION.md`.

## Configuration

Configuration is primarily driven by selecting the appropriate core design rules and platform adapters based on the task requirements. There are no external API keys or complex environment variables to manage.

## File Structure

```
.
├── README.md             (this file)
├── SKILL.md              (detailed skill description)
├── _meta.json
├── adapters/             (platform-specific recipes)
│   ├── HTML.md
│   ├── NOTION.md
│   ├── TYPST.md
│   └── GITHUB-MARKDOWN.md
└── core/                 (fundamental design rules and techniques)
    ├── AUTO-CONTEXT.md
    ├── LAYOUT.md
    ├── MODERN-CSS.md
    ├── POLISH.md
    ├── READABILITY.md
    ├── TASTE.md
    └── TOKENS.md
```

> [!TIP]
> The `core/` directory contains the foundational design knowledge, while `adapters/` provides concrete implementations for specific output formats.

