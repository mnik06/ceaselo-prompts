Redraft this repository's instructions: free text on its card that the project's people read and that every agent planning, building, verifying and reviewing its tickets receives and must follow.
Preset: {{preset}}

Its command contract, which the machine runs:
{{contract}}{{repository}}

{{current}}

Write clear, readable Markdown, short headings and bullets, at most 80 lines, covering what is true of this repository and only that:
- **Checking a change.** The feedback loop: the actual commands that check nothing is broken, named as runnable commands (for example "Typecheck: `pnpm run typecheck`", "Lint: `pnpm run lint`", "Test: `pnpm run test`"), fastest first; when the repository has one command that runs them all (a preflight, `check` or `ci` script), name it as the check to run before a change is done. Agents run exactly this loop to check their work and are not done while it is red, and the machine's final check runs the same commands, so name only commands that exist in the repository and pass on its current code. When the stack can run each check narrowed to what a branch changed (changed packages and their dependents, a cache, related tests), name that form beside it, marked as such: agents iterate with it and the machine's final check runs it, and the full commands run on the default branch. When the one command that runs them all sits beside its checks, the checks are the loop.
- **Local database and services**, when the stack has them: what they are (for example a local Supabase with Postgres, Auth and Storage), how a local migration is generated and applied, which the agent does itself, and how migrations reach staging and production, read from the preset, the CI workflows and the deploy configuration. State only what the files and the preset show; when nothing in them deploys or migrates staging or production, say that it is not set up, never invent one.
- **How to sign in or seed a test account locally, and how to reach each surface the contract lists** the way its drive does: for `browser`, where it opens and the route to start from (for a web build standing in for a native app, how it is built and served, and every stub that stands in on web for a plugin or API the web build lacks); for `cli`, the built command and how to run it; for `http`, the base address and how a request authenticates.
- A few genuinely useful gotchas, one line each. No trivia an agent finds on its own (an IPv6 localhost, a port of an admin console, how to open a database shell), and nothing the repository's own CLAUDE.md, AGENTS.md or agent docs already say.

No triple-backtick fence. `loop` is the feedback loop your text states, in its order, each command exactly as written: `tests` is true for a step that runs the test suite (a preflight that runs the tests counts), a command that only runs other steps of the loop together (a preflight beside its typecheck, lint and test) is left out of `loop`, `affected` is its narrowed form as written (a base branch in it becomes `{base}`) or null; the loop is null only when the text states no check.

Answer with exactly one JSON object and nothing else: { "instructions": string, "loop": { "name": string, "command": string, "tests": boolean, "affected": string | null }[] | null }
