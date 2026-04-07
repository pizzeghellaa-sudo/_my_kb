---
title: Claude Code Settings (8 Key Customizations)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

8 high-value Claude Code customizations documented by Vishwas Gopinath (builder.io, March 2026). The core philosophy: tell Claude what you want in plain English and it writes the JSON config for you. Everything lives in three places: shell profile (aliases), `~/.claude/settings.json` (global settings/hooks), and `~/.claude/CLAUDE.md` (instructions). [Source: 8 Claude Code Settings to Customize in Minutes.url]

## The 8 Settings at a Glance

| # | Setting | Where | Impact |
|---|---|---|---|
| 1 | `cc` alias | Shell profile | Skip all permission prompts |
| 2 | Auto-compact threshold | `~/.claude/settings.json` | Prevent context degradation |
| 3 | Personal CLAUDE.md | `~/.claude/CLAUDE.md` | Global instruction layer |
| 4 | Status line | `~/.claude/settings.json` | Live session dashboard |
| 5 | Auto-format hook | `.claude/settings.json` | Format on every edit |
| 6 | Spinner verbs | `~/.claude/settings.json` | Cosmetic / morale |
| 7 | Completion sound | `~/.claude/settings.json` | Async working style |
| 8 | Output style | `~/.claude/settings.json` | Response verbosity |

## Quick Reference

- **Setting up anything:** Just tell Claude what you want — it writes the config
- **Check active settings:** `/status`
- **Browse/install plugins:** `/plugin`
- **Set up hooks interactively:** `/hooks`
- **Set output style interactively:** `/config`
- **Set up status line:** `/statusline`

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Next Steps (from the article)

After these basics, MCP servers are the recommended next exploration — they connect Claude to external tools (databases, browser automation). The Playwright MCP server is suggested as a good first one. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Related Pages

- [[claude-code-aliases]] — the `cc`, `ccp`, `ccr` aliases (setting #1)
- [[claude-code-context-management]] — auto-compact, /clear, /compact (setting #2)
- [[claude-md-personal]] — personal CLAUDE.md at `~/.claude/CLAUDE.md` (setting #3)
- [[claude-code-status-line]] — live status line (setting #4)
- [[claude-code-hooks]] — PostToolUse and Stop hooks (settings #5, #7)
- [[claude-code-output-styles]] — output style options (setting #8)
- [[claude-code-settings-locations]] — where all settings files live
- [[vishwas-gopinath]] — author of this source
