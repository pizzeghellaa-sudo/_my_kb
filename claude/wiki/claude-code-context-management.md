---
title: Claude Code Context Management
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Strategies for managing Claude Code's context window — its working memory. As the context window fills, Claude loses track of earlier details and output quality drops. Proactive context management prevents this degradation. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## The Problem

The default auto-compaction threshold is ~95%. By then, coherence has already degraded. Quality drops before compaction kicks in. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Auto-Compact Threshold

Set via `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` in `~/.claude/settings.json`:

```json
{ "env": { "CLAUDE_AUTOCOMPACT_PCT_OVERRIDE": "75" } }
```

Recommended range: **60–75%** for most tasks. Use **85%** if your task genuinely needs more context before compacting. Trial and adjust based on how sessions feel. [Source: 8 Claude Code Settings to Customize in Minutes.url]

Tell Claude: *"Set my auto-compact threshold to 75% in my user settings"* and it will write the JSON.

## Manual Context Commands

| Command | What it does | When to use |
|---|---|---|
| `/clear` | Wipes everything, starts fresh | Switching to a completely different task |
| `/compact` | Summarizes history, keeps key details | Mid-feature, conversation getting long |

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## Preserving Context During Compaction

Add a preservation directive to `CLAUDE.md` (project or personal):

```
When compacting, always preserve:
- Current file paths being edited
- Test failure messages
- Architecture decisions made this session
```

When `/compact` runs (manually or automatically), the specified context survives. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Relationship to the Status Line

The [[claude-code-status-line]] visualizes context usage in real time (green/yellow/red), making it easy to see when you're approaching the threshold before quality degrades.

## Quantitative Cost of Long Conversations

The rolling window and accumulation mechanics are quantified in [[claude-context-window-mechanics]]: token cost formula `S × N(N+1) / 2` means message 30 costs 31× more than message 1. Auto-compact and `/compact` are Claude Code's structural response to this quadratic growth. See also [[claude-token-optimization]] for the broader set of habits.

## Relationship to KB Limitations

The context window ceiling is also a known limitation of the [[llm-knowledge-base-concept]] — Karpathy's wiki works at ~100 articles / ~400K words before the index-reading approach starts missing things. See [[kb-limitations]].

## Related Pages

- [[claude-code-settings]] — overview of all 8 customizations
- [[claude-code-status-line]] — visualizes context usage live
- [[claude-md-personal]] — where to add compaction preservation directives
- [[kb-limitations]] — the broader context window ceiling problem
