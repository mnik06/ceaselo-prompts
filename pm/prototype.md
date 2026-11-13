Build the clickable, low-fidelity prototype of "{{projectName}}" as ONE self-contained HTML file. It is the client's first look at the product and, once approved, the UI source of truth the tickets are built from: every in-scope feature, every role and every state the spec describes must be on screen.

Project Spec outline (read any section with doc_section):
{{specSections}}

In-scope (MVP) requirements, by feature:
{{spec}}

Roles:
{{roles}}

Features not in the MVP (show none of their screens):
{{scope}}

Other decisions:
{{decisions}}{{requestedChange}}

Exact slugs the machine check holds you to:
- MVP features (data-features): {{featureSlugs}}
- Roles (data-roles): {{roleSlugs}}

## How to work

1. Read the requirements above; read the full body of any requirement listed by title only (kb_get), and any Project Spec section you need (doc_section).
2. Plan the screen map before writing markup: for each MVP feature, the screens its flows need (list, detail, create, edit, settings, confirmation, empty first-run …), which roles use each one, which REQ keys it shows, and which states it has. Cover the spec's Main flow, Alternate flows, States, Validation and errors, Empty states and Permissions of every requirement. A role that may not do something sees it disabled, hidden or refused, as the spec says.
3. Build the file from that map.
4. Self-check against every rule below before you answer, and fix what fails.

## What the prototype shows

- Complete coverage: every MVP feature appears on at least one screen and every role on at least one screen. Do not build features listed as not in the MVP.
- Clickable end to end: every flow can be walked with clicks, e.g. create → list → detail → edit → delete behind a confirmation dialog, sign-in → home, and the list reflects what was created or deleted in the session (keep the sample data in a JS array and re-render).
- Forms show their validation: required fields, formats and limits from the spec; submitting an invalid form shows field-level error messages with real copy; a failed save keeps what was typed.
- Realistic sample data: plausible names, dates, amounts and statuses in the project's domain; at least one very long value (a 120-character name, a long email) to show wrapping and truncation; lists with many rows (25+) and pagination or scrolling where the spec expects volume.
- Real copy for labels, empty states, errors and confirmations. Low fidelity: neutral greys, one accent colour, system font, no brand polish, no images other than inline SVG or data: URIs.
- Navigation: a persistent menu or tab bar reaches every top-level screen; detail screens have a way back.

## Screens (checked by machine)

Every screen is one element carrying all of these attributes:
- data-screen="<route>": kebab-case route; navigation uses hash links href="#/<route>", and the page shows the screen whose route matches location.hash (the first screen when the hash is empty). Detail screens may read an id after the route (#/order?id=3) but the data-screen value stays the route.
- data-title="<screen name>" and data-summary="<one line: what the user does here>".
- data-features="<slug> …": the MVP feature slug(s) the screen serves, from the list above only.
- data-roles="<slug> …": the role slug(s) that use the screen, from the list above only.
- data-reqs="REQ-n …": the requirement keys the screen shows (may be empty for a pure navigation screen); only keys that exist.
- data-states="default …": always default, plus every one of empty, loading, error that can happen on that screen (a list has empty and loading; a form has error; a static page may have only default). Add other states the spec names (e.g. read-only, locked, offline) as kebab-case words.

Inside each screen, every state it lists is one child element with data-state="<state>" holding that state's full rendering: the empty state with its call to action, a loading skeleton, an error with a retry. Exactly one state is visible at a time; default is visible first.

A mobile screen also carries data-device="mobile" and is drawn inside a phone frame (rounded bezel, notch, about 390px wide) centred on the page. Desktop screens must still not overflow a 390px viewport horizontally.

## The prototype control bar (checked by machine)

One floating bar, fixed to a corner, with data-prototype-controls on its element. It is clearly prototype chrome, not part of the product: dashed outline, a small "Prototype" label, a distinct colour, collapsible so it never hides content for good. It holds, as static markup inside the bar:
- a role switcher with one option or button per role slug above (value or data-role set to the slug, label the role name); switching the role changes what the screens show (menu items, actions, read-only fields) as the spec's permissions say;
- a state switcher with one option or button per state used on any screen (default, empty, loading, error, …); it shows that state on the current screen, falling back to default where the screen does not list it.

The current role and state survive navigation between screens.

## File rules (checked by machine)

- One complete HTML document (<!doctype html><html> … </html>), at most 2 MB. Inline all CSS, JS and data.
- No external URL anywhere: no src or href to http(s) or relative files, no @import, no url() other than data: URIs, no <meta http-equiv="refresh">, no srcdoc.
- At most 200 screens: a variation that differs only by state or role is a state or role, not a screen.

## Before you answer

Walk your file and confirm: every MVP feature slug appears in some data-features; every role slug in some data-roles; every screen has all seven data-* attributes and lists default; every listed state has its data-state element inside that screen; every data-reqs key is a real key; the control bar has every role and every state; every link target exists. Fix anything that fails.

Answer with the HTML document only.{{rejected}}
