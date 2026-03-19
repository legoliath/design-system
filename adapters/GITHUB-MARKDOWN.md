# GitHub Markdown Adapter

Maximize GitHub Flavored Markdown for visually rich READMEs, docs, and issues.

## Alerts (Admonitions)

Five built-in alert types with automatic styling:

```markdown
> [!NOTE]
> Useful information that users should know.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.
```

| Alert | Color | Use for |
|-------|-------|---------|
| NOTE | Blue | Context, background info |
| TIP | Green | Best practices, shortcuts |
| IMPORTANT | Purple | Must-know information |
| WARNING | Yellow | Pitfalls, common mistakes |
| CAUTION | Red | Destructive actions, breaking changes |

## Mermaid Diagrams

Rendered natively by GitHub. Wrap in ` ```mermaid ` code blocks.

### Flowchart
````markdown
```mermaid
flowchart LR
    A[Input] --> B{Valid?}
    B -->|Yes| C[Process]
    B -->|No| D[Error]
    C --> E[Output]
```
````

### Sequence Diagram
````markdown
```mermaid
sequenceDiagram
    User->>API: Request
    API->>DB: Query
    DB-->>API: Results
    API-->>User: Response
```
````

### Gantt Chart
````markdown
```mermaid
gantt
    title Project Timeline
    dateFormat YYYY-MM-DD
    section Phase 1
    Research    :a1, 2026-01-01, 30d
    Design      :a2, after a1, 20d
    section Phase 2
    Build       :b1, after a2, 45d
    Test        :b2, after b1, 15d
```
````

### Pie Chart
````markdown
```mermaid
pie title Budget Allocation
    "Engineering" : 45
    "Marketing" : 25
    "Operations" : 20
    "Other" : 10
```
````

## Math (KaTeX)

```markdown
Inline: $E = mc^2$

Block:
$$
\sum_{i=1}^{n} x_i = x_1 + x_2 + \cdots + x_n
$$
```

## Tables

```markdown
| Feature | Status | Priority |
|:--------|:------:|----------:|
| Auth    | ✅ Done | High     |
| API     | 🔄 WIP | High     |
| Docs    | ❌ TODO | Medium   |
```

- `:---` left, `:---:` center, `---:` right
- Use emoji for visual status (✅ ❌ 🔄 ⚠️ 🟢 🟡 🔴)

## Badges (shields.io)

```markdown
![Build](https://img.shields.io/badge/build-passing-brightgreen)
![Version](https://img.shields.io/badge/version-2.1.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-beta-orange)
```

**Dynamic badges:**
```markdown
![GitHub stars](https://img.shields.io/github/stars/user/repo)
![npm](https://img.shields.io/npm/v/package)
![CI](https://img.shields.io/github/actions/workflow/status/user/repo/ci.yml)
```

Group badges on one line for a clean header:
```markdown
[![Build](...)](#) [![Version](...)](#) [![License](...)](#)
```

## HTML Elements (Allowed in GitHub Markdown)

### Collapsible Sections
```html
<details>
<summary><strong>Click to expand</strong></summary>

Content here (leave blank line after summary tag).

- Supports full Markdown inside
- Including code blocks

</details>
```

### Keyboard Shortcuts
```html
Press <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> to open.
```

### Superscript / Subscript
```html
H<sub>2</sub>O is water. E = mc<sup>2</sup>.
```

### Image Sizing
```html
<img src="screenshot.png" width="500" alt="Screenshot">
```

### Centered Content
```html
<div align="center">
  <img src="logo.png" width="200">
  <h3>Project Name</h3>
  <p>Short description of the project.</p>
</div>
```

### Picture (Light/Dark Mode)
```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="logo-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="logo-light.png">
  <img alt="Logo" src="logo-light.png" width="200">
</picture>
```

## Task Lists
```markdown
- [x] Completed task
- [ ] Pending task
- [ ] Another task
```

## Footnotes
```markdown
This needs clarification[^1].

[^1]: Here's the detailed explanation.
```

## README Structure Pattern

```markdown
<div align="center">
  <img src="logo.png" width="120">
  <h1>Project Name</h1>
  <p>One-line description</p>

  [![Build](badge)](#) [![License](badge)](#) [![Version](badge)](#)
</div>

---

## ✨ Features

- **Feature 1** — Short description
- **Feature 2** — Short description

## 🚀 Quick Start

\`\`\`bash
npm install package
\`\`\`

## 📖 Documentation

> [!TIP]
> Start with the [Getting Started guide](link).

## 🗺️ Architecture

\`\`\`mermaid
flowchart LR
  A --> B --> C
\`\`\`

<details>
<summary>📋 Full API Reference</summary>
...detailed content...
</details>

## 📄 License

MIT
```
