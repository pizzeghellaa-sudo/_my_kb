---
title: How to Write a Good CLAUDE.md (Builder.io Guide)
created: 2026-04-07
last_updated: 2026-04-07
source_count: 1
status: draft
---

Builder.io's guide to writing effective CLAUDE.md files. The goal: concise, specific shorthand reminders rather than comprehensive documentation. [Source: How to Write a Good CLAUDE.md File.url]

## What to Include

- Project structure and organization patterns
- Coding standards and style guidelines specific to your project
- Technology stack details and framework conventions
- File naming patterns and directory organization
- Testing approaches and quality standards
- Build and deployment procedures

[Source: How to Write a Good CLAUDE.md File.url]

## Structure Recommendations

- **Header section:** project overview and key context
- **Sections by topic:** group related conventions
- **Code examples:** show do's and don'ts side by side
- **Priority indicators:** mark critical vs optional conventions

[Source: How to Write a Good CLAUDE.md File.url]

## What to Avoid

- Overly verbose explanations when brief summaries suffice
- Mixing multiple unrelated topics in single sections
- Assumptions about Claude's prior knowledge of your codebase
- Outdated or deprecated practices still listed as current

[Source: How to Write a Good CLAUDE.md File.url]

## The Core Principle

"Shorthand reminders rather than complete documentation." Claude should understand your project's unique conventions without reading a manual. [Source: How to Write a Good CLAUDE.md File.url]

## Size Guidance

Keep CLAUDE.md under **200 lines**. Files longer than that start eating too much context, and Claude's instruction adherence actually drops. [Source: Anatomy of the .claude_ folder.md]

> RESOLVED CONTRADICTION: An earlier source (8 Claude Code Settings to Customize in Minutes.url) recommended "under 50 lines" for personal CLAUDE.md. The official Claude Code docs say "target under 200 lines." This source (Anatomy of the .claude_ folder.md) confirms 200 lines as the limit. The 50-line figure likely reflects a stricter personal preference, not a hard rule. Follow 200 lines as the authoritative guidance.

## Minimal Effective Example

~20 lines is sufficient for most projects:

```markdown
# Project: Acme API

## Commands
npm run dev          # Start dev server
npm run test         # Run tests (Jest)
npm run lint         # ESLint + Prettier check
npm run build        # Production build

## Architecture
- Express REST API, Node 20
- PostgreSQL via Prisma ORM
- All handlers live in src/handlers/
- Shared types in src/types/

## Conventions
- Use zod for request validation in every handler
- Return shape is always { data, error }
- Never expose stack traces to the client
- Use the logger module, not console.log

## Watch out for
- Tests use a real local DB, not mocks. Run `npm run db:test:reset` first
- Strict TypeScript: no unused imports, ever
```

This gives Claude everything it needs to work productively without constant clarification. [Source: Anatomy of the .claude_ folder.md]

## Related Pages

- [[claude-code-memory]] — the official Claude Code docs on all CLAUDE.md mechanics
- [[claude-md-personal]] — personal vs project CLAUDE.md
- [[claude-rules]] — `.claude/rules/` for larger projects
- [[kb-architecture]] — how the KB's CLAUDE.md serves as a schema file
