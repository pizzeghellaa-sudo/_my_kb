---
title: KB Limitations and Failure Modes
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Known failure modes of the [[llm-knowledge-base-concept]], as documented by [[andrej-karpathy]] and analyzed by [[god-of-prompt]]. The pattern is described as "nascent, not a finished product." Karpathy himself called his implementation "a hacky collection of scripts." [Source: Post by God of Prompt (@godofprompt).md]

## 1. Context Window Ceiling

- Karpathy's wiki works at ~100 articles / ~400K words
- Even 128K-token context windows hold only ~96K words
- The AI reads selectively through the index — it can miss things
- LLMs suffer from **"lost in the middle" effects**: information in the center of long inputs gets deprioritized
- Query results will have blind spots

**Mitigation:** Keep each wiki focused on one domain. Multiple domains → multiple separate knowledge bases. [Source: Post by God of Prompt (@godofprompt).md]

## 2. Error Compounding

The single biggest risk. Sequence: AI writes a subtle mistake → query answers build on it → you file the answer back → two pages reinforce the same error → five pages compound it.

Monthly [[lint-workflow]] helps but doesn't fully solve it — the AI doing the linting has the same blind spots as the AI that made the error.

**Mitigation:** Monthly lint checks. Cross-check critical claims manually. Never trust the wiki blindly on high-stakes decisions. [Source: Post by God of Prompt (@godofprompt).md]

## 3. Hallucination Doesn't Disappear

The wiki approach *reduces* hallucination (AI grounds answers in your sources) but doesn't eliminate it. The AI can still synthesize connections that don't exist in the source material.

Worse: because the wiki *looks* authoritative (clean markdown, cross-references, citations), you're more likely to trust incorrect information than you would a raw chat response.

**Mitigation:** The schema requires source citations on every claim. Uncited claims get flagged by linting. [Source: Post by God of Prompt (@godofprompt).md]

## 4. Cost

- ~$2–5 per source in API calls with frontier models (touching 10–15 pages)
- 50 sources = ~$100–250 just for ingestion
- Every query and lint check also costs tokens

**Mitigation:** Use frontier models for ingest and complex queries; cheaper models for simple updates. [Source: Post by God of Prompt (@godofprompt).md]

## 5. Doesn't Scale to Enterprise

The index-file approach works without RAG at ~100 articles. At 10,000+ sources:
- The index grows too large
- Consistency across thousands of pages becomes impossible
- You need the infrastructure (vector stores, RAG) the system was designed to avoid

**Mitigation:** Accept this as a personal tool, not enterprise infrastructure. Outgrowing it is a good problem. [Source: Post by God of Prompt (@godofprompt).md]

## 6. Single-Model Blind Spots

The entire wiki is one model's interpretation of your sources. That model has biases and tendencies.

**Mitigation:** For high-stakes decisions, run queries through 4+ models independently and compare agreement. More robust; also 4x the cost. [Source: Post by God of Prompt (@godofprompt).md]

## Quantitative Context: Token Accumulation Formula

The context ceiling isn't just a qualitative limit — it's quantifiable. Token cost per session follows `S × N(N+1) / 2` (S = avg tokens per exchange, N = turns). In a long KB session with many queries, costs compound quadratically just like a long chat. This reinforces keeping KB queries focused and filing good answers back in rather than re-deriving them. See [[claude-context-window-mechanics]] and [[claude-token-optimization]]. [Source: Post by kaize (@0x_kaize).md]

## Summary Table

| Failure Mode | Severity | Mitigation |
|---|---|---|
| Context window ceiling | Medium | One domain per KB |
| Error compounding | High | Monthly linting + manual cross-checks |
| Hallucination | Medium | Mandatory source citations, linting |
| Cost | Low-Medium | Tiered model use |
| Scale ceiling (~100 articles) | Low (for personal use) | Accept the scope |
| Single-model bias | Medium | Multi-model cross-check for high-stakes |

## Related Pages

- [[lint-workflow]] — primary mitigation for error compounding
- [[knowledge-compounding]] — the positive loop that error compounding corrupts
- [[llm-knowledge-base-concept]] — the system these limitations apply to
- [[kb-architecture]] — schema design choices that reduce some risks
