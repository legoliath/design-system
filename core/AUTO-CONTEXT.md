# Auto-Context — Content Enrichment for Headings

## Purpose
Transform a skeleton of headings into a rich document by auto-generating contextual introductions via web search.

## When to Activate
- **Explicit flag:** User says "enrichir", "ajouter du contexte", "remplir les sections", or similar
- **Auto-detect:** Document has 3+ headings with no body text (or only placeholder text like "TODO", "…", "TBD")
- **Never:** When the user provides full content under each heading — don't overwrite

## Process

### 1. Detect empty headings
Scan the document structure. For each heading (H1–H3) with no meaningful body text beneath it:
- Add to enrichment queue
- Skip headings that are structural (e.g., "Table of Contents", "References", "Appendix")

### 2. Web search (batched)
For each heading in the queue:
```
web_search("{heading text} overview summary")
```

**Limits:**
- Max **8 searches** per document (avoid token burn)
- If > 8 empty headings, prioritize H1 > H2 > H3, then first-come
- Skip generic headings ("Introduction", "Conclusion") — write those from document context instead

### 3. Synthesize intro paragraph
From search results, write **2–4 sentences** that:
- Define/contextualize the topic for the document's audience
- Are factual and current (prefer recent sources)
- Flow naturally as an introduction to the section
- **Never** include citations or URLs inline (this is body text, not a report)

### 4. Insert and format
Place the generated paragraph directly under the heading, before any existing sub-content.

## Style Rules

| Rule | Example |
|------|---------|
| **Concise** — no filler, no "In today's world…" | ✅ "Kubernetes orchestrates containerized workloads across clusters." |
| **Factual tone** — informative, not promotional | ❌ "Kubernetes is an amazing tool that revolutionizes…" |
| **Match document register** — formal doc → formal text, casual page → casual text | Adapt to surrounding content |
| **Present tense** — unless historical context required | ✅ "GraphQL provides…" not "GraphQL has provided…" |
| **No redundancy with heading** — don't restate the title | ❌ "## Docker \n Docker is Docker…" |

## Integration with Design Flow

Auto-context runs **before** design/formatting:
1. Receive skeleton → **Auto-Context enrichment**
2. Enriched document → Apply design adapter (HTML, Notion, Typst, etc.)
3. Final output with both content and polish

## Opt-out
If a heading has a comment `<!-- no-enrich -->` or the user specifies sections to skip, leave them empty.

## Example

**Input:**
```markdown
# Cloud Native Architecture

## Containers

## Service Mesh

## Observability
```

**After enrichment:**
```markdown
# Cloud Native Architecture

Cloud native architecture designs applications as loosely coupled microservices, packaged in containers, orchestrated dynamically, and managed through automation. This approach maximizes resilience, scalability, and velocity of deployment.

## Containers

Containers package an application with its dependencies into a standardized unit for deployment. Unlike virtual machines, they share the host OS kernel, making them lightweight and fast to start — typically in milliseconds.

## Service Mesh

A service mesh manages communication between microservices through a dedicated infrastructure layer, typically implemented as sidecar proxies. It handles load balancing, encryption, authentication, and observability without requiring changes to application code.

## Observability

Observability combines metrics, logs, and distributed traces to provide insight into system behavior. It goes beyond traditional monitoring by enabling teams to ask arbitrary questions about their systems without deploying new instrumentation.
```
