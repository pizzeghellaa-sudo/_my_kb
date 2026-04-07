# Wiki Index

## Core Concept
- [LLM Knowledge Base Concept](llm-knowledge-base-concept.md) — Karpathy's pattern: AI compiles a structured wiki from raw sources so knowledge accumulates across sessions

## Architecture & Workflows
- [KB Architecture](kb-architecture.md) — Folder structure, schema file (CLAUDE.md), personal vs project scopes
- [Ingest Workflow](ingest-workflow.md) — How a raw source is processed into the wiki (10–15 pages per source)
- [Query Workflow](query-workflow.md) — How to ask questions against the wiki and file answers back in
- [Lint Workflow](lint-workflow.md) — Monthly health check to catch errors, stale content, and orphan pages

## Knowledge Management Concepts
- [Knowledge Compounding](knowledge-compounding.md) — Why the system gets smarter over time and how to accelerate it
- [KB Limitations](kb-limitations.md) — Context ceiling, error compounding, hallucination, cost, and scale limits
- [KB Use Cases](kb-use-cases.md) — Creators, founders/consultants, researchers; notable adopters (Karpathy, Lex Fridman, DAIR.AI)

## Claude Code — Folder & Configuration
- [Anatomy of the .claude/ Folder](claude-dot-folder-anatomy.md) — Complete map: CLAUDE.md, commands/, rules/, skills/, agents/, settings.json; project vs global
- [Claude Code Settings](claude-code-settings.md) — 8 key customizations overview; three config locations
- [Claude Code Aliases](claude-code-aliases.md) — `cc`, `ccp`, `ccr` shell aliases; `--dangerously-skip-permissions`
- [Claude Code Hooks](claude-code-hooks.md) — PostToolUse (auto-format) and Stop (completion sound) hooks
- [Claude Code Settings Locations](claude-code-settings-locations.md) — Settings scopes; permissions allow/deny schema; cost tracking
- [Claude Code Status Line](claude-code-status-line.md) — Live terminal dashboard: dir, git branch, context usage
- [Claude Code Context Management](claude-code-context-management.md) — Auto-compact threshold, /clear vs /compact
- [Claude Code Output Styles](claude-code-output-styles.md) — Explanatory/Concise/Technical; spinner customization

## Claude Code — Memory & Instructions
- [Claude Code Memory System](claude-code-memory.md) — CLAUDE.md vs auto memory; 4 scopes; loading mechanics; /memory command
- [Claude Code Auto Memory](claude-code-memory-auto.md) — MEMORY.md + topic files; Claude writes its own notes across sessions
- [CLAUDE.md — Personal vs Project](claude-md-personal.md) — ~/.claude/CLAUDE.md (global) vs project-root; compliance research
- [How to Write a Good CLAUDE.md](claude-md-guide.md) — What to include, avoid, and structure; builder.io guide
- [.claude/rules/ (Path-Specific Rules)](claude-rules.md) — Modular, scoped rules; load on demand vs skills

## Claude Code — Skills, Commands & Agents
- [Claude Code Skills](claude-code-skills.md) — .claude/skills/ hub-and-spoke; design principles; skills vs commands; persistent memory
- [Claude Code Skills — 9 Durable Categories](claude-code-skills-categories.md) — Taxonomy: Library Ref, CI/CD, Data, Runbooks, etc.
- [Claude Code Custom Commands](claude-code-commands.md) — .claude/commands/ slash commands; ! backtick shell injection; $ARGUMENTS; /project: vs /user:
- [Claude Code Subagent Personas](claude-code-agents.md) — .claude/agents/ isolated-context specialists; model selection; tool restriction

## Claude Code — MCP & Browser Tools
- [MCP Protocol](mcp-protocol.md) — Model Context Protocol: what it is, config format, registry
- [Playwright MCP Server](playwright-mcp-server.md) — Browser automation: navigate, test, self-QA, storage state
- [Figma MCP Server](figma-mcp-server.md) — Design-to-code conversion via Figma integration
- [Chrome DevTools MCP](chrome-devtools-mcp.md) — Performance, network, debugging; 6 categories, 29 tools

## Claude Code — Fullstack Development
- [Claude Code for Fullstack Development](claude-code-fullstack.md) — 3 requirements: visibility, docs, opinionated stack
- [llms.txt](llms-txt.md) — LLM-optimized documentation standard; ~100 tokens vs 5-10K for MCP

## Claude Usage & Optimization
- [Claude Token Optimization](claude-token-optimization.md) — 10 habits; quadratic cost formula; rolling window; peak hours
- [Claude Context Window Mechanics](claude-context-window-mechanics.md) — Rolling 5-hour window; peak hours (March 26, 2026); S×N(N+1)/2
- [Claude Model Selection](claude-model-selection.md) — Haiku/Sonnet/Opus tiers; Advanced Thinking; 50–70% savings
- [Claude Use Cases](claude-use-cases.md) — Official gallery; inline interactive visualizations; product taxonomy

## AI Agents
- [AI Agent Patterns](ai-agent-patterns.md) — Anthropic's 5 patterns: chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer

## Gap Analysis
- [KB Gaps — April 7, 2026](kb-gaps-2026-04-07.md) — Three biggest gaps: Claude API/agent building, Claude Code practical workflows, Figma MCP + MCP ecosystem

## Reference
- [Prompt Library](prompt-library.md) — Copy-paste prompts for ingest, query, lint, explore, brief, and Claude Code config

## Entities
- [Andrej Karpathy](andrej-karpathy.md) — AI researcher; originated the LLM KB pattern
- [God of Prompt (@godofprompt)](god-of-prompt.md) — AI prompting educator; 7-step build guide
- [Vishwas Gopinath](vishwas-gopinath.md) — Developer educator at Builder.io; 8 Claude Code settings guide
- [kaize (@0x_kaize)](kaize.md) — 10 token optimization habits; rolling window mechanics
- [Thariq (@trq212)](thariq.md) — Claude Code skills system; AI second brain concept
- [Vaibhav (VB) Srivastav (@reach_vb)](vaibhav-srivastav.md) — Token optimization content creator
- [Akshay (@akshay_pachaar)](akshay-pachaar.md) — .claude/ folder anatomy; commands/ and agents/ coverage
