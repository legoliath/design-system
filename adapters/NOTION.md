# Notion Adapter

Notion pages optimized for **human readability**, not visual decoration.

## Page Structure — The Golden Template

Every Notion project page should follow this skeleton:

```
📌 Cover image (optional, relevant to topic)
🎯 Icon (emoji that represents the project)

# Page Title — Include the Key Point

💡 TL;DR callout (blue_background)
   → 2-3 sentences. The whole page in a nutshell.
   → A reader who stops here gets 80% of the value.

---

🟢 Status callout (green/yellow/red_background)
   → Current status + what's happening now + next deadline

## Key Decisions (or Key Findings)
   1. Decision one — **bold the answer**, then explain why
   2. Decision two — same pattern
   3. Decision three

---

## [Descriptive Section Title, Not "Details"]
   Content organized for scanning.
   Short paragraphs. Bold key terms.

▶ Toggle: Technical Details / Background / History
   Hidden by default. Open on demand.

▶ Toggle: Reference Links / Data
   Hidden by default.
```

## Callout Rules — Less Is More

Callouts are powerful BECAUSE they stand out. If everything is a callout, nothing stands out.

**Max 2-3 callouts per page.** Use them for:

| Purpose | Icon | Color | When |
|---------|------|-------|------|
| TL;DR / Summary | 💡 | `blue_background` | Every page, at the top |
| Status | 🟢/🟡/🔴 | matching bg | Project/task pages |
| Warning / Blocker | ⚠️ | `red_background` | Only when something is actually wrong |

**DON'T use callouts for:**
- Regular content → use paragraphs
- Lists of items → use bullet lists
- Every tip or note → use bold text inline
- Decoration → never

**Callout API:**
```json
{
  "type": "callout",
  "callout": {
    "icon": { "type": "emoji", "emoji": "💡" },
    "color": "blue_background",
    "rich_text": [{ "type": "text", "text": { "content": "TL;DR: The project is on track. Budget approved at $12K. Launch date: April 15." } }]
  }
}
```

## Headings — Descriptive, Not Decorative

Headings are the #1 navigation tool. Users scan them to find what they need.

```
❌ "Overview"           → ✅ "Budget: $12,400 approved for Q2"
❌ "Details"            → ✅ "Timeline: 6 weeks, launch April 15"
❌ "Technical"          → ✅ "Architecture: REST API + PostgreSQL"
❌ "Notes"              → ✅ "Open Questions (3 remaining)"
❌ "Section 3"          → ✅ "Risk: Vendor delivery may slip 2 weeks"
```

**Hierarchy:**
- **H1**: Page title only (one per page)
- **H2**: Major sections (3-6 per page max)
- **H3**: Subsections within H2 (use sparingly)

**Toggle headings** for content that most readers can skip:
```json
{
  "type": "heading_2",
  "heading_2": {
    "is_toggleable": true,
    "rich_text": [{ "type": "text", "text": { "content": "▶ Technical Architecture Details" } }]
  }
}
```

## Columns — Use Sparingly

Notion columns break reading flow, especially on mobile (they stack vertically = confusing order).

**When to use columns (max 2-3):**
- KPI metrics side by side (callout in each column)
- Short metadata pairs (left: info, right: info)
- Comparison of 2-3 options

**When NOT to use columns:**
- Body text (kills reading flow)
- More than 3 columns (unreadable on mobile)
- Nested columns (nightmare)

**KPI column recipe:**
```json
{
  "type": "column_list",
  "column_list": { "children": [
    { "type": "column", "column": { "children": [
      { "type": "callout", "callout": {
        "icon": { "type": "emoji", "emoji": "📊" },
        "color": "gray_background",
        "rich_text": [
          { "type": "text", "text": { "content": "Budget\n" }, "annotations": { "bold": false, "color": "gray" } },
          { "type": "text", "text": { "content": "$12,400" }, "annotations": { "bold": true } }
        ]
      }}
    ]}},
    { "type": "column", "column": { "children": [
      { "type": "callout", "callout": {
        "icon": { "type": "emoji", "emoji": "⏱" },
        "color": "gray_background",
        "rich_text": [
          { "type": "text", "text": { "content": "Timeline\n" }, "annotations": { "bold": false, "color": "gray" } },
          { "type": "text", "text": { "content": "6 weeks" }, "annotations": { "bold": true } }
        ]
      }}
    ]}}
  ]}
}
```

## Tables — For Structured Data Only

Tables are for comparison and structured data, not for layout.

**Good uses:**
- Feature comparison (options side by side)
- Task list with assignee + status + date
- Budget breakdown by category
- Timeline with milestones

**Table with headers:**
```json
{
  "type": "table",
  "table": {
    "table_width": 4,
    "has_column_header": true,
    "has_row_header": false,
    "children": [
      { "type": "table_row", "table_row": { "cells": [
        [{"type":"text","text":{"content":"Task"}}],
        [{"type":"text","text":{"content":"Owner"}}],
        [{"type":"text","text":{"content":"Status"}}],
        [{"type":"text","text":{"content":"Due"}}]
      ]}},
      { "type": "table_row", "table_row": { "cells": [
        [{"type":"text","text":{"content":"Finalize specs"}}],
        [{"type":"text","text":{"content":"Alice"}}],
        [{"type":"text","text":{"content":"✅ Done"}}],
        [{"type":"text","text":{"content":"Mar 10"}}]
      ]}}
    ]
  }
}
```

## Rich Text Formatting — Bold the Answer

**Within paragraphs:**
- **Bold** = the key info (name, number, decision, status)
- Regular = supporting context
- `Code` = technical terms, file names, commands
- *Italic* = almost never (poor readability)
- Color text = sparingly, for status only (red = problem, green = done)

```
❌ "After careful consideration of all available options, we decided to go with PostgreSQL."
✅ "Database: **PostgreSQL** — best fit for our read-heavy workload and JSON support."
```

## Dividers

Use dividers between major sections to create visual breathing room.

```json
{ "type": "divider", "divider": {} }
```

**When to use:**
- Between TL;DR and main content
- Between major H2 sections
- Before reference/appendix section

**When NOT to use:**
- Between every paragraph
- Between H3 subsections (spacing is enough)
- More than 4-5 per page (becomes noise)

## Progressive Disclosure in Notion

**Toggle headings** = the primary tool:

```
## Key Decisions
   Visible: the decisions themselves

▶ Background Research (toggle H2)
   Hidden: detailed analysis that led to decisions

▶ Meeting Notes Archive (toggle H2)  
   Hidden: historical discussion

▶ Reference Links (toggle H2)
   Hidden: source materials
```

**Rule: 60% visible, 40% in toggles.** The visible part should tell the complete story. Toggles add depth, not essential info.

## Page Types — Quick Recipes

### Project Page
```
🎯 Icon + Cover
# Project Name — One-Line Status
💡 TL;DR callout
---
[3-col KPI: Budget | Timeline | Status]
---
## Goals (numbered list, bold each goal)
## Current Sprint / Active Work
## Risks & Blockers
▶ Architecture / Technical Details
▶ Meeting Notes
▶ Reference
```

### Decision Document
```
⚖️ Icon
# Decision: [What We Chose]
💡 TL;DR: We chose X because Y. Alternatives were A and B.
---
## Context (2-3 short paragraphs)
## Options Considered (table: option | pros | cons | cost)
## Decision: Option B (bold the choice, explain reasoning)
## Next Steps (to-do blocks with @mentions)
▶ Detailed Analysis
```

### Meeting Notes
```
📝 Icon
# Meeting: [Topic] — [Date]
💡 TL;DR: Main decisions + action items
---
[2-col: Attendees | Date + Duration]
---
## Decisions Made (numbered)
## Action Items (to-do blocks: task + @owner + date)
▶ Full Discussion Notes
```

### Weekly Status
```
📊 Icon
# Week of [Date] — [On Track / At Risk / Blocked]
🟢/🟡/🔴 Status callout
---
[3-col KPIs]
## Highlights (bulleted, bold the achievement)
## Blockers (bulleted, bold the problem + who owns resolution)  
## Next Week (numbered priorities)
▶ Detailed Metrics
```

## Database Properties — Keep Tables Readable

**The #1 rule:** every property must be readable in a table cell without clicking.

**Property types for table columns (scanable):**
- `title` → 3-8 words max
- `select` / `multi_select` → short labels with emoji prefix
- `date` → dates are always compact
- `number` → numbers with format (currency, %)
- `url` → shows as link icon
- `files` → shows as attachment icon
- `relation` → shows linked item title
- `checkbox` → ✅ or empty

**NEVER put in a table column:**
- `rich_text` with more than 10 words → goes in the **page body**
- Long descriptions → page body
- Context, notes, conclusions → page body
- Lists of items → page body or relation

**The pattern:**
```
TABLE CELL (visible):     "Peplink BR1 Pro 5G" | 📦 Commandé | $1,500
PAGE BODY (on click):     Full description, alternatives evaluated, 
                          links, technical notes, installation guide
```

**If you need a short text column** (like "Résumé" on Decisions), keep it to ONE sentence max. Write it as a headline, not a paragraph.
