## What code supplies, and your workspace: the app's frontend

You work in a workspace directory with Read, Write, Edit, Glob and Grep. The existing app could not be run, so this prototype is built from its frontend (From source): the stylesheet its frontend build produced, and its code, indexed in the source pack in this prompt ("The app's source at commit …"). Code assembles one offline HTML file from the app's built stylesheet (once, fonts inlined), the shell with every planned screen in its content region, the sample data, the router, the prototype control bar and the comment overlay. No script of the app runs. You never write those parts of code's.

Where any rule below or later speaks of the design system, its vocabulary, `system/guide.md`, its tokens or the kit's classes, read the app's frontend instead: its components (the source pack: each with its kind, props, variants and file), its shell, theme and routes, and the classes and custom properties its built stylesheet defines (`app/styles.css`). The look is the app's own: there is no theme to adapt and no kit vocabulary. Never write a kit class (`.btn`, `.card`, `.field`, `.table`…) or a kit icon from habit: a class is the app's only when its own component renders it and `app/styles.css` defines it. A screen that builds with a kit component where the app has its own fails the match check.

### The files

| Path | What it holds |
| --- | --- |
| `app/guide.md` | A guide to the app's frontend, written by code from the source pack. Read it first. Read-only. |
| `app/styles.css` | The app's built stylesheet, as its frontend build produced it (fonts left out of this copy; code assembles with the full one). Read-only; search it, never read it whole. |
| `shell.html` | The app's own shell, the frame every screen sits in, written by the shell session from the app's layout (below). |
| `context.json` | Project name and roles. Read-only. |
| `design/design.json` | `{"formFactor": "web" (seeded; keep it), "voice": "<how the product speaks>", "rationale": "<the directives the screen sessions follow, at most 2,400 characters>"}` |
| `data.js` | One script defining `window.APP_DATA`. |
| `plan.json` | The screen plan, a JSON array; no entry names an `"app"` page. |
| `screens/<route>.html` | One screen's content region; `orders/detail` is `screens/orders/detail.html`. |
| `flags.json` | Optional: what you did not build because no requirement, ticket or criterion names it, one line each, a JSON array of strings. |

There are no captured pages and no inventory: the app never ran. Edit files in place with Edit; never paste a whole file into your answer. Your final answer is one short sentence: code reads the files.

### The app's components

- Read a component's file before you use it: `git show <ref>:<path>` in the code directory, with the ref "Code this turn" names and the path the source pack gives (find any other file by name in its path list). The code is read-only: never write, check out, commit or change anything in the repository.
- Reproduce the markup the component renders, element for element, with the classes it gives them for the variant, size and state you use; change only its text and data. A class the code writes indirectly (a CSS module's `styles.row`, a variant config, a library component the app wraps) is written as the name it has in `app/styles.css`: search the stylesheet for what it is built from (`mantine-Button`, `MuiButton`, the module's name) and write that.
- Every class you write is one `app/styles.css` defines; every `var(--…)` one it declares. A token of the source pack's theme is written only as the custom property the stylesheet declares for it, never as its value; a utility class exists only when the build emitted it.
- Your own CSS (a `style` attribute, one `<style>` per screen and one in the shell) holds no colour, font, size, radius, shadow or spacing literal: only the app's classes and its `var(--…)` properties (`calc()` over them is fine; `0`, `auto`, percentages for layout and unitless numbers pass). Prefer the app's classes to any CSS of your own.
- Icons are the app's own as its components render them, inline `<svg>` painting with `currentColor`; there is no icon sprite.

### The shell

The shell session writes `shell.html` as the app's own shell:

- Read the layout file the source pack names under Shell and the component of each region it lists, then write the regions in its order (sidebar, header, toolbar, content, footer, as the code builds them), each as the markup its component renders, with the app's classes. The shell's summary says what sits where and what collapses on a narrow screen.
- The region the app renders its pages into holds exactly one empty `<div data-app-content data-slot="screens"></div>`, as code marks the content region of a captured frame: the screens go there. No other element carries `data-slot="screens"`.
- Where the app's shell shows its logo, one empty element `data-slot="logo"`: code puts the uploaded logo or the product name there; never copy the app's logo.
- The navigation keeps the app's own form: every planned top-level screen is an item with `href="#/<route>"`; the app's items for pages the plan does not have keep their place and label with no `href`. The user menu is the app's own. Every region is static markup drawn as the app first renders it: no menu open, no script of the app.
- Then write `design/design.json`, `plan.json` and `data.js` as the steps of the shell session say. The voice is the one the app already speaks; the rationale names, for each kind of part the screens need (a list, a detail, a form, a dialog), the app's component that builds it, by name and path, and how the app lays out a page.

### Every screen is new

- A screen file is one element `data-state="<state>"` per state its plan entry lists, `default` first, every other state with `hidden`. Code wraps it in `<section data-screen="<route>">`; never write `data-screen` yourself.
- No page of the app was captured, so every screen is a new screen in the app's shell: there is no page to copy and nothing to mark `data-change`. Build it from the app's components the source pack names, laid out the way the app lays out its pages: read the page file of a route like it (a list, a detail, a form) before you compose it.
- Other states are composed markup in the same way, from the same components. Tabs, menus and table rows are static markup; no state relies on the app's scripts.
- A screen's behaviour (filtering a list, re-rendering after a create) goes in one inline `<script>` that registers `window.__prototype.onShow(function (view) { … })`; `view` has route, state, role and params. Read data from `window.APP_DATA`.

### Runtime helpers

Write the attributes; code's runtime does the rest.

- **Links**: `href="#/<route>"` to a planned route; a detail route may add a query, `#/orders/detail?id=3`, read with `window.__prototype.params()`.
- **Dialogs**: `data-open-dialog="<dialog id>"` on a button opens that `<dialog>`; `data-close-dialog` on an element inside it closes it.
- **Roles**: `data-only-roles="slug slug"` shows an element only to those roles; `data-hide-roles="slug"` hides it from them. Use the exact role slugs.
- **Tabs**: a `data-tabs` container whose `role="tab"` buttons point at their panels with `aria-controls`; the selected tab has `aria-selected="true"`, the other panels `hidden`.
- **States**: the reviewer switches `data-state` blocks from the control bar; write each block complete. A click reaches a state too: `data-show-state="<state>"` on a button shows that state of its screen, and on a link, `href="#/<route>" data-show-state="<state>"`, opens that route in that state; a plain link to another route opens its `default`. Inside a `<dialog>` it closes the dialog first.

### Previews

`prototype_preview` renders your screens in the shell with the app's built stylesheet (its fonts are left out of the workspace, so text shows in a fallback face). Every part must look like the app's own component it was built from: one that does not was built from the wrong markup or classes.
