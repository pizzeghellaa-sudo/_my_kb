---
title: AI Agent Patterns (Anthropic)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Anthropic's engineering guide to building effective AI agents. Core philosophy: find the simplest solution first, increase complexity only when needed. The most successful implementations use "simple, composable patterns rather than complex frameworks." [Source: Building Effective AI Agents - Anthropic.url]

## Fundamental Distinction: Workflows vs Agents

| Type | What it is | Best for |
|---|---|---|
| **Workflow** | LLMs + tools orchestrated through predefined code paths | Well-defined tasks, predictability |
| **Agent** | LLM dynamically directs its own processes | Open-ended problems, unpredictable step counts |

[Source: Building Effective AI Agents - Anthropic.url]

## The Augmented LLM (Base Building Block)

Foundation of all patterns: an LLM combined with retrieval, tools, and memory. The emphasis is on tailoring these specifically to the use case and providing "an easy, well-documented interface" for the model.

## The 5 Workflow Patterns

### 1. Prompt Chaining
Decompose tasks into sequential steps where each LLM call processes previous output.
- Best for: tasks decomposable into fixed subtasks
- Example: research → outline → draft → review

### 2. Routing
Classify inputs and direct them to specialized handlers.
- Best for: separation of concerns, optimized prompts for different input types
- Example: route customer questions to different specialized agents

### 3. Parallelization
Run LLM calls simultaneously via:
- **Sectioning** — independent subtasks run in parallel
- **Voting** — multiple attempts for a single task, then pick the best
- Best for: independent subtasks, confidence-requiring decisions

### 4. Orchestrator-Workers
A central LLM dynamically breaks tasks into worker assignments.
- Best for: complex tasks where subtask requirements are unpredictable
- Example: complex coding tasks where the orchestrator decides what to implement

### 5. Evaluator-Optimizer
Iterative refinement: one LLM generates, another evaluates and provides feedback in a loop.
- Best for: tasks with clear quality criteria that benefit from iteration
- Example: translation, writing, code review loops

[Source: Building Effective AI Agents - Anthropic.url]

## When to Deploy Agents (vs Simpler Patterns)

Agents suit open-ended problems where step counts can't be predicted and fixed paths can't be hardcoded. However: "higher costs and the potential for compounding errors" require extensive testing in sandboxed environments before production. [Source: Building Effective AI Agents - Anthropic.url]

## Three Core Implementation Principles

1. **Simplicity** — maintain straightforward agent design
2. **Transparency** — explicitly show planning steps
3. **Tool Design** — thoroughly document and test the agent-computer interface (ACI)

## Tool Engineering Best Practices

- Choose formats closer to naturally occurring internet text
- Avoid artificial constraints (like line counting requirements)
- Include example usage and edge cases in tool definitions
- Minimize cognitive load on the model

[Source: Building Effective AI Agents - Anthropic.url]

## Relationship to Claude Code

Claude Code is itself an agent implementation. The [[claude-code-skills]] system implements the Routing + Orchestrator pattern (skill dispatch). The [[mcp-protocol]] provides the tool interface. [[claude-code-memory]] addresses the memory component of the Augmented LLM.

## Related Pages

- [[claude-code-skills]] — skills as a routing/orchestration mechanism
- [[mcp-protocol]] — tool interface for agents
- [[claude-code-memory]] — memory component
- [[llm-knowledge-base-concept]] — the KB system implements the Augmented LLM pattern with retrieval
