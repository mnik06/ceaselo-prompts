Redraft the `## Feedback loops` section of the instructions for the agents that plan, build, verify and review tickets in this repository: only what they cannot learn from the repository itself.
Preset: {{preset}}

Its command contract, which every session already receives (do not repeat these commands):
{{contract}}{{repository}}

{{current}}

Write exactly one `## Feedback loops` section and nothing else, at most 40 lines of `- ` bullets, one fact per bullet. Cover, in this order: how to check a change here, fastest check first (one test file, one package's typecheck, the affected tests); how to run the stack and its local services; how to sign in or seed a test account locally; how to drive the UI (where it opens, the route to start from). Name a contract command only to add what it lacks (a narrower form, a flag, a port), never to repeat it, and never restate what the repository's own CLAUDE.md, AGENTS.md or agent docs already say. No other heading, no prose paragraph, no triple-backtick fence. The rest of the instructions is kept as written: never add anything outside this section.

Answer with exactly one JSON object and nothing else: { "instructions": string }
