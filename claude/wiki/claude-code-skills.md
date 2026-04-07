---
title: Claude Code Skills
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Reusable, named instruction files stored in `.claude/skills/` that extend Claude Code's capabilities with domain-specific knowledge and workflows. Skills are the mechanism for turning Claude Code into what Thariq (@trq212) calls an "AI second brain" for a codebase.

## What a Skill Is

A skill is a markdown file (typically `SKILL.md`) placed in `.claude/skills/<skill-name>/`. When triggered — either explicitly by name or by natural language that matches its description — Claude reads the skill file and follows its instructions. [Source: Post by Thariq (@trq212).md]

## Hub-and-Spoke Structure

Large skills use a hub-and-spoke pattern:

```
.claude/skills/
└── queue-debugging/
    ├── SKILL.md          ← hub: ~30 lines, dispatches to spokes
    ├── stuck-jobs.md
    ├── dead-letters.md
    ├── retry-storms.md
    └── consumer-lag.md
```

The hub SKILL.md matches the symptom and reads the linked spoke file. This keeps each file small while handling complex multi-scenario skills. [Source: Post by Thariq (@trq212).md]

## SKILL.md Design Principles

**Natural language triggers over step-by-step instructions:**

❌ Too prescriptive:
```
Step 1: Run git log to find the commit.
Step 2: If there are conflicts, run git status…
Step 3: For each <<< marker, decide which side to keep…
```

✅ Better:
```
Cherry-pick the commit onto a clean branch.
Resolve conflicts preserving intent.
If it can't land cleanly, explain why.
```

The better version gives Claude intent and judgment; the prescriptive version front-loads steps that may not apply. [Source: Post by Thariq (@trq212).md]

**Trigger-focused descriptions:**
```yaml
name: babysit-pr
description: Monitors a PR until it merges. Trigger on 'babysit',
  'watch CI', 'make sure this lands'.
```
Short, specific, trigger-phrase oriented — better than a comprehensive but vague description. [Source: Post by Thariq (@trq212).md]

## Skills with Persistent Memory

Skills can log state across sessions using `${CLAUDE_PLUGIN_DATA}`:

```markdown
## Memory
Append each standup to ${CLAUDE_PLUGIN_DATA}/standups.log
after posting. This folder persists across skill upgrades.

On each run:
- read the log to see what changed since yesterday
- write today's entry after sending to Slack
```

`${CLAUDE_PLUGIN_DATA}` is a persistent folder that survives skill updates, enabling accumulation of session state. [Source: Post by Thariq (@trq212).md]

## Library & API Reference Skills

One of the most powerful skill categories. Instead of Claude guessing your internal APIs, encode domain knowledge directly:

```python
# lib/signups.py
def fetch(day):
    """Signups from events.raw for one day.
    - event='signup_completed', NOT 'signup_started'
    - dedupe by anonymous_id — user_id is null until after signup"""
```

With this as a skill, Claude can generate accurate investigation scripts (like `investigate.py`) that use your specific conventions and field names without hallucinating them. [Source: Post by Thariq (@trq212).md]

## The 9 Durable Skill Categories

See [[claude-code-skills-categories]] for the full taxonomy.

## Skills vs Commands

The clearest distinction:

| | Skills | Commands |
|---|---|---|
| **Trigger** | Claude auto-invokes when conversation matches | You type an explicit slash command |
| **Structure** | Subdirectory with SKILL.md + supporting files | Single markdown file |
| **Use for** | Patterns Claude should recognize and act on | On-demand workflows you initiate |

Commands wait for you. Skills watch the conversation and act when the moment is right. [Source: Anatomy of the .claude_ folder.md]

## allowed-tools Frontmatter

SKILL.md can restrict which tools the skill is permitted to use:

```yaml
---
name: security-review
description: Comprehensive security audit. Use when reviewing code for
  vulnerabilities, before deployments, or when the user mentions security.
allowed-tools: Read, Grep, Glob
---
```

Restricting tools scopes the skill's blast radius and makes its behavior predictable. [Source: Anatomy of the .claude_ folder.md]

## Team Sharing

Skills in `.claude/skills/` can be committed to git for team sharing. Personal skills in `~/.claude/skills/` are available across all projects but not shared. Use `/plugin` to browse and install skills from a marketplace. [Source: 8 Claude Code Settings to Customize in Minutes.url | Anatomy of the .claude_ folder.md]

## Related Pages

- [[claude-code-skills-categories]] — the 9 taxonomy categories
- [[claude-code-commands]] — the explicit-trigger alternative to skills
- [[claude-code-agents]] — isolated-context subagents (vs in-session skills)
- [[claude-code-settings]] — skills are part of the broader Claude Code customization system
- [[claude-code-settings-locations]] — where skills are stored and how to share them
- [[thariq]] — primary source entity
- [[akshay-pachaar]] — additional source entity
