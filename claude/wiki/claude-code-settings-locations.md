---
title: Claude Code Settings File Locations
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Claude Code settings are split across three scoped files. Understanding which file to use prevents settings from leaking into wrong contexts or conflicting between team members. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## The Three Settings Scopes

| File | Scope | Git | Use for |
|---|---|---|---|
| `~/.claude/settings.json` | Global (all projects) | No | Personal preferences: aliases, sounds, output style, global hooks |
| `.claude/settings.json` | Project (team-shared) | **Committed** | Shared hooks, permissions, team conventions |
| `.claude/settings.local.json` | Project (personal) | Gitignored | Personal permission overrides that shouldn't affect teammates |

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Permissions Schema (settings.json)

The `permissions` block in `.claude/settings.json` has three states for any tool or command: **allow** (runs without confirmation), **deny** (blocked entirely), or **unspecified** (Claude asks before proceeding).

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(git status)",
      "Bash(git diff *)",
      "Read",
      "Write",
      "Edit"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(curl *)",
      "Read(./.env)",
      "Read(./.env.*)"
    ]
  }
}
```

The `$schema` line enables autocomplete and inline validation in VS Code or Cursor — always include it.

**Typical allow list:** `Bash(npm run *)` or `Bash(make *)`, read-only git commands, `Read`/`Write`/`Edit`/`Glob`/`Grep`.

**Typical deny list:** destructive shell commands (`rm -rf`), direct network calls (`curl`), sensitive files (`.env`, `secrets/`).

The middle ground — neither allowed nor denied — gives a safety net without requiring you to anticipate every possible command upfront. [Source: Anatomy of the .claude_ folder.md]

## Checking Active Layers

Run `/status` inside Claude Code to see which settings files are currently active and how they're layered. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Team Sharing

To share customizations with your team:
- Commit `.claude/settings.json` to the repository
- Commit `.claude/skills/` for shared skills
- Use `/plugin` to browse, install, and distribute packaged settings + skills + hooks [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Resetting to Defaults

Delete or rename the relevant file. Claude Code loads built-in defaults on the next session. To reset only one scope, remove just that file — other scopes are unaffected. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Cost Tracking Commands

Within a session:
- `/cost` — API spending (API key users)
- `/stats` — usage against subscription quota (Claude Max/Pro subscribers)

Cross-session analytics:
- `npx ccusage@latest` — breakdowns by model, project, and time period from local JSONL files
- Usagebar — always-visible menu bar app for macOS

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Related Pages

- [[claude-code-settings]] — the 8 settings and what goes where
- [[claude-code-hooks]] — hooks config in settings files
- [[claude-md-personal]] — the companion CLAUDE.md file system (separate from settings.json)
