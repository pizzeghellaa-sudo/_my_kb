---
title: MCP (Model Context Protocol)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Model Context Protocol — an open standard for connecting AI coding agents to external tools, APIs, and services. Claude Code uses MCP to extend its capabilities beyond what's available natively: databases, browser automation, design tools, DevTools, and more. [Source: Connect Claude Code to tools via MCP - Claude Code Docs.url]

## What MCP Does

MCP servers expose tools that Claude Code can call. When an MCP server is connected, Claude can use its tools just like built-in tools. This allows Claude to:
- Browse and interact with live web pages (Playwright MCP)
- Read and modify Figma designs (Figma MCP)
- Inspect Chrome browser state, network, and performance (Chrome DevTools MCP)
- Query databases, call APIs, interact with dev infrastructure

## Configuration Format

MCP servers are configured in Claude Code's settings files. Basic structure:

```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "package-name@latest"]
    }
  }
}
```

Scope follows the standard [[claude-code-settings-locations]] hierarchy — global (`~/.claude/settings.json`), project (`.claude/settings.json`), or local (`.claude/settings.local.json`). [Source: Connect Claude Code to tools via MCP - Claude Code Docs.url]

## MCP Registry

Anthropic maintains an official MCP registry at `https://api.anthropic.com/mcp-registry/v0/servers`. Servers are catalogued with metadata including which Claude products they work with (Claude Code, MCP Connector, Claude Desktop). [Source: Connect Claude Code to tools via MCP - Claude Code Docs.url]

## Notable MCP Servers in This KB

- [[playwright-mcp-server]] — browser automation (navigate, click, test, scrape)
- [[figma-mcp-server]] — Figma design-to-code conversion
- [[chrome-devtools-mcp]] — Chrome DevTools for performance, network, debugging

## Relationship to llms.txt

For documentation access, MCP servers consume significant context (5,000–10,000 tokens per server). `llms.txt` files are a lighter alternative (~100 tokens) for providing LLM-optimized documentation. See [[llms-txt]]. [Source: Claude Code for Fullstack Development- The 3 Things You Actually Need - DEV Community.url]

## Related Pages

- [[claude-code-settings-locations]] — where MCP config lives
- [[playwright-mcp-server]] — browser automation MCP
- [[figma-mcp-server]] — design tool MCP
- [[chrome-devtools-mcp]] — DevTools MCP
- [[llms-txt]] — lightweight alternative for documentation context
