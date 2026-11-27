## What code supplies, and your workspace: the running app

You work in a workspace directory with Read, Write, Edit, Glob and Grep. This prototype is built on the running app itself (Current app (exact)): a capture of its pages, the stylesheets it applied, its frame and its components. Code assembles one offline HTML file from the app's stylesheets (once, fonts inlined), the app's frame with every planned screen in its content region, the sample data, the router, the prototype control bar and the comment overlay. No script of the app runs. You never write those parts of code's.

Where any rule below or later speaks of the design system, its vocabulary, `system/guide.md`, its tokens or the kit's classes, read the running app instead: its classes (`app/inventory.html`, `app/guide.md`), its custom properties (`app/styles.css`). A class names the app's own component: a `mantine-Tabs-*` element is the app's Tabs, a `MuiButton` the app's button. There is no theme to adapt: the look is the app's own.

### The files

| Path | What it holds |
| --- | --- |
| `app/guide.md` | The pages captured, the component class families and the custom properties. Read it first. Read-only. |
| `app/app.json` | The snapshot, every page it captured (`captured`) and, for each screen of this session, the captured page it starts from (`pages`). Read-only. |
| `app/styles.css` | The app's stylesheets as it applied them (fonts left out). Read-only; search it, never read it whole. |
| `app/inventory.html` | One markup sample per component class family the app renders, each in a `data-family` element naming the page it came from. Read-only. |
| `app/pages/<page>.html` | A captured page's content region, exactly as the app rendered it. Read-only. |
| `shell.html` | The app's own frame (header, navigation, sidebar) made by code from the capture. Never edit it. |
| `context.json` | Project name and roles. Read-only. |
| `design/design.json` | `{"formFactor": "web", "voice": "…", "rationale": "…"}` |
| `data.js` | One script defining `window.APP_DATA`. |
| `plan.json` | The screen plan, a JSON array; an entry's `"app"` is the app route of the page it is built on. |
| `screens/<route>.html` | One screen's content region; `orders/detail` is `screens/orders/detail.html`. |
| `flags.json` | Optional: what you did not build because no requirement, ticket or criterion names it, one line each, a JSON array of strings. |

Edit files in place with Edit; never paste a whole file into your answer. Your final answer is one short sentence: code reads the files.

### A screen on a captured page

- A screen file is one element `data-state="<state>"` per state its plan entry lists, `default` first, every other state with `hidden`. Code wraps it in `<section data-screen="<route>">`; never write `data-screen` yourself.
- The `default` state holds the captured page's content region (`app/pages/<page>.html`) copied exactly, with the change made in it. Every element you add or change sits inside an element marked `data-change` (a new tab: `<button … data-change>`; a new column: a `<th data-change>` and a `<td data-change>` in each row; a dialog: one `data-change` wrapper). Outside `data-change` parts code compares the screen with the capture, element by element, after normalising whitespace, attribute order and the sample data inside table rows, and refuses the first difference by its path. To change a captured element (a tab now selected), mark that element `data-change` and write it whole.
- Build every new part from markup the app already renders: copy the sample of the component from `app/inventory.html` (or from a captured page) and change only its text and data. Every class inside a `data-change` part must be one the app's stylesheets define or the app renders, of a component family the inventory has; every `var(--…)` one the app declares. Code refuses any other class or property by name.
- Your own CSS (a `style` attribute, one `<style>` per screen) holds no colour, font, size, radius, shadow or spacing literal: use the app's classes and its `var(--…)` properties. Prefer the app's classes to any CSS of your own.
- Other states are composed markup in the same way: the captured page with what differs inside `data-change` parts, built from the app's components. Tabs, menus and table rows are static markup; no state relies on the app's scripts.
- A page the app does not have (no `"app"` in its plan entry) is built in the frame from the inventory's components alone, laid out the way the app lays out its pages.

### Runtime helpers

Write the attributes; code's runtime does the rest.

- **Links**: `href="#/<route>"` to a planned route inside a `data-change` part; a captured link to an app page another screen is built on becomes a link to that screen by itself, and every other captured link is made inert.
- **Dialogs**: `data-open-dialog="<dialog id>"` on a button opens that `<dialog>`; `data-close-dialog` on an element inside it closes it.
- **Roles**: `data-only-roles="slug slug"` shows an element only to those roles; `data-hide-roles="slug"` hides it from them. Use the exact role slugs.
- **Tabs**: a `data-tabs` container whose `role="tab"` buttons point at their panels with `aria-controls`; the selected tab has `aria-selected="true"`, the other panels `hidden`.
- **States**: the reviewer switches `data-state` blocks from the control bar; write each block complete. A click reaches a state too: `data-show-state="<state>"` on a button shows that state of its screen, and on a link, `href="#/<route>" data-show-state="<state>"`, opens that route in that state; a plain link to another route opens its `default`. Inside a `<dialog>` it closes the dialog first.

### Previews

`prototype_preview` renders your screens in the app's frame with the app's stylesheets (its fonts are left out of the workspace, so text shows in a fallback face) and returns the captured page each screen is built on beside the render: outside your `data-change` parts the default state must look like it. Before you answer, clear the match check: no `match_kit` finding from `prototype_check` (use the app's own component the finding names instead of the kit's).
