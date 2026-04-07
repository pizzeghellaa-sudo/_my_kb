---
title: Claude Code Auto Memory
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Auto memory lets Claude accumulate knowledge across sessions without you writing anything. Claude saves notes for itself as it works — build commands, debugging insights, architecture notes, code style preferences, workflow habits. Requires Claude Code v2.1.59+. [Source: How Claude remembers your project - Claude Code Docs.url]

## How It Works

Claude decides what's worth remembering based on whether information would be useful in a future conversation. It doesn't save something every session. When you see "Writing memory" or "Recalled memory" in the interface, Claude is actively updating or reading from the memory directory.

The **first 200 lines of `MEMORY.md`** (or 25KB, whichever comes first) load at the start of every conversation. Content beyond that threshold is not loaded at session start. Claude keeps `MEMORY.md` concise by moving detailed notes to separate topic files, which load on demand. [Source: How Claude remembers your project - Claude Code Docs.url]

## Storage Structure

```
~/.claude/projects/<project>/memory/
├── MEMORY.md          # Concise index — loaded every session (first 200 lines)
├── debugging.md       # Detailed notes on debugging patterns (on-demand)
├── api-conventions.md # API design decisions (on-demand)
└── ...                # Other topic files Claude creates
```

- `<project>` path is derived from the git repository
- All worktrees and subdirectories within the same repo share one auto memory directory
- Machine-local — not shared across machines or cloud environments

[Source: How Claude remembers your project - Claude Code Docs.url]

## Enable / Disable

Auto memory is on by default. Toggle via `/memory` or via settings:

```json
{ "autoMemoryEnabled": false }
```

Or set `CLAUDE_CODE_DISABLE_AUTO_MEMORY=1` as an env var.

Custom storage location: set `autoMemoryDirectory` in user or local settings (not project settings — to prevent shared projects redirecting writes to sensitive locations). [Source: How Claude remembers your project - Claude Code Docs.url]

## Editing Auto Memory

All auto memory files are plain markdown you can edit or delete at any time. Run `/memory` to browse and open them from within a session. Ask Claude to remember something verbally ("always use pnpm, not npm") and it saves to auto memory. To save to CLAUDE.md instead, say "add this to CLAUDE.md." [Source: How Claude remembers your project - Claude Code Docs.url]

## Subagents

Subagents can maintain their own auto memory. See subagent configuration in Claude Code docs for details. [Source: How Claude remembers your project - Claude Code Docs.url]

## Relationship to This KB's Memory System

This KB uses a structurally similar pattern: `MEMORY.md` as an index with linked topic files — inspired by the same principle that an LLM needs a lightweight entry point to a larger knowledge store. The auto memory system is essentially Claude Code's built-in implementation of what this KB builds manually. See [[llm-knowledge-base-concept]].

## Related Pages

- [[claude-code-memory]] — the full memory system (CLAUDE.md + auto memory together)
- [[claude-rules]] — path-specific rules as an alternative to large CLAUDE.md files
- [[llm-knowledge-base-concept]] — the broader pattern auto memory implements
