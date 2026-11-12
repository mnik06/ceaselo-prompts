Generate the project skeleton and the agent docs for this repository from its preset, in the current directory.
Preset: {{preset}}

The command contract the machines will run (JSON):
{{contract}}

Write the code, a root CLAUDE.md, the per-layer agent docs the preset asks for and a .gitignore that keeps dependencies and build output out of git. Make `install`, `build` and every `verify` step of the contract pass. Do not commit or push: the runtime commits and pushes when the floor is green. Stop when done.
