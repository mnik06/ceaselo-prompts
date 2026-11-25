Read the instructions below, written by the project team for the agents that work in one repository, and find the feedback loop they state: the commands an agent runs to check that a change broke nothing (for example "Test: `pnpm run test`, Lint: `pnpm run lint`", or "Before you are done, run `pnpm run preflight`").

<instructions>
{{instructions}}
</instructions>

Take only the commands the instructions give as that check, in their order, exactly as written (no flag, path or placeholder of your own). Leave out commands for anything else: starting the stack or its services, installing, migrating, seeding, deploying, a single test file given as an example of a narrower run. A command that runs several checks at once (a preflight, a `check` or `ci` script) is one step. `tests` is true when the step runs the test suite (a preflight that runs the tests counts), false for a typecheck, lint, format or build check. `name` is a short label such as "typecheck" or "preflight". `affected` is the same check narrowed to what a branch changed, when the instructions state one for it (for example "while iterating: `pnpm lint:affected`", or `vitest --changed origin/main`), exactly as written; a base branch written in it becomes `{base}`. Null when they state none; a single file or package given as an example is not one. When the instructions state no such check, the loop is null: never infer one from conventions, the stack or package scripts.

Answer with exactly one JSON object and nothing else: { "loop": { "name": string, "command": string, "tests": boolean, "affected": string | null }[] | null }
