---
title: Claude Code Subagent Personas (.claude/agents/)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

The `.claude/agents/` folder lets you define specialized subagent personas — Claude instances with their own system prompt, restricted tool access, and model preference. When a task is complex enough to benefit from a dedicated specialist, Claude spawns the appropriate agent in an isolated context window. [Source: Anatomy of the .claude_ folder.md]

## How Agents Work

Each agent is a single markdown file with YAML frontmatter:

```
.claude/agents/
├── code-reviewer.md
└── security-auditor.md
```

Example `code-reviewer.md`:

```markdown
---
name: code-reviewer
description: Expert code reviewer. Use PROACTIVELY when reviewing PRs,
  checking for bugs, or validating implementations before merging.
model: sonnet
tools: Read, Grep, Glob
---
You are a senior code reviewer with a focus on correctness and maintainability.

When reviewing code:
- Flag bugs, not just style issues
- Suggest specific fixes, not vague improvements
- Check for edge cases and error handling gaps
- Note performance concerns only when they matter at scale
```

[Source: Anatomy of the .claude_ folder.md]

## Frontmatter Fields

| Field | Purpose |
|---|---|
| `name` | Agent identifier |
| `description` | When Claude should spawn this agent (scanned at session start) |
| `model` | Model to use: `haiku`, `sonnet`, `opus` |
| `tools` | Comma-separated list of allowed tools |

## Isolated Context Window

When Claude spawns a subagent:
1. The agent gets its own fresh context window with its system prompt
2. The agent works independently — explores, reads files, produces findings
3. Findings are compressed and returned to the main session
4. The main session context stays clean — no thousands of tokens of intermediate exploration

This is particularly valuable for long investigative tasks (code review, security audit, debugging) that would otherwise crowd the main conversation context. [Source: Anatomy of the .claude_ folder.md]

## Model Selection Strategy

The `model` field is an optimization lever:

| Model | Best for |
|---|---|
| `haiku` | Focused read-only tasks: search, scan, classify |
| `sonnet` | Code review, analysis, moderate complexity |
| `opus` | Tasks requiring deep reasoning or judgment |

A security auditor that only reads files doesn't need Opus. Restricting it to Haiku saves cost without sacrificing quality. [Source: Anatomy of the .claude_ folder.md]

## Tool Restriction

The `tools` field restricts what the agent can do. Explicit restriction is intentional:

```
tools: Read, Grep, Glob
```

A security auditor that can only read files has no business writing to the codebase. Principle of least privilege applied to AI agents. [Source: Anatomy of the .claude_ folder.md]

## Project vs Personal Agents

| Location | Shared? |
|---|---|
| `.claude/agents/` | Yes — committed to git, available to team |
| `~/.claude/agents/` | No — personal, available across all projects |

## Agents vs Skills

| | Agents | Skills |
|---|---|---|
| **Context** | Isolated window — reports back | Within main session |
| **Definition** | Persona + system prompt + tools + model | Instructions + supporting files |
| **Use for** | Long investigations that would crowd main context | Recurring workflows within a session |

## Relationship to AI Agent Patterns

The `.claude/agents/` mechanism implements the **orchestrator-workers** pattern from Anthropic's agent design: a main Claude instance (orchestrator) delegates tasks to specialized subagents (workers) who return synthesized results. See [[ai-agent-patterns]]. [Source: Anatomy of the .claude_ folder.md]

## Related Pages

- [[claude-dot-folder-anatomy]] — full .claude/ folder map
- [[ai-agent-patterns]] — Anthropic's 5 patterns; orchestrator-workers is the relevant one
- [[claude-code-skills]] — in-session workflows (vs agents which run in isolation)
- [[claude-code-commands]] — explicit slash commands (vs agents which auto-invoke)
- [[akshay-pachaar]] — author of the source document
