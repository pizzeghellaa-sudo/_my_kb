---
title: Anatomy of the .claude/ Folder
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

The `.claude/` folder is the control center for how Claude Code behaves in a project. It holds instructions, custom commands, permission rules, reusable skills, and subagent personas. Understanding every subfolder turns Claude Code from a generic AI assistant into a fully configured team tool. [Source: Anatomy of the .claude_ folder.md]

## Two Directories, Not One

There are two `.claude/` directories:

| Directory | Purpose | Shared? |
|---|---|---|
| `<project-root>/.claude/` | Team configuration — committed to git | Yes — all teammates |
| `~/.claude/` | Personal preferences, session state, machine-local | No — just you |

The project-level folder holds shared rules. The global folder holds personal preferences and session history. [Source: Anatomy of the .claude_ folder.md]

## The Complete Map

```
your-project/
├── CLAUDE.md                  # Team instructions (committed)
├── CLAUDE.local.md            # Personal overrides (gitignored)
│
└── .claude/
    ├── settings.json          # Permissions + config (committed)
    ├── settings.local.json    # Personal permission overrides (gitignored)
    │
    ├── commands/              # Custom slash commands
    │   ├── review.md          # → /project:review
    │   ├── fix-issue.md       # → /project:fix-issue
    │   └── deploy.md          # → /project:deploy
    │
    ├── rules/                 # Modular, path-scoped instruction files
    │   ├── code-style.md
    │   ├── testing.md
    │   └── api-conventions.md
    │
    ├── skills/                # Auto-invoked reusable workflows
    │   ├── security-review/
    │   │   └── SKILL.md
    │   └── deploy/
    │       └── SKILL.md
    │
    └── agents/                # Specialized subagent personas
        ├── code-reviewer.md
        └── security-auditor.md

~/.claude/
├── CLAUDE.md                  # Your global personal instructions
├── settings.json              # Your global settings
├── commands/                  # Personal commands (/user:command-name)
├── skills/                    # Personal skills (all projects)
├── agents/                    # Personal agents (all projects)
└── projects/                  # Session history + auto-memory
```

[Source: Anatomy of the .claude_ folder.md]

## What Each Component Does

### CLAUDE.md
Claude's instruction manual. Loaded into the system prompt at session start and kept in mind for the entire conversation. Keep under 200 lines — instruction adherence drops with file length. See [[claude-md-guide]] and [[claude-code-memory]].

### CLAUDE.local.md
Personal overrides for the current project. Lives at the project root alongside `CLAUDE.md`. Automatically gitignored so personal tweaks never land in the repo.

### settings.json
Controls what Claude is and isn't allowed to do. The permissions block has three states:
- **allow**: runs without confirmation
- **deny**: blocked entirely
- **neither**: Claude asks before proceeding

See [[claude-code-settings-locations]] for the full permissions schema.

### commands/
Markdown files that become slash commands: `review.md` → `/project:review`. Supports shell injection (`!` backtick) and arguments (`$ARGUMENTS`). Personal commands in `~/.claude/commands/` become `/user:command-name`. See [[claude-code-commands]].

### rules/
Modular instruction files, optionally path-scoped via YAML frontmatter. The right escalation path once CLAUDE.md gets crowded. See [[claude-rules]].

### skills/
Auto-invoked workflows that Claude recognizes from conversation context, without you typing a slash command. Each lives in its own subdirectory with a `SKILL.md`. See [[claude-code-skills]].

### agents/
Specialized subagent personas with their own system prompt, tool restrictions, and model preference. Run in an isolated context window. See [[claude-code-agents]].

## Practical Setup Progression

1. Run `/init` — generates a starter CLAUDE.md from your project; trim heavily
2. Add `settings.json` — allow your run commands, deny destructive operations and `.env` reads
3. Create 1–2 commands — code review and issue fixing are good starting points
4. Split into `rules/` — when CLAUDE.md starts feeling crowded; scope by path where useful
5. Add `~/.claude/CLAUDE.md` — personal preferences that apply across all projects

Skills and agents come in at step 6+ for teams with recurring complex workflows. [Source: Anatomy of the .claude_ folder.md]

## Key Insight

> "CLAUDE.md is your highest-leverage file. Get that right first. Everything else is optimization." [Source: Anatomy of the .claude_ folder.md]

## Related Pages

- [[claude-code-memory]] — official CLAUDE.md loading mechanics, 4-scope hierarchy
- [[claude-md-guide]] — what to write, what to avoid, size guidance
- [[claude-rules]] — .claude/rules/ modular instructions
- [[claude-code-commands]] — .claude/commands/ slash commands
- [[claude-code-skills]] — .claude/skills/ auto-invoked workflows
- [[claude-code-agents]] — .claude/agents/ subagent personas
- [[claude-code-settings-locations]] — settings.json structure and permissions
- [[akshay-pachaar]] — author entity
