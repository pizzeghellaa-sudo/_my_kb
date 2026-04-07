---
title: Ingest Workflow
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

The process by which a new raw source document is read, summarized, and integrated into the wiki. Defined in the KB's `CLAUDE.md` schema. Part of the [[llm-knowledge-base-concept]] system.

## Standard Ingest Steps

1. Read the full source document
2. Discuss key takeaways with the user
3. Create or update a summary page in `wiki/`
4. Update `wiki/index.md`
5. Update ALL relevant entity and concept pages across the wiki
6. Add backlinks from existing pages to new content
7. Flag any contradictions with existing wiki content
8. Append entry to `wiki/log.md`
9. A single source should touch **10–15 wiki pages**

[Source: Post by God of Prompt (@godofprompt).md]

## Ingest Prompt (Copy-Paste)

**Single source (supervised):**
```
"Read the schema in CLAUDE.md. Process [FILENAME] from raw/. Read it fully, discuss key takeaways with me, then: create summary page, update index, update all relevant pages, add backlinks, flag contradictions, log the ingest."
```

**Batch (less supervised):**
```
"Read CLAUDE.md. Process all unprocessed files in raw/ sequentially. For each: create summary, update index, update relevant pages, log the ingest. Proceed automatically."
```

[Source: Post by God of Prompt (@godofprompt).md]

## Best Practices

- **Process one source at a time** — [[andrej-karpathy]] does the same. Read summaries, check updates, guide the AI on what to emphasize. Produces dramatically better results than batch-processing. [Source: Post by God of Prompt (@godofprompt).md]
- **Start with raw/ dump, no organizing** — don't rename, clean up, or sort. Volume over perfection. The AI's job is to organize.
- **Use Obsidian Web Clipper** — converts web articles to markdown in one click; hotkey to pull images locally for AI reference. [Source: Post by God of Prompt (@godofprompt).md]
- After 5–10 sources, the wiki will have an index, a log, and 15–30 interconnected pages — that's when the system "clicks." [Source: Post by God of Prompt (@godofprompt).md]

## Related Pages

- [[kb-architecture]] — the folder structure sources are dropped into
- [[query-workflow]] — what happens after enough sources are ingested
- [[lint-workflow]] — maintenance after many ingests
- [[knowledge-compounding]] — why per-source ingests compound over time
- [[kb-limitations]] — error compounding risk introduced at ingest time
