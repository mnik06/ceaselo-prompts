Rewrite the instructions for the agents that plan, build, verify and review tickets in this repository: only what they cannot learn from the repository itself.
Preset: {{preset}}

Its command contract, which every session already receives (do not repeat these commands):
{{contract}}{{repository}}

{{current}}

Never restate what the repository's own CLAUDE.md, AGENTS.md or agent docs already say; Claude reads those in the checkout. When the repository has no such docs, cover where each kind of code goes, the conventions to follow, generated code and migrations and how to produce them, and the traps. Always cover what no file holds: test accounts and fixtures, external services and how their credentials reach the code, quirks of the environment. At most 60 lines of Markdown; no triple-backtick fences.

Answer with exactly one JSON object and nothing else: { "instructions": string }
