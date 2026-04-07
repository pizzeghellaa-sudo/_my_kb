---
title: Claude Code Memory System
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Claude Code has two complementary memory systems that carry knowledge across sessions. Both are loaded at the start of every conversation. Claude treats them as context, not enforced configuration. [Source: How Claude remembers your project - Claude Code Docs.url]

## Two Memory Systems

| | CLAUDE.md files | Auto memory |
|---|---|---|
| **Who writes it** | You | Claude |
| **What it contains** | Instructions and rules | Learnings and patterns |
| **Scope** | Project, user, or org | Per working tree |
| **Loaded into** | Every session | Every session (first 200 lines or 25KB of MEMORY.md) |
| **Use for** | Coding standards, workflows, project architecture | Build commands, debugging insights, preferences Claude discovers |

## CLAUDE.md Files — Four Scopes

More specific locations take precedence over broader ones:

| Scope | Location | Shared with |
|---|---|---|
| **Managed policy** | `/Library/Application Support/ClaudeCode/CLAUDE.md` (macOS) | All org users — cannot be excluded |
| **Project** | `./CLAUDE.md` or `./.claude/CLAUDE.md` | Team (via source control) |
| **User (personal)** | `~/.claude/CLAUDE.md` | Just you, all projects |
| **Local** | `./CLAUDE.local.md` | Just you, current project (gitignored) |

Files in the directory tree above the working directory all load. `CLAUDE.local.md` appends after `CLAUDE.md` at each level, so personal notes win conflicts at that scope. [Source: How Claude remembers your project - Claude Code Docs.url]

## Writing Effective Instructions

- **Size:** target under 200 lines per CLAUDE.md file (see contradiction note below)
- **Specificity:** concrete enough to verify — "Use 2-space indentation" not "Format code properly"
- **Structure:** markdown headers and bullets help Claude scan; organized sections beat dense paragraphs
- **Consistency:** contradicting rules cause arbitrary picks; audit periodically

> CONTRADICTION: [[claude-md-personal]] (from 8 Claude Code Settings to Customize in Minutes.url) says "keep personal CLAUDE.md under 50 lines." Official Claude Code docs say "target under 200 lines." The official docs may be referring to any CLAUDE.md, while the builder.io guide may be giving a more conservative personal preference recommendation. Follow the official 200-line guidance; 50-line guidance may reflect an older or stricter interpretation.

[Source: How Claude remembers your project - Claude Code Docs.url | 8 Claude Code Settings to Customize in Minutes.url]

## Import Syntax

CLAUDE.md files can pull in additional files with `@path/to/file`. Relative paths resolve from the importing file. Max depth 5 hops.

```markdown
See @README for project overview.
# Additional Instructions
- git workflow @docs/git-instructions.md
```

[Source: How Claude remembers your project - Claude Code Docs.url]

## AGENTS.md Compatibility

Claude Code reads `CLAUDE.md`, not `AGENTS.md`. If your repo uses `AGENTS.md` for other agents, create a `CLAUDE.md` that imports it: `@AGENTS.md`. Add Claude-specific instructions below the import. [Source: How Claude remembers your project - Claude Code Docs.url]

## How Files Load

Claude Code walks up the directory tree from the working directory, loading all `CLAUDE.md` and `CLAUDE.local.md` files it finds. All discovered files concatenate — they don't override each other. Subdirectory files load on demand when Claude reads files in those directories.

Use `claudeMdExcludes` in `.claude/settings.local.json` to skip specific files (e.g. other teams' instructions in a monorepo). Managed policy files cannot be excluded. [Source: How Claude remembers your project - Claude Code Docs.url]

## `/memory` Command

Run `/memory` in a session to:
- Browse all loaded CLAUDE.md, CLAUDE.local.md, and rules files
- Toggle auto memory on/off
- Open the auto memory folder
- Select any file to open in your editor

[Source: How Claude remembers your project - Claude Code Docs.url]

## Troubleshooting

- **Not following instructions:** run `/memory` to verify the file is loaded; make instructions more specific; check for conflicts
- **Instructions lost after `/compact`:** CLAUDE.md fully survives compaction (re-read from disk). If instructions disappear, they were only in conversation — write them to CLAUDE.md
- **File too large:** split into `@path` imports or `.claude/rules/` files

[Source: How Claude remembers your project - Claude Code Docs.url]

## Related Pages

- [[claude-md-personal]] — personal vs project CLAUDE.md; compliance research
- [[claude-rules]] — `.claude/rules/` for path-specific scoped instructions
- [[claude-code-memory-auto]] — auto memory details (MEMORY.md, topic files, storage)
- [[kb-architecture]] — how this KB uses CLAUDE.md as a schema file
- [[claude-code-context-management]] — what survives /compact
