---
title: Claude Code Custom Commands (.claude/commands/)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

The `.claude/commands/` folder turns markdown files into custom slash commands available inside Claude Code sessions. Every markdown file in the folder becomes a `/project:filename` command. They are explicitly triggered — you type the command; Claude does not invoke them automatically. [Source: Anatomy of the .claude_ folder.md]

## How Commands Work

Filename maps directly to command name:

| File | Command |
|---|---|
| `.claude/commands/review.md` | `/project:review` |
| `.claude/commands/fix-issue.md` | `/project:fix-issue` |
| `.claude/commands/deploy.md` | `/project:deploy` |

When you run the command, Claude reads the markdown file, executes any embedded shell commands, and uses the result as the prompt. [Source: Anatomy of the .claude_ folder.md]

## Shell Injection: The `!` Backtick Syntax

The most powerful feature of commands. Use `` !`shell command` `` to run a shell command and embed its output directly into the prompt before Claude sees it:

```markdown
---
description: Review the current branch diff for issues before merging
---
## Changes to Review

!`git diff --name-only main...HEAD`

## Detailed Diff

!`git diff main...HEAD`

Review the above changes for:
1. Code quality issues
2. Security vulnerabilities
3. Missing test coverage
4. Performance concerns

Give specific, actionable feedback per file.
```

Running `/project:review` automatically injects the real git diff. Claude sees live data, not a template. [Source: Anatomy of the .claude_ folder.md]

## Passing Arguments: `$ARGUMENTS`

Use `$ARGUMENTS` to pass text typed after the command name:

```markdown
---
description: Investigate and fix a GitHub issue
argument-hint: [issue-number]
---
Look at issue #$ARGUMENTS in this repo.

!`gh issue view $ARGUMENTS`

Understand the bug, trace it to the root cause, fix it, and write a
test that would have caught it.
```

Running `/project:fix-issue 234` feeds the text `234` into `$ARGUMENTS`, which gets substituted into the shell command and the prompt body. [Source: Anatomy of the .claude_ folder.md]

## Project vs Personal Commands

| Location | Command prefix | Shared? |
|---|---|---|
| `.claude/commands/` | `/project:command-name` | Yes — committed to git |
| `~/.claude/commands/` | `/user:command-name` | No — personal, all projects |

Personal commands in `~/.claude/commands/` are available in every project but not committed to any repo. Useful for standup helpers, commit message generators, or personal security scans. [Source: Anatomy of the .claude_ folder.md]

## Commands vs Skills

| | Commands | Skills |
|---|---|---|
| **Trigger** | You type the slash command explicitly | Claude auto-invokes when conversation matches |
| **Structure** | Single markdown file | Subdirectory with SKILL.md + supporting files |
| **Use for** | On-demand workflows you initiate | Recurring patterns Claude should recognize |

Commands wait for you. Skills watch the conversation and act when the moment is right. [Source: Anatomy of the .claude_ folder.md]

## Good Starting Commands

- Code review against main branch (`/project:review`)
- Fix a specific GitHub issue by number (`/project:fix-issue`)
- Format a commit message following your convention (`/user:commit`)
- Daily standup aggregator (`/user:standup`)
- Quick security scan (`/user:security-scan`)

## Related Pages

- [[claude-dot-folder-anatomy]] — full .claude/ folder map and how commands fit in
- [[claude-code-skills]] — the auto-invoked alternative to explicit commands
- [[claude-code-settings-locations]] — where command files are stored
- [[akshay-pachaar]] — author of the source document
