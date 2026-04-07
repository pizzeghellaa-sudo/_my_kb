---
title: CLAUDE.md — Personal vs Project
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

`CLAUDE.md` files exist at multiple scopes. Understanding the distinction between personal (global) and project-level files is critical to avoiding instruction conflicts and keeping each file focused. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Two Scopes of CLAUDE.md

| File | Scope | Who writes it |
|---|---|---|
| `~/.claude/CLAUDE.md` | **Personal global** — applies to every project | You, for your preferences |
| `<project-root>/CLAUDE.md` | **Project-level** — applies to one repo | Team, for shared conventions |

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Personal CLAUDE.md (`~/.claude/CLAUDE.md`)

The personal file is where you encode your universal preferences — tooling choices, formatting opinions, output habits that should apply everywhere:

```markdown
# Global preferences
- Use pnpm, not npm
- Prefer types over interfaces
- When writing tests, use Vitest not Jest
- Keep PR descriptions concise — summary + test plan only
```

Tell Claude: *"Create my personal CLAUDE.md at ~/.claude/CLAUDE.md. I prefer pnpm over npm, types over interfaces..."* and it creates the file. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Official Scope Hierarchy

The official Claude Code docs ([[claude-code-memory]]) document 4 CLAUDE.md scopes — the personal `~/.claude/CLAUDE.md` is the "User instructions" scope, one of four:
1. Managed policy (org-wide, cannot be excluded)
2. Project (`./CLAUDE.md` or `./.claude/CLAUDE.md`)
3. **User personal** (`~/.claude/CLAUDE.md`) — applies to all projects
4. Local (`./CLAUDE.local.md` — gitignored, current project only)

All layers load and concatenate; they don't override each other. [Source: How Claude remembers your project - Claude Code Docs.url]

## Compliance Research

Instruction compliance drops sharply with file length: [Source: 8 Claude Code Settings to Customize in Minutes.url]

- Specific, concise rules ("use pnpm, not npm"): **~89% compliance**
- Vague instructions ("write clean code"): **~35% compliance**
- Recommendation: **keep personal CLAUDE.md under 50 lines**

## Project CLAUDE.md

Generate with `/init` inside Claude Code — but trim the output heavily. The auto-generated version tends to be bloated; only keep what actually matters. For scoping rules, rules directories, and team-shared conventions, the builder.io guide on writing CLAUDE.md files is referenced as a deeper resource. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Compaction Preservation

Add directives to either CLAUDE.md to tell Claude what to preserve when `/compact` runs:

```
When compacting, always preserve:
- Current file paths being edited
- Test failure messages
- Architecture decisions made this session
```

See [[claude-code-context-management]]. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Relationship to KB Schema

In the [[llm-knowledge-base-concept]], the project-root `CLAUDE.md` serves as the **schema file** — defining workflows, conventions, and the KB's identity. This is a specific, structured use of the project-level CLAUDE.md. See [[kb-architecture]].

> Note: The personal `~/.claude/CLAUDE.md` (global preferences) is distinct from the KB schema `CLAUDE.md` (project-root workflow definition). They coexist without conflict — both are read by Claude.

## Related Pages

- [[claude-code-memory]] — official docs: full 4-scope CLAUDE.md hierarchy, loading mechanics
- [[claude-rules]] — `.claude/rules/` for path-specific, modular instructions
- [[claude-md-guide]] — builder.io guide on what to include and how to structure
- [[kb-architecture]] — how CLAUDE.md is used as a KB schema file
- [[claude-code-context-management]] — compaction preservation directives in CLAUDE.md
- [[claude-code-settings]] — overview of all 8 customizations
- [[claude-code-settings-locations]] — parallel settings.json file scopes
