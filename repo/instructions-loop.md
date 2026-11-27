Read the instructions below, {{author}} for the agents that work in one repository, and find the feedback loop they state: the commands an agent runs to check that a change broke nothing (for example "Test: `pnpm run test`, Lint: `pnpm run lint`", or "Before you are done, run `pnpm run preflight`"). Drafted instructions list them under a **Feedback loops — run to check a change** section and their narrowed forms under **Narrowed feedback loops — run to check a change and target only affected files**; a person's text may state them anywhere, in any shape. The repository's build files follow them: use them only to resolve what the instructions name and to write probes, never to add a check or a narrowed form the instructions do not state.

<instructions>
{{instructions}}
</instructions>

<build-files>
{{buildFiles}}
</build-files>

The machine runs this loop in full once per ticket, in its verification, and runs the parts of the full loop side by side, so a loop of separate checks finishes in the time of its slowest one, where one aggregate command runs them one after another. Agents never run the full loop: they run only the narrowed forms, and only those stated by a person or proven by the machine.

**The steps.** Take only the commands the instructions give as that check (the Feedback loops section, when there is one), in their order, exactly as written (no flag, path or placeholder of your own). Leave out commands for anything else: starting the stack or its services, installing, migrating, seeding, deploying, a single test file given as an example of a narrower run. `name` is a short label such as "typecheck" or "lint". `tests` is true when the step runs the test suite, false for a typecheck, lint, format or build check.

**An aggregate.** A command that runs several checks at once (a preflight, a `check` or `ci` script):
- When the loop you take also has, as steps of their own, every check it runs, leave it out: its checks are the loop.
- When the build files define it as only running other checks, one after another (`"preflight": "pnpm typecheck && pnpm lint && pnpm test"`, a Makefile target whose recipe is those commands, a turbo pipeline of those tasks), answer each of them as its own step, in its order, exactly as the definition runs it from the repository root (a part the definition runs in a folder keeps that: `cd be && pnpm test`). Give each of them `partOf`: the aggregate's name and its command as the instructions give it.
- Otherwise it stays one step with `partOf` null: its definition is not in the build files, it does more than run checks (it builds, migrates, generates, starts something), or it runs a script whose contents you cannot see.

**The narrowed form**, `affected`: the same check narrowed to what a branch changed, taken exactly as written from a line the instructions mark narrowed (the Narrowed feedback loops section, or a line saying it is the narrowed, affected or iterating form of that check); a base branch in it becomes `{base}`. A single file or package given as an example is not one. Never compose one yourself: a check the instructions give no narrowed form for has `affected` null, and the machine's full run covers it.
- `affectedSource` is "derived" when the instructions were drafted by an agent, "stated" when the project team wrote them.
- Give a narrowed form a `probe` when you can, and always when it is derived: one new file, at a path that does not exist in the listing, inside what the check covers, whose content alone turns that check red: a type error for a typecheck, a lint violation of a rule the repository's config enables for a lint, a failing test the test runner picks up by its name and place for the tests. The machine adds it on a scratch branch and runs the narrowed form: it must go red, else the form is not proven and agents never run it.
- Otherwise `affected`, `affectedSource` and `probe` are null.

When the instructions state no such check, the loop is null: never infer one from conventions, the stack or package scripts the instructions do not name.

Answer with exactly one JSON object and nothing else: { "loop": { "name": string, "command": string, "tests": boolean, "affected": string | null, "affectedSource": "stated" | "derived" | null, "probe": { "path": string, "content": string } | null, "partOf": { "name": string, "command": string } | null }[] | null }
