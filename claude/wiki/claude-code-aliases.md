---
title: Claude Code Shell Aliases
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Shell aliases that make Claude Code faster to invoke. The `cc` alias is described as "how I start every Claude session" by Vishwas Gopinath. Add to `~/.zshrc` or `~/.bashrc`, then run `source ~/.zshrc` to activate. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Core Aliases

```bash
# Skip all permission prompts
alias cc='claude --dangerously-skip-permissions'

# Start in plan mode (read-only, no edits)
alias ccp='claude --permission-mode plan'

# Resume the last session
alias ccr='claude --resume'
```

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## One-Shot and Piped Usage

The `cc` alias works for quick one-liners without opening an interactive session:

```bash
# Generate a commit message from staged changes
cc -c "write a commit message for the staged changes"

# Pipe in context
cat error.log | cc "explain this error and suggest a fix"
```

[Source: 8 Claude Code Settings to Customize in Minutes.url]

## The `--dangerously-skip-permissions` Flag

The name is intentionally alarming. It lets Claude run any command and edit any file without asking for confirmation. Recommended only after months of daily use — when you fully understand what Claude Code will and won't do to a codebase. [Source: 8 Claude Code Settings to Customize in Minutes.url]

## Plan Mode (`ccp`)

Launches Claude in read-only mode — it can analyze and plan but cannot make edits. Useful for research sessions or reviewing before committing to changes. See also [[claude-code-context-management]] for context-related session management.

## Related Pages

- [[claude-code-settings]] — overview of all 8 customizations
- [[claude-code-hooks]] — complementary shell-level automation
- [[claude-code-context-management]] — session context commands (/clear, /compact)
