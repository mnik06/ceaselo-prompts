## Design rules

The prototype is the UI source of truth: it must look like the shipped product, and once approved the tickets are built to it and the real app's theme is generated from the same design system.

### Always

- **One design system, used everywhere.** Screens are built from the vocabulary's classes and the system's tokens; a screen's own `<style>` adds only what that screen needs. Edges line up on one grid; spacing follows the system's scale.
- **Hierarchy through size, weight and space.** One `h1` per screen; a clear reading order; secondary text quieter (`--text-muted`), not a new colour.
- **AA contrast.** Body text and controls at least 4.5:1 against what is behind them, large text 3:1. The system's tokens are contrast-checked; keep to their pairings (`--accent-ink` on `--accent`, `--accent-text` on surfaces).
- **Visible focus.** Every interactive element is a real `<a href>`, `<button>`, form control or `<summary>`, never a clickable `div`.
- **44 px tap targets** for anything tappable on a mobile screen.
- **One primary action per view**, worded as a verb plus object ("Send invoice", not "Submit").
- **Real domain copy and data.** Labels, help, errors and empty states use the product's own nouns and the brief's voice; sample data looks like the client's real records: full lists (15–25 rows) with varied lengths, edge values, every status, relative and absolute dates, totals that add up across screens.
- **Every state designed.** Each state the plan lists (empty, loading, error, partial, permission-limited, success) is a composed screen with its message and next step, never a blank region or a lone spinner. Forms show inline validation with specific error text, a busy button while saving, a confirmation for destructive actions.
- **Semantic structure.** Landmarks (`header`, `nav`, `main`, `aside`), labelled form controls, table headers, `aria-current` on the current nav item, `aria-label` on icon-only controls.
- **Colour never carries meaning alone**: pair it with a label or an icon.
- **A mobile product is designed for the phone first**: bottom navigation or clear back navigation, lists instead of wide tables, thumb-reachable primary actions.

### Never

- A colour, font, size, radius, shadow or spacing value that is not a `var(--…)` token; an `@font-face` or `@import`; an external URL, web font, remote image or CDN script.
- Emoji as icons or labels in buttons, links, nav items, tabs or headings.
- "Lorem ipsum", "Item 1", "John Doe", "Acme" or other filler.
- Fake charts made of boxes or characters: draw real proportions from the sample data (`.bars`, `.meter`, inline SVG on tokens), or show a table.
- Styling the prototype chrome (`[data-prototype-controls]`, any `.pk-*` class), or restyling a vocabulary class into a different component.
