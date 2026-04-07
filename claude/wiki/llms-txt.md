---
title: llms.txt (LLM-Optimized Documentation)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

An emerging standard for providing LLM-optimized documentation for websites, libraries, and frameworks. A lightweight alternative to MCP servers for giving Claude context about external tools. [Source: Claude Code for Fullstack Development- The 3 Things You Actually Need - DEV Community.url]

## What It Is

An `llms.txt` file sits at the root of a website or repository and provides a concise, structured summary optimized for LLM consumption — what the project offers, key APIs, conventions, and where to find more. Like `robots.txt` but for language models.

## Why It Matters

| Approach | Context cost |
|---|---|
| MCP server for documentation | 5,000–10,000 tokens |
| llms.txt file | ~100 tokens |

At 100 tokens, an llms.txt file costs ~50–100× less context than an MCP server. For the [[llm-knowledge-base-concept]], this is significant: every token saved on documentation overhead is available for actual reasoning and wiki content. [Source: Claude Code for Fullstack Development- The 3 Things You Actually Need - DEV Community.url]

## Claude Code Docs Example

The Claude Code documentation itself uses llms.txt. The MCP docs page instructs: "Fetch the complete documentation index at: https://code.claude.com/docs/llms.txt — Use this file to discover all available pages before exploring further." [Source: Connect Claude Code to tools via MCP - Claude Code Docs.url]

## Related Pages

- [[mcp-protocol]] — the heavier alternative
- [[claude-code-fullstack]] — where the llms.txt vs MCP tradeoff is discussed
- [[claude-token-optimization]] — the broader token conservation context
- [[kb-limitations]] — token cost considerations for KB workflows
