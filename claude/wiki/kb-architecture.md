---
title: KB Architecture (Folder Structure & Schema)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 2
status: draft
---

The physical and conceptual structure of an [[llm-knowledge-base-concept]]: three folders, one schema file, no special software or infrastructure required.

## Folder Structure

```
my-knowledge-base/
├── raw/           # Source material. AI reads but NEVER modifies.
│   └── assets/    # Images, screenshots, diagrams
├── wiki/          # AI-maintained wiki. You read. AI writes.
├── outputs/       # Reports, analyses, answers from queries
└── CLAUDE.md      # Schema file — the rules the AI follows
```

[Source: Post by God of Prompt (@godofprompt).md]

## The Schema File (CLAUDE.md)

The schema is what separates a disciplined wiki maintainer from a generic chatbot. It tells the AI: what the knowledge base is about, how to organize it, and exactly what to do when processing sources, answering questions, or running maintenance. [Source: Post by God of Prompt (@godofprompt).md]

Key sections of a production schema:
- **Identity** — topic and ownership model (human curates, AI maintains)
- **Architecture** — folder roles and access rules
- **Wiki Conventions** — YAML frontmatter format, internal link syntax `[[topic]]`, citation format `[Source: file]`, contradiction flagging
- **Index and Log** — `wiki/index.md` (all pages) and `wiki/log.md` (append-only history)
- **Ingest Workflow** — step-by-step instructions for processing a new source
- **Query Workflow** — how to answer questions from the wiki
- **Lint Workflow** — monthly health check procedure
- **Focus Areas** — 3-5 topics the KB covers

## Wiki File Conventions

Every wiki page uses YAML frontmatter:
```yaml
---
title: [Topic Name]
created: [Date]
last_updated: [Date]
source_count: [Number of raw sources that informed this page]
status: [draft | reviewed | needs_update]
---
```

- Internal links: `[[topic-name]]`
- Source citations: `[Source: filename.md]`
- Contradiction flags: `> CONTRADICTION: [old claim] vs [new claim] from [source]`

[Source: Post by God of Prompt (@godofprompt).md]

## Personal vs Project CLAUDE.md

The KB schema uses the project-root `CLAUDE.md`. But Claude Code also supports a **personal** `~/.claude/CLAUDE.md` that applies globally across all projects. These two files coexist:

- `~/.claude/CLAUDE.md` — your universal personal preferences (tooling, formatting style, habits)
- `<project-root>/CLAUDE.md` — the KB schema (workflows, conventions, identity)

Both are read by Claude; neither overrides the other. See [[claude-md-personal]] for detail on compliance research and best practices. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Design Principles

- **raw/ is immutable** — the AI reads but never modifies source files
- **wiki/ is AI-owned** — the AI writes; the human reads and guides
- **No infrastructure** — no database, no vector store, no embeddings; plain markdown files
- **Schema-driven** — the CLAUDE.md file is the single source of behavioral truth

## Related Pages

- [[llm-knowledge-base-concept]] — why this architecture exists
- [[ingest-workflow]] — how sources enter the system
- [[query-workflow]] — how the wiki is queried
- [[lint-workflow]] — how the wiki is maintained
- [[kb-limitations]] — scale limits of this flat-file approach
- [[claude-md-personal]] — personal vs project CLAUDE.md scopes
- [[claude-code-settings-locations]] — parallel concept: settings.json scopes in Claude Code
