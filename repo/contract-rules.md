The command contract is exactly one JSON object of this shape:
{
  "lockfiles": string[],                       // files whose contents decide whether dependencies must be installed again
  "install": string, "build": string,
  "test": { "all": string, "affected": string | null },   // affected may use {base}
  "run": { "command": string, "readyUrl": string | null, "readyTimeoutS": number, "memoryMb": number },
  "deploy": string | null, "deployPreview": string | null,
  "verify": { "steps": { "name": string, "command": string, "kind": "typecheck" | "build" | "lint" | "test" | "other" }[] },   // the floor, in order, fail fast
  "ledgers": { "name": string, "paths": string[], "regenerate": string }[],
  "db": { "template": string, "create": string, "drop": string } | null,   // placeholders {db} and {template}
  "ports": { "block": number, "env": { [ENV_NAME: string]: number } } | null,   // env name -> offset inside the block
  "toolchain": { "node": string | null, "packageManager": string | null, "flutter": string | null },  // see below
  "instructions": string | null                // see below
}

Rules: every command runs with `sh -c` at the root of the repository; nothing is assumed about the package manager or the database, so every tool a command needs is named by the command itself. Dependencies are installed against one shared store: use `$CEASELO_PACKAGE_STORE` where the tool takes a store or cache directory. A stack gets its database name in `$CEASELO_DB_NAME` and its ports as the env variables listed in `ports.env`; `readyUrl` may use `{NAME}` for one of those ports. `ports` is null for a repository that serves nothing on a port (a mobile app, a library, a CLI), and `db` is null for one without a database. Use null for what neither the repository nor the preset defines.

The floor (`verify.steps`) is what every change must pass before its tests, cheapest first, and is refused unless it holds:
- every step has a `kind`: `typecheck`, `build`, `lint`, `test` or `other` (code or project generation, formatting checks);
- a `typecheck` step before the first `lint` step. Use a dedicated typecheck whenever the stack has one (`tsc --noEmit`, `mypy`, `pyright`, `cargo check`, `go vet`); only a compiled stack without a cheaper one uses its compile as a `build` step there (`xcodebuild build`, `swift build`, `gradle compileDebugKotlin`);
- a `lint` step;
- no `test` step before the first `lint` step. Full test suites belong in `test`, which runs after the floor (`test.affected` when it can narrow), not in `verify.steps`.

`toolchain` is what the repository pins, which the machine installs and puts first on PATH for every command: `node` from `.nvmrc`, `.node-version`, `.tool-versions` or `engines.node`, as digits only (`22`, `22.11` or `22.11.0`; for a range such as `>=20` give its lowest major, for `lts/<name>` the major it names, otherwise null); `packageManager` from `package.json#packageManager` as `name@x.y.z` without the `+sha...` suffix (npm, pnpm or yarn only), else null. Set both to null for a repository that is not a Node project. `flutter` is the exact Flutter release (`3.27.1`) from `.fvmrc`, `.fvm/fvm_config.json` or the preset, else null; the machine provisions that SDK (with its own `dart`), so commands call `flutter` and `dart` by name.

`instructions` is for the agents that plan, build, verify and review tickets here: only what they cannot learn from the repository itself, in at most 60 lines of Markdown, or null when there is nothing to add. Never repeat the contract's commands, and never restate what the repository's own CLAUDE.md, AGENTS.md or agent docs already say. When the repository has no such docs, cover where each kind of code goes, the conventions, generated code and migrations, and the traps. Always cover what no file holds: test accounts and fixtures, external services and how their credentials reach the code, quirks of the environment. Write only what the preset and the files support. Do not use triple-backtick fences inside it.
