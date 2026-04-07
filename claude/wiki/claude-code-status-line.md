---
title: Claude Code Status Line
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

A shell script that runs after every Claude turn and displays live session information at the bottom of the terminal — effectively a dashboard for your Claude Code session. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Setup

Fastest method: run `/statusline` inside Claude Code. It asks what you want to display and generates the script.

Manual method: write the script yourself, save to `~/.claude/statusline-command.sh`, make it executable, then tell Claude to register it in user settings. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## What It Can Display

The script receives a JSON object on stdin with session data. Common displays:

- **Current directory** — `basename` of working dir
- **Git branch + dirty status** — branch name with `✗` if uncommitted changes exist
- **Context usage** — tokens used vs window size, as percentage, color-coded:
  - Green: < 50% full
  - Yellow: 50–80% full
  - Red: > 80% full
- Active model, cost-per-session (user-configured)

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Context Usage Color Coding

The color-coding makes context saturation visible at a glance, complementing the auto-compact threshold setting. See [[claude-code-context-management]] for how these two features work together.

## Community Tools

Pre-built status line templates exist if you don't want to write your own:
- `ccstatusline`
- `starship-claude`

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Related Pages

- [[claude-code-settings]] — overview of all 8 customizations
- [[claude-code-context-management]] — the context usage that the status line visualizes
- [[claude-code-settings-locations]] — where the status line config is stored
