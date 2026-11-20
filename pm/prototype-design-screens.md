{{designKit}}

{{designMethod}}

{{designRules}}

{{designSystem}}

# The prototype of "{{projectName}}"

Code assembles one offline HTML file from the design system, the app shell, the sample data and every screen of the plan. They are fixed and are in your workspace; you write screens.

Design brief:
{{brief}}

App shell (`shell.html`; screens go into its data-slot="screens"):
{{shell}}

Sample data (`data.js`, `window.APP_DATA`, loaded before any screen script runs):
{{data}}

Screen plan (every route that exists):
{{plan}}{{reference}}

# Your job: these screens

{{routes}}

Requirements these screens show (read any other with kb_get):
{{requirements}}

## Rules

- Write each screen as `screens/<route>.html`: one element data-state="<state>" per state its plan entry lists, holding that state's full rendering (default first: a populated, realistic view), every other state `hidden`.
- Build from the vocabulary's classes (`system/guide.md`); a screen's own `<style>` (one, at most 8 KB) adds only what this screen needs, every value a token, and never restyles a vocabulary class.
- Link to every route the entry lists in "links", with href="#/<route>"; link only to planned routes. Flows are clickable end to end.
- Forms show their validation: required fields, formats and limits from the spec, field-level errors with real copy (aria-invalid).
- Show each role what the spec says it sees (data-only-roles, data-hide-roles).
- Take every action label, toast, entity name and empty or error line from `APP_DATA.copy`; a word you need that it lacks follows its pattern.
- Preview every state of every screen above at its viewports with `prototype_preview` (6 views per call) and judge each view as its user would: does it lead with the screen's one job; is there one primary action; does any state read as empty or broken; is there a generated-page tell (identical cards for everything, an all-caps label above every heading, middle-dot meta, an accented headline word, "→" on links); does anything clip, crowd or misalign at the phone width. Then remove one decoration that does not serve the screen. Fix, and re-preview what you changed; code refuses the answer if a view is missing. Then call `prototype_check` if it is listed and fix every reason it returns before you answer.
- Any part of your brief that asks for a new field, rule, role or flow the spec does not have goes in `flags.json` instead of being built.
- Answer with one short sentence once the files are written. Write exactly the routes above.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading what these screens show (20, "requirements read"), once every screen file is written (50, "screens written"), and last, when you start previewing (70, "previewing the screens"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
