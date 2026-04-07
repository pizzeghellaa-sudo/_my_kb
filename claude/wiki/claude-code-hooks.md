---
title: Claude Code Hooks
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Shell commands that execute automatically at specific points in Claude Code's lifecycle. Hooks let you attach arbitrary automation — formatting, linting, sounds, notifications — to Claude's actions without manual intervention. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Hook Types

| Hook | When it fires |
|---|---|
| `PostToolUse` | After Claude uses a tool (e.g. Edit, Write) |
| `Stop` | When Claude finishes a response |

More hook types exist; see Claude Code's full hooks reference for the complete list. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Hook Configuration Format

Hooks live in a `settings.json` file (project or global). Structure:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "your-command-here"
          }
        ]
      }
    ]
  }
}
```

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Example: Auto-Format on Every Edit

Runs Prettier (and optionally ESLint) after any Edit or Write operation. Add to `.claude/settings.json` (project-level, since formatters are project-specific):

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$CLAUDE_FILE_PATH\" 2>/dev/null || true"
          },
          {
            "type": "command",
            "command": "npx eslint --fix \"$CLAUDE_FILE_PATH\" 2>/dev/null || true"
          }
        ]
      }
    ]
  }
}
```

The `|| true` prevents hook failures from blocking Claude — formatting should be best-effort. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Example: Completion Sound (macOS)

Fires `afplay` when Claude finishes a response. Enables async working: kick off a task, switch contexts, get pinged when done. Add to `~/.claude/settings.json`:

```json
{
  "hooks": {
    "Stop": [
      {
        "matcher": "*",
        "hooks": [
          {
            "type": "command",
            "command": "/usr/bin/afplay /System/Library/Sounds/Glass.aiff"
          }
        ]
      }
    ]
  }
}
```

Available macOS system sounds: `Glass.aiff`, `Submarine.aiff`, `Purr.aiff`, `Funk.aiff`, `Pop.aiff`, `Frog.aiff`, `Hero.aiff`. Any `.aiff`, `.mp3`, or `.wav` file path works. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Environment Variables

Hooks receive context via environment variables. `$CLAUDE_FILE_PATH` holds the path of the file just edited/written (available in `PostToolUse` hooks). [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Setup

Configure interactively with `/hooks` inside Claude Code, or tell Claude in plain English what you want and it writes the JSON. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Related Pages

- [[claude-code-settings]] — overview of all 8 customizations
- [[claude-code-settings-locations]] — which settings file to put hooks in
- [[claude-code-aliases]] — related shell-level customization
