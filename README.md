# ceaselo-prompts

Public prompts, MCP tool contracts and orchestration docs for Ceaselo.

## Layout

- `prompts.json` at the root: `{ version, prompts: [{ name, file, vars[] }] }`.
- Each `file` is a template using `{{var}}`. Every placeholder must be declared in `vars`, or the set is refused.
- Prompt names are lowercase, grouped with `/` (e.g. `system/echo`).

## Releasing

1. Change templates and `prompts.json`; set `version` to the new tag.
2. Commit, then tag (`git tag vX.Y.Z && git push --tags`).
3. Bump `prompts.tag` in the Ceaselo repo to the same tag.

Published tags must never move: the api refuses a tag it already stored under another commit.
