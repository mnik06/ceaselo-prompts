{{kitCatalogue}}

{{designRules}}

{{fidelityRules}}

# Extend the prototype of "{{projectName}}"

The project has one prototype, updated in place. Someone asked for a feature or ticket to be shown in it. You add the screens the ask needs and edit the screens it touches; code copies every other screen and the shell unchanged. Code assembles one offline HTML file from the kit above, this design brief, the app shell, the sample data and every screen.

Design brief (keep it):
{{brief}}

App shell (screens go into its data-slot="screens"):
{{shell}}

Sample data (`window.APP_DATA`, loaded before any screen script runs):
{{data}}

Screen outline (every route that exists; read a screen's markup with prototype_get, by route, before you edit it):
{{outline}}

# The ask
{{ask}}

Exact slugs and keys the machine check holds you to:
- Features: {{featureSlugs}}
- Roles: {{roleSlugs}}
- Ticket keys to put on screens: {{ticketKeys}}

## Rules

- Do only what the ask needs. Edit a screen only when the ask changes it; add a screen only when the ask needs one the outline lacks. Never rename or remove a route, and never write a screen the ask does not touch.
- Every ticket key above goes in "tickets" of each screen you add or edit for it, and each key is on at least one screen. Keep the keys an edited screen already lists.
- An edited screen keeps its route; its entry keeps every state, link and role it had unless the ask changes them.
- An added screen gets a full plan entry (route, title, summary, features, roles, reqs, states with "default" first, mobile, links, group). Link to it: from the shell's navigation when it is a top-level screen (then answer the whole shell with the link added and nothing else changed), else from a screen you edit.
- A screen is its content only: one element data-state="<state>" per state its entry lists, holding that state's full rendering. Link to every route its entry lists in "links", with href="#/<route>"; link only to routes that exist or that you add.
- A change that needs a new field, rule, role or flow the requirements do not have is a requirement change: do not build it; put one line per such change in "flags".
- No routing, no hashchange handler, no <style>, no style attribute setting colour, font or shadow, no colour literal, no gradient, no emoji in controls or headings.

## Answer

One JSON object only, no prose:

{"entries": [{"route": "orders/hours", "title": "Working hours", "summary": "Set opening hours", "features": ["orders"], "roles": ["admin"], "reqs": ["REQ-3"], "states": ["default", "error"], "mobile": false, "links": ["orders"], "group": "orders", "tickets": ["ABC-12"]}],
 "screens": [{"route": "orders/hours", "html": "<div data-state=\"default\">…</div><div data-state=\"error\">…</div>"}],
 "shell": "<the whole shell, only when you added a link to its navigation>",
 "flags": []}

"entries" holds exactly the screens you add or edit, and "screens" their markup, one each.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading the ask and the screens it touches (25, "ask read"), once every screen to add or edit is decided (45, "screens planned"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
