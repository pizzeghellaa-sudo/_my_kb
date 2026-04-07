---
title: Claude Model Selection (Haiku / Sonnet / Opus)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Choosing the right Claude model is described as "the most important decision you make every day" by [[kaize]]. Using a more powerful model than a task requires wastes 50–70% of your token budget.

## The Three-Tier Mental Model

| Model | Best for | Relative cost |
|---|---|---|
| **Haiku** | Quick tasks, drafts, simple tasks | Low |
| **Sonnet** | Real work, medium complexity | Medium |
| **Opus** | Deep thinking, high complexity | High |

[Source: Post by kaize (@0x_kaize).md]

## Simple Tasks for Haiku

Grammar checking, brainstorming, formatting, quick translations, short answers — Haiku handles all of these. Using Haiku for simple tasks can free up 50–70% of your budget for work that truly requires Sonnet or Opus. [Source: Post by kaize (@0x_kaize).md]

## Advanced Thinking

Claude's Advanced Thinking feature (extended reasoning) also consumes significant extra tokens. Keep it off by default; only enable it if your first attempt at a response was unsatisfactory. [Source: Post by kaize (@0x_kaize).md]

## Model Selection in Claude Code Context

The builder.io guide on [[claude-code-settings]] recommends using frontier models (Sonnet/Opus) for ingest and complex queries in the [[llm-knowledge-base-concept]], and cheaper models for simple updates — the same tiering logic applied to KB workflows. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Related Pages

- [[claude-token-optimization]] — the full 10-habit context for model selection
- [[claude-context-window-mechanics]] — model cost multiplied by token accumulation
- [[kb-limitations]] — cost considerations for LLM KB workflows (~$2-5/source with frontier models)
