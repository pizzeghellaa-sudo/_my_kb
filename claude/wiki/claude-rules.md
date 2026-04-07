---
title: Claude Code .claude/rules/ (Path-Specific Rules)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

`.claude/rules/` is a directory for organizing Claude Code instructions into modular, topic-specific files — with optional path scoping so rules only load when Claude is working with matching files. An alternative to stuffing everything into a single CLAUDE.md. [Source: How Claude remembers your project - Claude Code Docs.url]

## Structure

```
your-project/
├── .claude/
│   ├── CLAUDE.md              # Main project instructions
│   └── rules/
│       ├── code-style.md      # Loaded always
│       ├── testing.md         # Loaded always
│       ├── security.md        # Loaded always
│       └── frontend/
│           └── react.md       # Could be path-scoped to src/**/*.tsx
```

Rules without `paths` frontmatter load at launch like `.claude/CLAUDE.md`. Rules with `paths` frontmatter only load when Claude reads matching files. [Source: How Claude remembers your project - Claude Code Docs.url]

## Path-Specific Rules (YAML Frontmatter)

```markdown
---
paths:
  - "src/api/**/*.ts"
---

# API Development Rules
- All API endpoints must include input validation
- Use the standard error response format
```

Glob patterns supported:

| Pattern | Matches |
|---|---|
| `**/*.ts` | All TypeScript files |
| `src/**/*` | All files under src/ |
| `*.md` | Markdown files in project root |
| `src/**/*.{ts,tsx}` | TS and TSX files |

[Source: How Claude remembers your project - Claude Code Docs.url]

## When to Use rules/

Once your CLAUDE.md starts feeling crowded, `.claude/rules/` is the right escalation path. Split by concern: the team member who owns API conventions edits `api-conventions.md`; the person who owns testing standards edits `testing.md`. Nobody stomps on each other. [Source: Anatomy of the .claude_ folder.md]

## Difference from Skills

Rules load into context every session (or when matching files open). For task-specific instructions that don't need to be in context all the time, use [[claude-code-skills]] instead — skills only load when explicitly invoked or when Claude determines they're relevant to the prompt. [Source: How Claude remembers your project - Claude Code Docs.url]

## User-Level Rules

Personal rules in `~/.claude/rules/` apply to every project on your machine. User-level rules load before project rules (project rules have higher priority). [Source: How Claude remembers your project - Claude Code Docs.url]

## Sharing Across Projects (Symlinks)

`.claude/rules/` supports symlinks for sharing a rule set across multiple projects:

```bash
ln -s ~/shared-claude-rules .claude/rules/shared
ln -s ~/company-standards/security.md .claude/rules/security.md
```

Circular symlinks are detected and handled gracefully. [Source: How Claude remembers your project - Claude Code Docs.url]

## Related Pages

- [[claude-code-memory]] — the full memory system; rules are part of CLAUDE.md scope
- [[claude-md-personal]] — personal vs project CLAUDE.md scoping
- [[claude-code-skills]] — the on-demand alternative to always-loaded rules
