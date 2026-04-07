---
title: Claude Context Window Mechanics
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

How Claude's usage limits and context window actually work — the rolling window, quadratic token accumulation, and peak-hour adjustments. Understanding these mechanics is the foundation of [[claude-token-optimization]].

## Rolling 5-Hour Window

Claude does **not** reset at midnight. It uses a rolling 5-hour window. Tokens spent at 9 AM expire from your limit by 2 PM. This means:
- Heavy use in one morning session wastes potential capacity later in the day
- Spreading work across 2–3 sessions (morning/afternoon/evening) maximizes effective throughput [Source: Post by kaize (@0x_kaize).md]

## Peak Hours (Since March 26, 2026)

Anthropic introduced peak-hour throttling effective March 26, 2026:
- **Peak:** 5:00 AM – 11:00 AM Pacific Time / 8:00 AM – 2:00 PM Eastern Time, weekdays
- Same query during peak hours consumes the 5-hour window limit faster
- Weekly total limit remains the same; only the rate of consumption changes
- Non-US users: peak hours may fall in afternoon; calculate from PT timezone [Source: Post by kaize (@0x_kaize).md]

## Quadratic Token Accumulation

Every Claude turn re-reads the entire conversation history. Cost formula:

```
Total tokens = S × N(N+1) / 2
```
where S = average tokens per exchange, N = message count.

This means cost grows quadratically — message 30 costs 31× more than message 1.
Practical implication: long conversations are disproportionately expensive. See [[claude-token-optimization]] for mitigation strategies. [Source: Post by kaize (@0x_kaize).md]

## Relationship to Claude Code Auto-Compact

The same quadratic accumulation problem applies within Claude Code sessions. The [[claude-code-context-management]] auto-compact threshold (recommended 60–75%) is the Claude Code equivalent of the "start a fresh chat every 15–20 messages" habit. Both address the same underlying mechanic.

## Relationship to KB Limitations

The context window ceiling in [[kb-limitations]] is the same mechanic at the wiki scale: even 128K-token windows hold only ~96K words, and LLMs suffer "lost in the middle" effects as context fills. The rolling window and quadratic accumulation apply to KB query sessions too.

## Plans with Overage

Pro, Max 5x, Max 20x subscribers can enable Overage (Settings → Usage) to continue at API pay-as-you-go rates when the session limit is hit, rather than being blocked. A monthly spending cap prevents surprise bills. [Source: Post by kaize (@0x_kaize).md]

## Related Pages

- [[claude-token-optimization]] — the 10 habits that exploit these mechanics
- [[claude-model-selection]] — model cost tiers compound with token accumulation
- [[claude-code-context-management]] — Claude Code's approach to the same problem
- [[kb-limitations]] — the context ceiling in LLM knowledge bases
