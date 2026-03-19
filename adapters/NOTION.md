# Notion Adapter

Maximize Notion's visual potential via the API. Notion is more powerful than most people realize.

## Page-Level Features

### Cover Images
Set the mood. Every important page should have a cover.
```json
{ "cover": { "type": "external", "external": { "url": "https://images.unsplash.com/photo-..." } } }
```
- Use Unsplash for free, high-quality covers
- Match the cover to the page theme (code = dark/abstract, project = team/workspace)
- Aspect: renders ~300px tall, use landscape images

### Icons
Identity at a glance. Two options:
```json
{ "icon": { "type": "emoji", "emoji": "🎯" } }
{ "icon": { "type": "external", "external": { "url": "https://..." } } }
```
- **Emoji**: quick, universal, colorful
- **Custom URL**: consistent icon sets (Notion native icons, Iconic, Phosphor)
- Pick ONE icon style per workspace for coherence

### Page Settings
- **Font style**: Default (sans), Serif (editorial), Mono (technical)
- **Full width**: ON for dashboards, OFF for long-form reading
- **Small text**: ON for dense data pages, OFF for readability

## Block Types — Full Arsenal

### Text & Structure
| Block | Design use | API type |
|-------|-----------|----------|
| Paragraph | Body text, descriptions | `paragraph` |
| Heading 1 | Page sections (max 2-3 per page) | `heading_1` |
| Heading 2 | Subsections | `heading_2` |
| Heading 3 | Groups within subsections | `heading_3` |
| Toggle heading | **Expandable sections** — hide detail, show on demand | `heading_1/2/3` + `is_toggleable: true` |
| Bulleted list | Unordered items | `bulleted_list_item` |
| Numbered list | Sequential steps | `numbered_list_item` |
| To-do | Actionable tasks | `to_do` |
| Quote | Standout text, testimonials | `quote` |
| Divider | **Visual breath** between sections | `divider` |
| Table of contents | Auto-nav for long pages | `table_of_contents` |

### 🌟 Callouts — The Most Powerful Visual Block

Callouts are Notion's secret weapon. They combine **icon + colored background + rich content**.

```json
{
  "type": "callout",
  "callout": {
    "icon": { "type": "emoji", "emoji": "💡" },
    "color": "yellow_background",
    "rich_text": [{ "type": "text", "text": { "content": "Pro tip: ..." } }],
    "children": []
  }
}
```

**Callouts support nested children!** Put lists, headings, even other callouts inside.

#### Callout Recipes
| Purpose | Icon | Color | Example |
|---------|------|-------|---------|
| Info/tip | 💡 | `blue_background` | Feature explanation |
| Success/done | ✅ | `green_background` | Completion status |
| Warning | ⚠️ | `orange_background` | Caveats, gotchas |
| Error/blocked | 🚨 | `red_background` | Blockers, failures |
| Idea/note | 📝 | `purple_background` | Brainstorm, thoughts |
| KPI/metric | 📊 | `gray_background` | Number + label |
| Quote/highlight | 💬 | `yellow_background` | Key takeaways |
| Status badge | 🟢/🟡/🔴 | matching bg | Current phase |

### Columns — Multi-Column Layouts

Create side-by-side content with `column_list` + `column` blocks.

```json
{
  "type": "column_list",
  "column_list": { "children": [
    { "type": "column", "column": { "children": [/* blocks */] } },
    { "type": "column", "column": { "children": [/* blocks */] } },
    { "type": "column", "column": { "children": [/* blocks */] } }
  ]}
}
```

- **2 columns**: sidebar + content, comparison
- **3 columns**: KPI cards, feature highlights
- **4+ columns**: use sparingly, gets cramped on mobile
- Columns can contain ANY block type (callouts, images, lists, toggles)

### Media & Embeds
| Block | Use for | API type |
|-------|---------|----------|
| Image | Screenshots, diagrams, photos | `image` (URL or upload) |
| Video | Tutorials, demos | `video` (YouTube, Vimeo, URL) |
| Bookmark | **Rich link previews** with thumbnail | `bookmark` |
| Embed | Figma, Loom, Maps, Typeform, Miro, CodePen | `embed` |
| File | Downloadable attachments | `file` |
| PDF | Inline PDF viewer | `pdf` |
| Code | **Syntax-highlighted** snippets (50+ languages) | `code` |
| Equation | Math formulas (KaTeX) | `equation` |

### Synced Blocks — Reusable Components

Create once, use everywhere. Edit in one place, updates everywhere.

```json
{
  "type": "synced_block",
  "synced_block": {
    "synced_from": null,
    "children": [/* original content */]
  }
}
```

Reference an existing synced block:
```json
{
  "type": "synced_block",
  "synced_block": {
    "synced_from": { "type": "block_id", "block_id": "original-block-id" }
  }
}
```

Use for: headers, footers, navigation bars, status legends, recurring callouts.

### Tables

```json
{
  "type": "table",
  "table": {
    "table_width": 3,
    "has_column_header": true,
    "has_row_header": false,
    "children": [
      { "type": "table_row", "table_row": { "cells": [[/*rich text*/], [/*...*/], [/*...*/]] } }
    ]
  }
}
```

- Use `has_column_header: true` for visual distinction
- Tables support rich text in cells (bold, color, links)

## Rich Text Formatting

Every text block supports annotations:
```json
{
  "type": "text",
  "text": { "content": "important", "link": null },
  "annotations": {
    "bold": true,
    "italic": false,
    "strikethrough": false,
    "underline": false,
    "code": false,
    "color": "red"
  }
}
```

### Available Colors
**Text**: `default`, `gray`, `brown`, `orange`, `yellow`, `green`, `blue`, `purple`, `pink`, `red`
**Background**: same names + `_background` suffix

### Inline Elements
- **@mentions**: link to pages or users
- **Dates**: formatted date ranges
- **Links**: clickable URLs
- **Inline code**: for technical terms
- **Equations**: inline KaTeX math

## Design Recipes

### Project Dashboard
1. Cover: relevant Unsplash image
2. Icon: project emoji
3. Callout (`green_background`): current status + phase
4. Divider
5. Column list (3 cols): KPI callouts with 📊 + bold number + gray label
6. Divider
7. H2: "Active Work"
8. Linked database view (table or board)
9. H2: "Recent Updates"
10. Timeline using dated callouts
11. Toggle H2: "Resources" — links, docs, references
12. Toggle H2: "Archive"

### Documentation Page
1. Icon: 📖
2. Table of contents block
3. Callout (`blue_background`): page purpose / TL;DR
4. Divider
5. H2 sections with content
6. Callouts for tips (💡), warnings (⚠️)
7. Code blocks with language specified
8. Toggle sections for detailed examples

### Meeting Notes
1. Icon: 🤝
2. Column list (2 cols):
   - Left: Callout with 👥 attendees
   - Right: Callout with 📅 date + ⏱ duration
3. Divider
4. H2: "Agenda" — numbered list
5. H2: "Notes" — bulleted list
6. H2: "Action Items" — to_do blocks with @mentions
7. Toggle H2: "Previous Meeting" — synced block or link

### Weekly Report
1. Cover: team/project themed
2. Callout (`green_background`): 🟢 "On Track" or 🟡 "At Risk"
3. Column list (3-4 cols): KPI callouts
4. H2: "Highlights" — callout per highlight with ✅ icon
5. H2: "Challenges" — callout per challenge with ⚠️ icon
6. H2: "Next Week" — numbered list of priorities
7. Table: detailed metrics
