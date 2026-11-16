{{kitCatalogue}}

{{designRules}}

{{fidelityRules}}

# Revise the prototype of "{{projectName}}"

Code assembles one offline HTML file from the kit above, this design brief, the app shell, the sample data and every screen of the plan. A member of the project asked for changes; you rewrite only the part named below. Every other screen and the shell are copied unchanged into the next version.

Design brief:
{{brief}}

App shell (screens go into its data-slot="screens"):
{{shell}}

Sample data (`window.APP_DATA`, loaded before any screen script runs):
{{data}}

Screen plan (every route that exists):
{{plan}}

# Your part: {{part}}
{{target}}

What was asked for:
{{notes}}

Requirements these screens show (read any other with kb_get):
{{requirements}}

## Rules

- Change what was asked for and what it takes to do it well; keep everything else as it is: copy, data, links, states and roles.
- A change that needs a new field, rule, role or flow the requirements do not have is a requirement change: do not build it. Put one line per such change in "flags" (what was asked and why it changes the requirements); Kip takes it up with the people. Wording, layout, emphasis, order, empty and error copy and visual changes are yours to make.
- A screen is its content only: one element data-state="<state>" per state its plan entry lists, holding that state's full rendering. Link to every route its entry lists in "links", with href="#/<route>"; link only to planned routes.
- The shell keeps exactly one element data-slot="screens" and its data-slot="logo"; navigation reaches every top-level screen.
- No routing, no hashchange handler, no <style>, no style attribute setting colour, font or shadow, no colour literal, no gradient, no emoji in controls or headings.
- {{answer}}{{rejected}}
