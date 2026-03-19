# Layout Patterns

Reusable visual patterns. Pick the right one for the content type.

## Hero Section

Opening section that sets the tone. Use for project pages, dashboards, landing pages.

```
┌─────────────────────────────────────────────┐
│            [COVER IMAGE/BANNER]             │
│                                             │
│  🎯  Page Title                             │
│      Subtitle or short description          │
│                                             │
│  [Status Badge]  [Date]  [Owner]            │
└─────────────────────────────────────────────┘
```

**Notion:** Cover image + Icon + H1 + paragraph + callout for status.
**HTML:** Full-width header with background image/gradient + overlay text.
**Typst:** Title page with centered text + decorative line.

## Metrics / KPI Cards

Display 3-5 key numbers at a glance. Use for dashboards, reports, status pages.

```
┌───────────┐  ┌───────────┐  ┌───────────┐
│  📊 142   │  │  ✅ 89%   │  │  ⚡ 2.3s  │
│  Tasks    │  │  Complete  │  │  Avg Time │
└───────────┘  └───────────┘  └───────────┘
```

**Notion:** Column list with 3 columns, each containing a callout (icon + number + label).
**HTML:** CSS Grid `grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))`.
**Markdown:** Table row with bold numbers.

## Sidebar + Content

Main content with navigation or metadata alongside. Use for documentation, wiki pages.

```
┌──────────┬──────────────────────────────┐
│ 📑 Nav   │                              │
│          │  Content Area                │
│ • Item 1 │                              │
│ • Item 2 │  Text, images, tables...     │
│ • Item 3 │                              │
│          │                              │
└──────────┴──────────────────────────────┘
```

**Notion:** Two columns (narrow left, wide right). Left = linked page list or TOC.
**HTML:** CSS Grid `grid-template-columns: 250px 1fr`.

## Sections with Dividers

Clean separation between content groups. Use for reports, long documents.

```
┌─────────────────────────────────────────────┐
│  ## Section Title                           │
│  Content content content...                 │
│                                             │
│  ─────────────────────────────────────────  │
│                                             │
│  ## Next Section                            │
│  More content...                            │
└─────────────────────────────────────────────┘
```

**Notion:** H2 + content + divider block. Use toggle headings for expandable sections.
**Markdown:** `---` horizontal rule.

## Timeline / Changelog

Sequential events ordered by time. Use for project updates, release notes.

```
┌─────────────────────────────────────────────┐
│  🟢 Mar 18 — Feature X shipped             │
│     Details about the release...            │
│                                             │
│  🟡 Mar 15 — Bug Y discovered              │
│     Impact assessment...                    │
│                                             │
│  🔵 Mar 10 — Sprint started                │
│     Goals for this sprint...                │
└─────────────────────────────────────────────┘
```

**Notion:** Callouts with colored icons per status + date in bold.
**HTML:** Vertical line with positioned cards (CSS `border-left` + offset blocks).
**Markdown:** Bold date + nested content. Mermaid `gantt` for visual timelines.

## Dashboard Layout

Overview page combining multiple patterns. Use for project home, team hub.

```
┌─────────────────────────────────────────────┐
│  [HERO: Cover + Title + Status Callout]     │
├───────────┬───────────┬─────────────────────┤
│  📊 KPI   │  📊 KPI   │  📊 KPI             │
├───────────┴───────────┴─────────────────────┤
│  ## Active Tasks          │  ## Recent       │
│  • Task 1 — @owner        │  • Update 1     │
│  • Task 2 — @owner        │  • Update 2     │
├───────────────────────────┴─────────────────┤
│  ▶ Archived (toggle)                        │
│  ▶ Resources (toggle)                       │
└─────────────────────────────────────────────┘
```

**Notion recipe:**
1. Cover image (relevant to project)
2. Icon (emoji or custom)
3. H1 title
4. Callout: status/phase with colored background
5. Column list (3 cols): KPI callouts with emoji + bold number
6. Divider
7. Two columns: linked database (active tasks) + recent updates
8. Toggle headings for archived/reference content

## Comparison / Feature Matrix

Side-by-side comparison. Use for tool evaluation, feature lists.

```
┌──────────┬─────────┬─────────┬─────────┐
│ Feature  │  Opt A  │  Opt B  │  Opt C  │
├──────────┼─────────┼─────────┼─────────┤
│ Speed    │  ✅ Fast │  ⚠️ Med  │  ❌ Slow │
│ Cost     │  $10    │  $25    │  $5     │
│ Support  │  ✅     │  ✅     │  ❌     │
└──────────┴─────────┴─────────┴─────────┘
```

**Notion:** Table block with emoji indicators.
**Markdown:** GFM table with emoji status.
**HTML:** Styled `<table>` with status colors.

## Pattern Selection Guide

| Content type | Best pattern |
|-------------|-------------|
| Project overview | Dashboard Layout |
| Status update | Hero + KPI Cards + Timeline |
| Documentation | Sidebar + Content |
| Report | Sections with Dividers |
| Comparison | Feature Matrix |
| Changelog | Timeline |
| Landing page | Hero + Sections |
