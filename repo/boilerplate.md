Generate the project skeleton and the agent docs for this repository from its preset, in the current directory.
Preset: {{preset}}{{humanInstructions}}

If the repository already holds code from an earlier attempt, keep it and finish it rather than starting over.

Write the code, a .gitignore that keeps dependencies and build output out of git, and the agent docs:
- a root CLAUDE.md that stays short: what the repository is, a map of where each kind of code lives, the rules that hold everywhere, and pointers to the per-layer docs;
- one doc per layer or area the preset names (for example agent-docs/<layer>.md), read only when working there: its conventions, where new code goes, generated code and migrations and how to produce them, how to test it, and its traps.
Layout, conventions and traps go in these docs; how to check a change, the local database and services and how migrations ship go in the contract's `instructions`, which every session receives.{{designTokens}}

Run the install, the build and every floor step yourself until they pass, on the tools you find on this machine. Do not commit or push: when you are done, the machine provisions the contract's toolchain, runs `install`, `build` and every `verify` step of the contract you answer, in order, and commits and pushes only when all of them pass.

{{contractRules}}

End your turn with the contract object for this repository as you leave it, and nothing after it. Pin in `toolchain` what you built with.
