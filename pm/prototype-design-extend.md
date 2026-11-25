{{designKit}}

{{designMethod}}

{{designRules}}

{{scopeRule}}

{{designSystem}}

{{sourcePack}}

# Extend the prototype of "{{projectName}}"

The project has one prototype, updated in place. Someone asked for a feature or ticket to be shown in it. You add the screens the ask needs and edit the screens it touches, in your workspace; code copies every other screen and the shell unchanged. Code assembles one offline HTML file from the design system, the app shell, the sample data and every screen of the plan.

Design brief (keep it):
{{brief}}

App shell (`shell.html`; screens go into its data-slot="screens"):
{{shell}}

Sample data (`data.js`, `window.APP_DATA`, loaded before any screen script runs):
{{data}}

Screen outline (every route that exists; `plan.json` holds the full entries and `screens/<route>.html` the markup, both in your workspace):
{{outline}}

# The ask
{{ask}}

Exact slugs and keys the machine check holds you to:
- Features: {{featureSlugs}}
- Roles: {{roleSlugs}}
- Ticket keys to put on screens: {{ticketKeys}}

## Rules

- Do only what the ask needs. Edit a screen only when the ask changes it; add a screen only when the ask needs one the outline lacks. Never rename or remove a route or a `plan.json` entry, and never touch a screen the ask does not.
- Every ticket key above goes in "tickets" of each `plan.json` entry you add or edit for it, and each key is on at least one screen. Keep the keys an edited entry already lists.
- An edited screen keeps its route; its entry keeps every state, link and role it had unless the ask changes them. Edit `screens/<route>.html` in place.
- An added screen gets a full entry appended to `plan.json` (route, title, summary, features, roles, reqs, states with "default" first, mobile, links, group, tickets) and its file `screens/<route>.html`. Link to it: from the navigation in `shell.html` when it is a top-level screen (add the link and change nothing else there), else from a screen you edit.
- A screen file is its content only: one element data-state="<state>" per state its entry lists, holding that state's full rendering, every other state `hidden`. Build from the vocabulary's classes; a screen's own `<style>` (one, at most 8 KB) adds only what this screen needs, every value a token. Link to every route its entry lists in "links", with href="#/<route>"; link only to routes that exist or that you add.
- Build what the ask, its tickets, their criteria and the requirements name, nothing else. A change that needs a new field, rule, role or flow the requirements do not have, and anything you would add that none of them names (a chart, stat, summary, illustration, column, control, state or copy), is not built: put one line per such item in `flags.json`.
- Take every action label, toast, entity name and empty or error line from `APP_DATA.copy`; a word you need that it lacks follows its pattern.
- Preview every state of every screen you added or edited at its viewports, and every other route's default state when you changed the shell, with `prototype_preview` (6 views per call) and judge each view as its user would: does it lead with the screen's one job; is there one primary action; does any state read as empty or broken; is there a generated-page tell (identical cards for everything, an all-caps label above every heading, middle-dot meta, an accented headline word, "→" on links); does anything clip, crowd or misalign at the phone width. Then remove one decoration that does not serve the screen. Fix, and re-preview what you changed; code refuses the answer if a view is missing. Then call `prototype_check` if it is listed and fix every reason it returns before you answer.
- Answer with one short sentence once the files are written.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading the ask and the screens it touches (25, "ask read"), once every screen to add or edit is written (55, "screens written"), and last, when you start previewing (70, "previewing the changes"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
