{{kitCatalogue}}

{{designRules}}

{{fidelityRules}}

# Fix screens of the prototype

Code assembles one offline HTML file from the kit above, this design brief, the app shell, the sample data and every screen of the plan. A review rendered the screens below and found the problems listed with them. Rewrite these screens so every major finding is resolved, and the minor ones too where the same change covers them.

Design brief:
{{brief}}

App shell (screens go into its data-slot="screens"):
{{shell}}

Sample data (`window.APP_DATA`, loaded before any screen script runs):
{{data}}

Screen plan (every route that exists):
{{plan}}

# The screens to fix

Their plan entries:
{{routes}}

Their current markup:
{{screens}}

What the review found (route, state, viewport, kind, severity, element, note):
{{findings}}

## Rules

- Change what the findings name and what it takes to resolve them; keep everything else of the screen as it is: its copy, data, links and states. A fixed screen that brings a new problem is thrown away and the old one kept.
- Kinds: contrast (text below WCAG AA on its background: keep text on the kit's surfaces), overflow (the page scrolls sideways: let tables scroll inside `.table-wrap`, let rows wrap, never fix a width), clipped (text cut off by its box: let it wrap or truncate it with `.truncate`), overlap (two controls on top of each other), console (a script error: fix or remove the script), design (the reviewer's note).
- Write each screen's content only: one element data-state="<state>" per state its plan entry lists, holding that state's full rendering. Code wraps it with its route and coverage attributes.
- Link to every route the entry lists in "links", with href="#/<route>"; link only to planned routes.
- No routing, no hashchange handler, no <style>, no style attribute setting colour, font or shadow, no colour literal, no gradient, no emoji in controls or headings.
- Answer with one JSON object only, no prose: {"screens": [{"route": "<route>", "html": "…"}], "flags": []}. Write exactly the routes above, each once.

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading the findings (25, "findings read"), once every fix is decided (45, "fixes planned"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
