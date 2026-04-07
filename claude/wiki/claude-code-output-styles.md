---
title: Claude Code Output Styles
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Output styles control how Claude Code formats its responses — verbosity, structure, and tone. Configure interactively with `/config` or tell Claude your preference and it sets it. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Built-In Styles

| Style | Best for |
|---|---|
| **Explanatory** | Detailed, step-by-step responses — learning new concepts |
| **Concise** | Brief, action-focused responses — shipping fast |
| **Technical** | Precise, jargon-friendly responses — deep implementation work |

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Custom Output Styles

Create `.md` files with YAML frontmatter in `~/.claude/output-styles/`. Custom styles appear as options in `/config`. Examples:
- A "code-review" style: terse, finding-focused
- A "documentation" style: thorough, structured

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Related Display Settings

| Setting | What it does |
|---|---|
| `showTurnDuration` | Displays how long each response took — useful for spotting when a model switch might help |
| `prefersReducedMotion` | Tones down animations — accessibility |

Both set in `~/.claude/settings.json`. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Spinner Customization

While Claude thinks, the terminal shows a spinner with verbs ("Flibbertigibbeting…"). These can be replaced or augmented:

```json
{
  "spinnerVerbs": {
    "mode": "replace",
    "verbs": ["Hallucinating responsibly", "Pretending to think", "..."]
  }
}
```

Use `"mode": "append"` to mix custom verbs with the defaults. Related: `spinnerTipsOverride` (replace hint text) and `spinnerTipsEnabled` (toggle hints on/off). [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Related Pages

- [[claude-code-settings]] — overview of all 8 customizations
- [[claude-code-settings-locations]] — settings.json locations
