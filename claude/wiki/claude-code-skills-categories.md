---
title: Claude Code Skills — 9 Durable Categories
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

The taxonomy of "durable skills" for Claude Code — categories of reusable skill files that fit cleanly into long-term codebase knowledge. Documented by [[thariq]] (@trq212). Each category has example skill names showing the pattern.

## The 9 Categories

| Category | Purpose | Example skills |
|---|---|---|
| **Library & API Reference** | Internal libs, CLIs, SDKs, gotchas | `billing-lib`, `platform-cli`, `events` |
| **Product Verification** | Drive the running product to verify | `signup-driver`, `checkout`, `admin` |
| **Data & Analysis** | IDs, field names, query patterns | `funnel-query`, `grafana`, `datadog` |
| **Business Automation** | Multi-tool workflows → one command | `standup`, `tickets`, `weekly-recap` |
| **Scaffolding & Templates** | Framework-correct boilerplate | `new-app`, `migration`, `workflow` |
| **Code Quality & Review** | Methodology that ships better code | `adversarial`, `hypothesis`, `bughunt` |
| **CI/CD & Deployment** | Commit, push, deploy safely | `babysit-pr`, `deploy`, `cherry-pick` |
| **Incident Runbooks** | Symptom → investigation → report | `oncall`, `correlator`, `queue-debug` |
| **Infrastructure Ops** | Safety-gated cleanup & maintenance | `orphans`, `deps`, `cost-investigation` |

[Source: Post by Thariq (@trq212).md]

## Key Observation

The categories represent tasks that require **codebase-specific context** — the kind of knowledge that would otherwise be lost between sessions or require re-explaining each time. Skills make this context permanent and reusable.

## Related Pages

- [[claude-code-skills]] — how skills work (structure, design principles, memory)
- [[thariq]] — source entity
