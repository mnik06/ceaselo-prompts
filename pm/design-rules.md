## Design rules

The prototype must look like a real, shipped product built by a careful team, not like generated filler. Every rule below is checked on the rendered screens.

### Never

- Gradients, glassmorphism, frosted or blurred panels, glows, neon.
- Emoji as icons or decoration; use kit icons, and only where they help recognition.
- A purple-to-blue or any default "AI" palette; colour comes from the brief's tokens only.
- A centred marketing hero on an app screen; app screens start with the page header and the work.
- Card soup: every block in its own card, cards inside cards, dashboards of identical tiles with nothing to act on.
- Decorative blobs, waves, illustrations, background patterns, fake 3D.
- Generic copy: "Welcome back!", "Unlock the power of…", "Get started today", "Lorem ipsum", "Item 1", "John Doe", "Acme".
- Fake charts drawn from boxes or characters; use `.bars` or `.meter` with proportions from the sample data, or a table.
- Pills and large radii on everything; let the brief's radius decide.
- Colour as the only carrier of meaning; pair it with a label or an icon.
- More than one primary button in a view.

### Always

- **Hierarchy through size and weight, not colour.** One `h1` per screen; secondary text is `.muted`, not a new colour.
- **One alignment grid.** Edges line up across header, toolbar, content and footer; spacing comes only from the kit's layout utilities and gap modifiers.
- **Readable line length.** Body text stays within 65 characters per line (`p` is capped; use `.measure` for other long text).
- **Tabular numbers in data.** Amounts, counts, dates and IDs in tables and stats use `.num` columns, right-aligned when numeric.
- **AA contrast.** Keep text on the kit's surfaces; never place text on an accent area other than `.btn--primary` and `.badge`.
- **Visible focus.** Every interactive element is a real `<a href>`, `<button>`, form control or `<summary>`; never a clickable `div`.
- **44 px tap targets on mobile.** Use kit controls for anything tappable; do not shrink them.
- **One primary action per view**, placed in the page header actions or the dialog footer, worded as a verb plus object ("Send invoice", not "Submit").
- **Real domain copy.** Labels, help text, errors and empty states use the product's own nouns and the brief's voice; errors say what happened and how to fix it.
- **Consistent iconography.** One icon per concept everywhere it appears; nav items either all have icons or none do.
- **Realistic data density.** Lists and tables show 8–25 believable rows with varied lengths, edge values and statuses; names, amounts and dates look like the client's real records.
- **Every state designed.** Empty, loading, error, partial and permission-limited states are composed screens with a next step, never a blank region or a lone spinner.
- **Semantic structure.** Landmarks (`header`, `nav`, `main`, `aside`), labelled form controls, table headers, `aria-current` on the current nav item, `aria-label` on icon-only controls.
