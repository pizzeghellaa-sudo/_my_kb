---
title: Lint Workflow (Monthly Health Checks)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Monthly maintenance process for the wiki — catches errors, stale content, and structural problems before they compound. Part of the [[llm-knowledge-base-concept]] system. Described as "the step nobody does" but critical for long-term trustworthiness. [Source: Post by God of Prompt (@godofprompt).md]

## Why It Matters

When the AI writes something slightly wrong and you save it back, the next answer builds on the wrong thing. Two months later, five pages reinforce the same error. Monthly linting catches this before it snowballs. [Source: Post by God of Prompt (@godofprompt).md]

*Caveat: the AI doing the linting has the same blind spots as the AI that made the error — linting helps but doesn't fully solve error compounding. See [[kb-limitations]].*

## What to Check

- Contradictions between pages
- Stale claims superseded by newer sources
- Orphan pages with no inbound links
- Concepts mentioned but never explained
- Missing cross-references
- Claims without source attribution

[Source: Post by God of Prompt (@godofprompt).md]

## Lint Prompt (Copy-Paste)

```
"Run a full health check on wiki/ per the lint workflow in CLAUDE.md. Output to wiki/lint-report-[date].md with severity levels (🔴 errors, 🟡 warnings, 🔵 info). Suggest 3 articles to fill the biggest knowledge gaps."
```

[Source: Post by God of Prompt (@godofprompt).md]

## Output Format

`wiki/lint-report-[date].md` with severity levels:
- 🔴 Errors — contradictions, missing citations, broken logic
- 🟡 Warnings — stale claims, missing cross-references, orphan pages
- 🔵 Info — suggestions, gaps to fill, optional improvements

## Cadence

Once per month. ~10 minutes of human review time. Non-negotiable if you want the system to stay trustworthy long-term. [Source: Post by God of Prompt (@godofprompt).md]

## Related Pages

- [[ingest-workflow]] — where errors are introduced
- [[query-workflow]] — where errors surface in answers
- [[kb-limitations]] — why lint alone doesn't fully solve error compounding
- [[knowledge-compounding]] — the positive feedback loop lint protects
