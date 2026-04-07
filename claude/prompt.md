Ingest — Single Source (Supervised)
"Read the schema in CLAUDE.md. Process [FILENAME] from raw/. Read it fully, discuss key takeaways with me, then: create summary page, update index, update all relevant pages, add backlinks, flag contradictions, log the ingest."
[Source: Post by God of Prompt (@godofprompt).md]

Ingest — Batch (Less Supervised)
"Read CLAUDE.md. Process all unprocessed files in raw/ sequentially. For each: create summary, update index, update relevant pages, log the ingest. Proceed automatically."
[Source: Post by God of Prompt (@godofprompt).md]

Query — Standard
"Read wiki/index.md. Answer: [QUESTION]. Cite wiki pages. If this answer is worth preserving, offer to file it as a new wiki page."
[Source: Post by God of Prompt (@godofprompt).md]

Lint — Monthly Health Check
"Run a full health check on wiki/ per the lint workflow in CLAUDE.md. Output to wiki/lint-report-[date].md with 🔴/🟡/🔵 severity. Suggest 3 articles to fill gaps."
[Source: Post by God of Prompt (@godofprompt).md]

Explore — Find Hidden Connections
"Read wiki/index.md and identify the 5 most interesting unexplored connections between existing topics. For each, explain what insight it might reveal and what source would help confirm it."
[Source: Post by God of Prompt (@godofprompt).md]

Brief — Executive Summary
"Based on everything in wiki/, write a 500-word executive briefing on [TOPIC]. Cite sources. Structure it as: current state, key tensions, open questions, recommended next steps."
[Source: Post by God of Prompt (@godofprompt).md]

High-Value Query Starters
"What are the three biggest gaps in this knowledge base?"
"Which sources disagree with each other, and on what?"
"What should I research next based on what's here?"
"Write a 500-word briefing on [topic] using only wiki content"
"What connections exist between [concept A] and [concept B]?"
[Source: Post by God of Prompt (@godofprompt).md]

Claude Code Settings — Natural Language Prompts
For configuring Claude Code itself, tell Claude what you want and it writes the JSON. Examples: [Source: 8 Claude Code Settings to Customize in Minutes.url]

"Set my auto-compact threshold to 75% in my user settings"
"Create my personal CLAUDE.md at ~/.claude/CLAUDE.md. I prefer pnpm over npm, types over interfaces, Vitest over Jest, and concise PR descriptions."
"Set up a PostToolUse hook in the project settings that runs Prettier on any file after you edit or write it"
"Set up a Stop hook in my user settings that plays the Glass sound when you finish responding. Use afplay on macOS."
"Save the above script to ~/.claude/statusline-command.sh, make it executable, and set it as my status line in user settings"
"Set my output style to Concise"
See claude-code-settings for the full list of configurable settings.