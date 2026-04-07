---
title: Query Workflow
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

The process for asking questions against the wiki and filing valuable answers back in. Part of the [[llm-knowledge-base-concept]] system; becomes useful after ~10 wiki pages are built via [[ingest-workflow]].

## Query Steps

1. Read `wiki/index.md` first to find relevant pages
2. Read all relevant wiki pages
3. Synthesize answer with `[Source: page-name]` citations
4. If answer reveals new insights, offer to file it back into `wiki/`
5. Save valuable answers to `outputs/`

[Source: Post by God of Prompt (@godofprompt).md]

## Query Prompt (Copy-Paste)

```
"Read wiki/index.md. Answer: [QUESTION]. Cite wiki pages. If this answer is worth preserving, offer to file it as a new wiki page."
```

[Source: Post by God of Prompt (@godofprompt).md]

## High-Value Query Types

Questions that extract the most value from the KB: [Source: Post by God of Prompt (@godofprompt).md]

- "What are the three biggest gaps in this knowledge base?"
- "Which sources disagree with each other, and on what?"
- "What should I research next based on what's here?"
- "Write a 500-word briefing on [topic] using only wiki content"
- "What connections exist between [concept A] and [concept B]?"

## The Critical Loop

Good answers should be filed back into the wiki. A comparison, an analysis, a discovered connection — these compound in the knowledge base just like ingested sources do. Every question makes the next answer better. See [[knowledge-compounding]]. [Source: Post by God of Prompt (@godofprompt).md]

## Specialized Query Prompts

**Explore (find hidden connections):**
```
"Read wiki/index.md and identify the 5 most interesting unexplored connections between existing topics. For each, explain what insight it might reveal and what source would help confirm it."
```

**Brief (executive summary):**
```
"Based on everything in wiki/, write a 500-word executive briefing on [TOPIC]. Cite sources. Structure it as: current state, key tensions, open questions, recommended next steps."
```

[Source: Post by God of Prompt (@godofprompt).md]

## Related Pages

- [[ingest-workflow]] — prerequisite; build the wiki before querying
- [[knowledge-compounding]] — why filing answers back matters
- [[lint-workflow]] — what to do when query answers start feeling stale
- [[kb-limitations]] — "lost in the middle" effects and hallucination risks in query results
