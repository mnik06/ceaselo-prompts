Distill the repository preset below, and for a repository that already has code its own files, into a command contract that machines run without reading prose, plus the repository's instructions for the agents that will work in it.
Preset: {{preset}}{{repository}}{{humanInstructions}}

Answer with exactly one JSON object of this shape and nothing else:
{
  "lockfiles": string[],                       // files whose contents decide whether dependencies must be installed again
  "install": string, "build": string,
  "test": { "all": string, "affected": string | null },   // affected may use {base}
  "run": { "command": string, "readyUrl": string | null, "readyTimeoutS": number, "memoryMb": number },
  "deploy": string | null, "deployPreview": string | null,
  "verify": { "steps": { "name": string, "command": string }[] },   // the floor, in order, fail fast
  "ledgers": { "name": string, "paths": string[], "regenerate": string }[],
  "db": { "template": string, "create": string, "drop": string } | null,   // placeholders {db} and {template}
  "ports": { "block": number, "env": { [ENV_NAME: string]: number } },      // env name -> offset inside the block
  "toolchain": { "node": string | null, "packageManager": string | null },  // see below
  "instructions": string | null                // how to work in this repository, as Markdown (see below)
}

Rules: every command runs with `sh -c` at the root of the repository; nothing is assumed about the package manager or the database, so every tool a command needs is named by the command itself. Dependencies are installed against one shared store: use `$CEASELO_PACKAGE_STORE` where the tool takes a store or cache directory. A stack gets its database name in `$CEASELO_DB_NAME` and its ports as the env variables listed in `ports.env`; `readyUrl` may use `{NAME}` for one of those ports. Use null for what neither the repository nor the preset defines.

`toolchain` is what the repository pins, which the machine installs and puts first on PATH for every command: `node` from `.nvmrc`, `.node-version`, `.tool-versions` or `engines.node`, as digits only (`22`, `22.11` or `22.11.0`; for a range such as `>=20` give its lowest major, for `lts/<name>` the major it names, otherwise null); `packageManager` from `package.json#packageManager` as `name@x.y.z` without the `+sha...` suffix (npm, pnpm or yarn only), else null. Set both to null for a repository that is not a Node project.

`instructions` is what an engineer new to this repository must know to change it safely, in at most 60 lines of Markdown: where each kind of code goes, the conventions to follow, generated code and migrations and how to produce them, test accounts or fixtures, and the traps. Write only what the preset and the files support, and never repeat the commands of the contract. Do not use triple-backtick fences inside it.{{rejected}}
