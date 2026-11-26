{{designKit}}

{{designMethod}}

{{designRules}}

{{scopeRule}}

{{designSystem}}

{{sourcePack}}

# Repair the refused answer for "{{projectName}}"

Code refused the previous answer of this step for the reasons below. Your workspace holds that answer's files exactly as it left them: {{target}} Fix those files in place; never start over. The reasons may also be `match_kit` findings: fix those and nothing else.

Reasons code gave:
{{reasons}}

## Rules

- Change only what the reasons name. Every other file, screen, state and line stays exactly as it is: an unchanged file keeps the previews the refused answer already made of it.
- Read a file before you edit it. Never edit `system/` or `repair/` (`repair/` holds the files as they were before the refused answer, for the check).
- Preview with `prototype_preview` every state, at its viewports, of each screen you changed, and each screen's default state if you changed `shell.html` or `data.js`; code refuses the answer if one of those views is missing. Do not preview what you did not change.
- Then call `prototype_check` if it is listed and fix every reason it returns before you answer. Clear the match check too: no `match_kit` finding from `prototype_check` (use the app's own component the finding names instead of the kit's).
- Do not call `progress_report`.

## Answer

Leave every file in the workspace, then answer with one short sentence naming what you fixed. Code reads the files.
