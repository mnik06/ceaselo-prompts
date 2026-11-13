Rewrite the instructions for the agents that plan, build, verify and review tickets in this repository: what an engineer new to it must know to change it safely.
Preset: {{preset}}

Its command contract, which every session already receives (do not repeat these commands):
{{contract}}{{repository}}

{{current}}

Cover, as far as the preset and the files support it: where each kind of code goes, the conventions to follow, generated code and migrations and how to produce them, test accounts or fixtures, and the traps. At most 60 lines of Markdown; no triple-backtick fences.

Answer with exactly one JSON object and nothing else: { "instructions": string }
