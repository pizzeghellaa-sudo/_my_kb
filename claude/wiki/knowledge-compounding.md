---
title: Knowledge Compounding
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

The core value proposition of the [[llm-knowledge-base-concept]]: knowledge accumulates and cross-references rather than resetting each session. Each new source, query, and filed answer makes the system incrementally smarter.

## The Compounding Loop

1. New source added → wiki pages created/updated with cross-references
2. Query asks a question → answer draws on accumulated connections
3. Valuable answer filed back → becomes source material for future queries
4. Next source added → connects to everything already in the wiki

Every iteration makes the next iteration more valuable. [Source: Post by God of Prompt (@godofprompt).md]

## Contrast with Non-Compounding Systems

Standard tools (ChatGPT file uploads, NotebookLM, most RAG): zero accumulation. Each session starts fresh. No connections built. No synthesis retained. [Source: Post by God of Prompt (@godofprompt).md]

LLM KB: the AI reads your sources once and the connections persist. The synthesis already reflects everything you've read.

## Timeline

- **Week 1–2:** Mostly input. Wiki grows but value isn't obvious yet.
- **After 5–10 sources:** Wiki has 15–30 interconnected pages. The system "clicks."
- **After 4–6 weeks:** You're querying a structured knowledge system that understands connections between sources better than you do. [Source: Post by God of Prompt (@godofprompt).md]

## Three Ways to Accelerate Compounding

1. **File exploration outputs back** — when the AI generates a comparison or analysis you find valuable, save it to `wiki/` or `outputs/`. [[andrej-karpathy]] says his own explorations "always add up" in the KB. [Source: Post by God of Prompt (@godofprompt).md]

2. **Add visual outputs** — have the AI render answers as markdown tables, charts, or Marp slide decks. These become reusable assets, not throwaway chat messages. [Source: Post by God of Prompt (@godofprompt).md]

3. **Version control** — initialize a git repo. Full history, branching, and the ability to undo anything the AI messes up. [Source: Post by God of Prompt (@godofprompt).md]

## The Dark Side: Error Compounding

The same loop that compounds knowledge also compounds errors. A wrong wiki page → wrong query answer → wrong filed answer → multiple pages reinforcing the same mistake. [[lint-workflow]] is the mitigation. See [[kb-limitations]] for the full risk picture. [Source: Post by God of Prompt (@godofprompt).md]

## Why Humans Abandon Wikis (And This Doesn't)

Humans abandon personal wikis because maintenance grows faster than value. LLMs don't get bored. They don't forget to update a cross-reference. They can touch 15 files in one pass without complaining. [Source: Post by God of Prompt (@godofprompt).md]

## Related Pages

- [[llm-knowledge-base-concept]] — the system this property belongs to
- [[query-workflow]] — the critical loop that feeds compounding
- [[ingest-workflow]] — the input side of the compounding loop
- [[lint-workflow]] — protecting the loop from error compounding
- [[kb-limitations]] — where compounding breaks down
