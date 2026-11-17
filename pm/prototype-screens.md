{{kitCatalogue}}

{{designRules}}

{{fidelityRules}}

# The prototype of "{{projectName}}"

Code assembles one offline HTML file from the kit above, this design brief, the app shell, the sample data and every screen of the plan. The brief, shell, data and plan are fixed; you write screens.

Design brief:
{{brief}}

App shell (screens go into its data-slot="screens"):
{{shell}}

Sample data (`window.APP_DATA`, loaded before any screen script runs):
{{data}}

Screen plan (every route that exists):
{{plan}}

# Your job: these screens

{{routes}}

Requirements these screens show (read any other with kb_get):
{{requirements}}

## Rules

- Write each screen's content only: one element data-state="<state>" per state its plan entry lists, holding that state's full rendering (default first: a populated, realistic view; empty with its call to action; loading as skeletons; error with a retry). Code wraps it with its route and coverage attributes.
- Link to every route the entry lists in "links", with href="#/<route>"; link only to planned routes. Flows are clickable end to end: create → list → detail → edit → delete behind a confirmation dialog.
- Forms show their validation: required fields, formats and limits from the spec, field-level errors with real copy (aria-invalid and .field__error).
- Behaviour a screen needs (filtering a list, re-rendering after a create) goes in one inline <script> per screen that registers `window.__prototype.onShow(function (view) { … })`; view has route, state, role and params. Read data from `window.APP_DATA`. No routing, no hashchange handler, no <style>, no style attribute setting colour, font or shadow, no colour literal.
- Show each role what the spec says it sees (data-only-roles, data-hide-roles).
- Answer with one JSON object only, no prose: {"screens": [{"route": "<route>", "html": "…"}], "flags": []}. Write exactly the routes above, each once. Put in "flags" any part of your brief that asks for a new field, rule, role or flow the spec does not have, instead of building it.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading what these screens show, before you plan them (20, "requirements read"), once every screen's content and layout are decided (45, "screens planned"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
