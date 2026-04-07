---
title: Claude Token Optimization (10 Habits)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

10 habits for reducing Claude token consumption and avoiding usage limits. Posted by [[kaize]] (@0x_kaize, March 29, 2026). Core insight: Claude counts tokens, not messages — and token cost grows quadratically with conversation length.

## The Quadratic Cost Problem

Every turn, Claude re-reads the entire conversation history. Token cost per turn = all previous messages + current one.

**Formula:** `Total = S × N(N+1) / 2`
(S = avg tokens per exchange, N = number of messages)

At ~500 tokens per exchange:
| Messages | Total tokens | Cost vs message 1 |
|---|---|---|
| 5 | 7.5K | — |
| 10 | 27.5K | — |
| 20 | 105K | — |
| 30 | 232K | **31×** |

One developer (Aniket Parihar) tracked usage and found 98.5% of tokens went to re-reading history; only 1.5% to actual output. [Source: Post by kaize (@0x_kaize).md]

## The 10 Habits

### 1. Edit your prompt — don't send a follow-up
Click Edit on your original message → fix it → regenerate. The old exchange is replaced, not stacked. Sending a corrective follow-up ("No, I meant…") adds to history permanently. [Source: Post by kaize (@0x_kaize).md]

### 2. Start a fresh chat every 15–20 messages
At 100+ messages (~500 tokens/exchange), that's 2.5M+ tokens — mostly re-reading history. When long: ask Claude to summarize → copy → new chat → paste as first message. [Source: Post by kaize (@0x_kaize).md]

### 3. Batch questions into one message
Three separate prompts = three context loads. One prompt with three tasks = one context load. Also produces better answers (Claude sees the full picture at once). [Source: Post by kaize (@0x_kaize).md]

### 4. Upload recurring files to Projects
Files uploaded to multiple individual chats get re-tokenized every time. Upload once to a Project → it's cached. Every subsequent conversation in that project references it without re-burning tokens. [Source: Post by kaize (@0x_kaize).md]

### 5. Set up Memory & User Preferences
"Act as a…" in every prompt wastes 3–5 setup messages per chat. Use Settings → Memory and User Settings to save role, communication style, and preferences permanently. [Source: Post by kaize (@0x_kaize).md]

### 6. Turn off features you're not actively using
Web search, connectors, Explore mode — all add tokens to every response even when not needed. Advanced Thinking also consumes tokens; keep off by default, enable only when first attempt is unsatisfactory. [Source: Post by kaize (@0x_kaize).md]

### 7. Use Haiku for simple tasks
See [[claude-model-selection]] for the full decision framework. Haiku for drafts/simple tasks frees up 50–70% of budget for tasks requiring Sonnet or Opus. [Source: Post by kaize (@0x_kaize).md]

### 8. Spread work across the day
The rolling 5-hour window means usage doesn't reset at midnight — it gradually decreases. Tokens spent at 9 AM expire by 2 PM. Divide into 2–3 sessions: morning, afternoon, evening. See [[claude-context-window-mechanics]]. [Source: Post by kaize (@0x_kaize).md]

### 9. Work during off-peak hours
Since March 26, 2026: peak hours consume the 5-hour limit more quickly. Peak: **5:00 AM – 11:00 AM PT / 8:00 AM – 2:00 PM ET, weekdays**. Resource-intensive tasks in evenings or weekends stretch the plan further. Non-US users: check timezone equivalents. [Source: Post by kaize (@0x_kaize).md]

### 10. Enable Extra Usage / Overage as a safety net
Available on Pro, Max 5x, Max 20x plans (Settings → Usage → Overage). When session limit is reached, switches to pay-as-you-go at API rates rather than blocking access. Set a monthly spending cap to control costs. [Source: Post by kaize (@0x_kaize).md]

## Related Pages

- [[claude-context-window-mechanics]] — rolling window mechanics, peak hours, token formula
- [[claude-model-selection]] — Haiku/Sonnet/Opus decision framework
- [[claude-code-context-management]] — related: auto-compact and /compact in Claude Code
- [[kb-limitations]] — same quadratic token cost applies to LLM KB sessions
- [[kaize]] — author entity
