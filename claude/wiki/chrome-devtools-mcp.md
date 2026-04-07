---
title: Chrome DevTools MCP
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

An [[mcp-protocol]] server from the ChromeDevTools team that enables AI coding agents to control and inspect live Chrome browsers via Chrome DevTools. Organized into 6 capability categories with 29 total tools. [Source: ChromeDevTools-chrome-devtools-mcp- Chrome DevTools for coding agents.url]

## Six Capability Categories

| Category | Tools | What it enables |
|---|---|---|
| **Input Automation** | 9 | Click, drag, fill forms, handle dialogs, hover, press keys, type, upload files |
| **Navigation** | 6 | Create/close/select pages, navigate URLs, wait for conditions |
| **Emulation** | 2 | Emulate devices, resize viewports |
| **Performance** | 4 | Record traces, analyze insights, memory snapshots, performance data |
| **Network** | 2 | Inspect and list network requests with full details |
| **Debugging** | 6 | Analyze network requests, screenshots, console messages with source-mapped stack traces |

[Source: ChromeDevTools-chrome-devtools-mcp- Chrome DevTools for coding agents.url]

## Installation

```json
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```

Slim mode (basic tasks only):
```json
"args": ["-y", "chrome-devtools-mcp@latest", "--slim", "--headless"]
```

[Source: ChromeDevTools-chrome-devtools-mcp- Chrome DevTools for coding agents.url]

## Configuration Options

| Flag | Effect |
|---|---|
| `--headless` | Run without visible browser UI |
| `--isolated` | Use temporary user data directory |
| `--slim` | Expose only 3 essential tools |
| `--browserUrl` | Connect to existing Chrome instance |
| `--channel` | Select Chrome channel (stable/canary/beta/dev) |
| `--experimentalVision` | Enable coordinate-based tools |
| `--no-usage-statistics` | Opt out of usage collection |

## Key Notes

- Supports Google Chrome and Chrome for Testing only
- Exposes all browser content to MCP clients (security consideration)
- Browser launches automatically when tools are first invoked
- Performance tools may query Google CrUX API for real-user data

## Quick Test

```
"Check the performance of https://developers.chrome.com"
```

[Source: ChromeDevTools-chrome-devtools-mcp- Chrome DevTools for coding agents.url]

## Comparison with Playwright MCP

| | Chrome DevTools MCP | Playwright MCP |
|---|---|---|
| Focus | Inspection, performance, debugging | Automation, testing, interaction |
| Performance analysis | Yes (traces, memory, CrUX) | No |
| Input automation | Yes (9 tools) | Yes |
| Official maintainer | ChromeDevTools team | Community |

## Related Pages

- [[mcp-protocol]] — the protocol this server implements
- [[playwright-mcp-server]] — complementary browser automation MCP
- [[claude-code-fullstack]] — Chrome DevTools MCP cited as a key debugging visibility tool
