# Readability — Information Architecture for Humans

Design serves comprehension. A beautiful page that hides the answer is a failed page.

Sources: Nielsen Norman Group eyetracking research, inverted pyramid, chunking theory.

## Rule #1: Conclusion First (Inverted Pyramid)

Humans don't read — they scan for the answer, then leave. Put the answer FIRST.

```
✅ Inverted Pyramid (web/docs):
   CONCLUSION / KEY FINDING
   ↓ Supporting details
   ↓ Context and background
   ↓ Deep technical details (optional)

❌ Academic style (never use for docs):
   Background and context
   ↓ Methodology
   ↓ Data and analysis
   ↓ Conclusion at the very end
```

**Every page, every section, every paragraph:** lead with the point.
- Page: TL;DR / summary at the very top
- Section: first sentence = the takeaway
- Paragraph: first sentence = topic sentence, rest = support

**Test:** If someone reads ONLY the first line of each section, do they get 80% of the value? If not, restructure.

## Rule #2: Layer-Cake Scanning (Headings ARE the Content)

NN/g eyetracking: the most effective scanning pattern is "layer-cake" — users read ONLY the headings, then dive into the section that matters to them.

**Headings must be descriptive, not decorative:**

```
❌ Bad headings (say nothing):
   "Overview"
   "Details"  
   "Section 1"
   "Notes"
   "Miscellaneous"

✅ Good headings (say the content):
   "Budget: $12,400 for 3 months"
   "Timeline: Launch by March 15"
   "Risk: Vendor may not deliver on time"
   "Decision: Go with Option B (cheaper, faster)"
   "Next steps: Alice contacts vendor Monday"
```

**Rules for headings:**
- Must be scannable in isolation — someone reading ONLY headings gets the story
- Include the key data point when possible (numbers, names, dates)
- Max 8 words — shorter is better
- Use consistent hierarchy (H1 = page topic, H2 = major sections, H3 = subsections)
- Visual distinction: bold + size difference from body text

## Rule #3: Chunking (One Idea Per Block)

The brain processes ~7 chunks at a time. Break content into small, visually distinct blocks.

**Text chunking:**
- Max 3-4 sentences per paragraph
- One idea per paragraph
- White space between chunks = visual breathing room
- Short lines: 50-75 characters (not full-width on large screens)

**Content chunking:**
- Group related items together (proximity = relationship)
- Separate unrelated items with space, dividers, or background changes
- Use bullet lists for 3+ items of the same type
- Use tables for comparisons or structured data
- Use callouts/cards for standalone pieces of information

**Number formatting:**
```
❌ 19195552743
✅ +1 (919) 555-2743

❌ $1234567.89
✅ $1,234,567.89

❌ 20250319T143022Z
✅ March 19, 2025 at 2:30 PM
```

## Rule #4: Progressive Disclosure (Show Summary, Hide Details)

Not everyone needs all the details. Show the essentials upfront, offer details on demand.

**Pattern:**
```
VISIBLE:   Summary / key decision / status
HIDDEN:    Technical details, full data, methodology, history
TRIGGER:   Toggle, accordion, link to sub-page, "Read more"
```

**In Notion:** Toggle headings are perfect for this.
**In HTML:** `<details>` / `<summary>` elements, or accordion components.

**What goes in the summary (always visible):**
- The decision / conclusion
- Status (on track / at risk / blocked)
- Key numbers
- Who owns it
- Next action + date

**What goes in the detail (hidden by default):**
- How we got there (methodology, discussion)
- Full data tables
- Historical context
- Edge cases and exceptions
- Reference links

## Rule #5: Visual Hierarchy = Information Hierarchy

The most important info should be the most visually prominent. If everything looks the same, nothing stands out.

**Prominence stack (most → least visible):**
1. Large bold text (page title, key finding)
2. Colored/tinted background blocks (callouts, status badges)
3. Bold text within a paragraph
4. Normal body text
5. Muted/grey text (metadata, timestamps, secondary info)
6. Hidden behind toggle/accordion

**Map content to prominence:**
| Content type | Visual treatment |
|-------------|-----------------|
| Key decision or conclusion | Callout block, large text, or colored badge |
| Status | Colored badge (green/yellow/red) |
| Action items | Checklist / to-do with owner name in bold |
| Deadlines | Bold + specific date (not "soon") |
| Context / background | Normal body text, or hidden in toggle |
| Reference data | Table or toggle section |
| Metadata (author, date, version) | Small, muted text |

## Rule #6: Frontload Everything

The first words of every element carry the most weight (F-pattern scanning).

```
❌ "In our recent analysis of the Q3 data, we found that revenue increased by 23%"
✅ "Revenue up 23% in Q3"

❌ "It is important to note that the deadline has been moved to Friday"
✅ "Deadline moved to Friday"

❌ Button: "Click here to download the report"
✅ Button: "Download report"
```

**Applies to:**
- Page titles
- Section headings
- First sentence of each section
- Bullet points (start with the key word)
- Button labels
- Table column headers

## Rule #7: Document Structure Template

For any project doc, proposal, or technical doc, use this structure:

```
📋 TL;DR / Executive Summary
   → 2-3 sentences maximum. The whole doc in a nutshell.
   → If they read nothing else, they get this.

🎯 Decisions / Key Points
   → Numbered list of decisions or findings.
   → Each with: what + why + who owns it.

📊 Status / Current State  
   → Visual status (badges, progress bars)
   → Key metrics or numbers

📝 Details
   → Full content, organized by topic
   → Toggle sections for deep dives
   → Tables for structured data

📎 Reference / Appendix
   → Links, source data, historical notes
   → Hidden by default (toggle or separate page)
```

## Rule #8: Tables & Databases — Scanable Cells

Table cells must be readable WITHOUT clicking or expanding.

**Good column types:** title (3-8 mots), select/tags (court + emoji), date, nombre, URL, fichier, relation, checkbox.

**Never in a column:** rich_text de plus de 10 mots. Descriptions, notes, contexte, conclusions → dans le **corps de la page** (chaque entrée est une page qu'on ouvre au clic).

```
TABLE (visible):     "Peplink BR1 Pro" | 📦 Commandé | $1,500 | Mars 15
PAGE BODY (au clic): Description complète, alternatives évaluées, 
                     notes techniques, liens, historique
```

**Si tu as besoin d'un champ texte court** (ex: "Résumé" d'une décision), max 1 phrase — écris un titre, pas un paragraphe.

## Anti-Patterns (Never Do This)

- ❌ **Wall of text** — no headings, no breaks, no visual hierarchy
- ❌ **Decorative headings** — "Overview", "Details", "Miscellaneous" (say nothing)
- ❌ **Conclusion at the bottom** — academic style in a work document
- ❌ **Everything visible** — no progressive disclosure, everything at same prominence
- ❌ **Dense tables without summary** — raw data without interpretation
- ❌ **Centered body text** — harder to scan (left-align always for body)
- ❌ **Multiple font sizes for decoration** — size = hierarchy, not aesthetics
- ❌ **Walls of callouts** — if everything is a callout, nothing stands out
- ❌ **More than 3-4 columns** — hard to read on Notion mobile, forces horizontal scrolling
- ❌ **rich_text properties in database columns** — truncated = useless. Long text goes in page body
- ❌ **Description/Notes/Context as table columns** — always page body content
