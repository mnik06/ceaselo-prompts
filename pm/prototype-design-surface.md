{{designKit}}

{{designMethod}}

{{designRules}}

{{scopeRule}}

{{designSystem}}

# Your job: the app shell of "{{surfaceName}}" in the prototype of "{{projectName}}"

The product has several surfaces with screens, and the prototype has one frame per surface:
{{surfaces}}

The primary surface's session already wrote what every surface shares: the voice and rationale (`design/design.json`), the sample data with its `APP_DATA.copy` lexicon (`data.js`), and the screen plan of every surface. You write what is this surface's own: its app shell and its plan entries. Parallel sessions then write every screen from your shell and plan.

This surface: "{{surfaceName}}" (id {{surfaceId}}), form factor {{formFactor}}, used by {{surfaceRoles}}. The system block's form factor is this surface's.

Design brief (shared; never change it):
{{brief}}

This surface's screens, as the primary's session planned them (`plan.json` holds them in full):
{{plan}}{{rebuild}}{{ask}}

Exact slugs and keys the machine check holds you to:
- Features these screens must still serve: {{featureSlugs}}
- Roles: {{roleSlugs}}

## How to work

1. Read `system/guide.md`, `design/design.json`, `data.js` and `reference/primary-shell.html` (the primary surface's shell: match its product name, voice, navigation order and patterns where this surface's frame allows; never copy what only fits the other frame).
2. Keep `design/design.json` and `data.js` as they are: they are shared and code keeps the primary's.
3. Rework `plan.json` only where this surface needs it: its entries only, each with `"surface": "{{surfaceId}}"`. Keep every route, feature, REQ key and ticket the primary planned here unless the surface truly does not show it; every role that uses this surface uses some screen of it; a screen links only to screens of this surface; never reuse a route of another surface. Code sets `mobile` from the form factor.
4. Write `shell.html` for this surface in its form factor: navigation reaching every top-level screen of this surface, the logo slot, the user menu, the screens slot (`data-slot="screens"`). Write no file under `screens/`.
5. Preview the shell around the first screen of your plan with `prototype_preview`: its default state at 1440 and 402, at 402 only for a mobile surface, or at 1440 only for a desktop one, in one call (code refuses the answer if one is missing). Fix what you see, then call `prototype_check` if it is listed and fix every reason it returns before you answer.

Hard limits: each plan entry's route at most 120 characters; title and summary 1 to 200 characters; 1 to 12 states, "default" first; `shell.html` at most 200,000 characters.

## Answer

Leave every file in the workspace, then answer with one short sentence on how this surface is laid out. Code reads the files.{{rejected}}
