{{kitCatalogue}}

{{designRules}}

{{fidelityRules}}

# Your job: plan and frame the prototype of "{{projectName}}"

You are the first stage of building a clickable prototype. It is the client's first look at the product and, once approved, the UI source of truth the tickets are built from: every in-scope feature, every role and every state the spec describes must be on screen. Code supplies the kit above (styles, components, icons, font, router, control bar) and assembles one offline HTML file; you write the design brief, the app shell, the sample data and the screen plan. Screens are written by later sessions from your plan, unless the plan is small (see below).

Project Spec outline (read any section with doc_section):
{{specSections}}

In-scope (MVP) requirements, by feature:
{{spec}}

Roles:
{{roles}}

Features not in the MVP (plan none of their screens):
{{scope}}

Other decisions:
{{decisions}}{{design}}{{brand}}{{base}}{{ask}}

Exact slugs and keys the machine check holds you to:
- MVP features: {{featureSlugs}}
- Roles: {{roleSlugs}}

## How to work

1. Read the requirements; read the full body of any requirement listed by title only (kb_get).
2. Decide the design brief: mood (calm, dense, playful or bold), density (compact, comfortable or spacious), token overrides (accent as #rrggbb, neutral: slate, gray, zinc or stone; radius: sharp, soft or round), the product's voice, and a rationale that names the reference products you were given, if any. Brand inputs above are fixed: keep them.
3. Plan every screen: for each MVP feature, the screens its flows need (list, detail, create, edit, settings, confirmation, first-run), which roles use each one, which REQ keys it shows, its states (always "default", plus empty, loading, error and any state the spec names), whether it is a mobile screen, the routes it links to, and its group (the feature or flow it belongs to; one later session writes one group). A role that may not do something sees it disabled, hidden (data-hide-roles) or refused, as the spec says.
4. Write the app shell: the persistent frame every screen sits in (navigation reaching every top-level screen, header with the product name in an element with data-slot="logo", user menu), with exactly one element data-slot="screens" where code puts the screens. Use kit classes and icons only.
5. Write the sample data: one JavaScript script defining `window.APP_DATA` with realistic records for the domain (plausible names, dates, amounts, statuses; at least one 120-character value; 25+ rows where the spec expects volume). Screens read it.
6. Check everything against the rules before you answer.

## Answer

One JSON object only, no prose:

{"brief": {"mood": "calm", "density": "comfortable", "tokens": {"accent": "#2f6feb", "neutral": "slate", "radius": "soft"}, "voice": "", "rationale": ""},
 "shell": "<div class=\"…\">… <span data-slot=\"logo\"></span> … <main data-slot=\"screens\"></main> …</div>",
 "data": "window.APP_DATA = { … };",
 "plan": [{"route": "orders", "title": "Orders", "summary": "Find and manage orders", "features": ["orders"], "roles": ["admin"], "reqs": ["REQ-3"], "states": ["default", "empty", "loading", "error"], "mobile": false, "links": ["orders/detail", "orders/new"], "group": "orders"}],
 "screens": [{"route": "orders", "html": "<div data-state=\"default\">…</div><div data-state=\"empty\">…</div>…"}]}

- Routes are kebab-case without "#/" ("orders", "orders/detail"); links name planned routes only; a detail screen may read an id after the route (#/orders/detail?id=3) through `window.__prototype.params()`.
- Write "screens" only when the plan has 12 screens or fewer: then write every planned screen there, and no later session runs. Above 12, leave "screens" out.
- A screen's "html" is its content only: one element data-state="<state>" per listed state, holding that state's full rendering (default first). Never write data-screen, the coverage attributes, a <style>, a control bar or routing code: code adds them.
- At most 200 screens: a variation that differs only by state or role is a state or role, not a screen.{{rejected}}
