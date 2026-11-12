Distill the repository preset below into a command contract that machines run without reading prose.
Preset: {{preset}}

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
  "ports": { "block": number, "env": { [ENV_NAME: string]: number } }       // env name -> offset inside the block
}

Rules: every command runs with `sh -c` at the root of the repository; nothing is assumed about the package manager or the database, so every tool a command needs is named by the command itself. Dependencies are installed against one shared store: use `$CEASELO_PACKAGE_STORE` where the tool takes a store or cache directory. A stack gets its database name in `$CEASELO_DB_NAME` and its ports as the env variables listed in `ports.env`; `readyUrl` may use `{NAME}` for one of those ports. Use null for what the preset does not define.{{rejected}}
