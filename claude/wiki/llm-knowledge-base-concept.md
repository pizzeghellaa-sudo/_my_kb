---
title: LLM Knowledge Base Concept
created: 2026-04-07
last_updated: 2026-04-07
source_count: 2
status: draft
---

A personal knowledge base where an LLM reads source documents once and compiles a structured, interlinked wiki — so knowledge accumulates across sessions instead of resetting each time. Originated by Andrej Karpathy and popularized via a viral GitHub Gist in April 2026.

## Origin

[[andrej-karpathy]] posted about this pattern on April 2, 2026. The GitHub Gist reached 5,000+ stars and 1,400+ forks within two days. [[god-of-prompt]] published a detailed breakdown with copy-paste prompts for every step. [Source: Post by God of Prompt (@godofprompt).md]

## The Core Problem It Solves

Standard AI tools (ChatGPT file uploads, NotebookLM, most RAG systems) start from zero every session. You upload docs, ask a question, get an answer — and the next session it's forgotten everything. Knowledge never accumulates. [Source: Post by God of Prompt (@godofprompt).md]

The LLM KB flips this: the AI reads your sources once and compiles a structured wiki with summaries, cross-references, and flagged contradictions. Subsequent queries read the wiki, not the raw files. The connections are already there. [Source: Post by God of Prompt (@godofprompt).md]

## Division of Labor

> "The human's job is to curate sources, direct the analysis, ask good questions, and think about what it all means. The LLM's job is everything else." — Andrej Karpathy [Source: Post by God of Prompt (@godofprompt).md]

## Karpathy's Result

~100 articles, ~400,000 words on a single research topic. No database. No embeddings. No vector store. Just folders and markdown files. [Source: Post by God of Prompt (@godofprompt).md]

## Recommended Tooling

Any AI coding agent that reads local files works. Specifically recommended: Claude Code, Cursor, Codex. Claude Code is the most natural fit given this KB's schema uses `CLAUDE.md`. See [[claude-code-settings]] for Claude Code customizations that improve the KB workflow (auto-compact thresholds, hooks, status line). [Source: Post by God of Prompt (@godofprompt).md]

## Key Properties

- **Accumulation over reset** — every new source makes the wiki richer
- **Compounding** — every query can be filed back in, making the next answer better (see [[knowledge-compounding]])
- **No infrastructure** — markdown files in a folder; no vector store, no database
- **Schema-driven** — a `CLAUDE.md` file defines the rules the AI follows (see [[kb-architecture]])

## Related Pages

- [[kb-architecture]] — folder structure and schema
- [[ingest-workflow]] — how sources are processed
- [[query-workflow]] — how to query the wiki
- [[lint-workflow]] — monthly health checks
- [[knowledge-compounding]] — why the system gets smarter over time
- [[kb-limitations]] — where this system breaks
- [[kb-use-cases]] — who benefits and how
- [[prompt-library]] — copy-paste prompts for every step
- [[claude-code-settings]] — Claude Code customizations that improve the KB workflow
