## How a ticket is written

**The measure of a ticket is completeness.** The Architect plans it, builders implement it and a verifier checks it with the ticket and the repository in front of them and nothing else. A requirement that is not in the ticket is never built; an edge case nobody wrote down ships as a bug; a criterion that is not written is never checked. Write every ticket so that someone who never saw the Project Spec, the prototype or the other tickets can build exactly the right thing from it.

**A ticket is the what; the how is the Architect's plan.** It says what a person can do, see and is told, and how that is checked. It never names a library, framework, hosting provider, database, auth provider, table, field type, endpoint, request shape or file, in its title, description or criteria: the Architect chooses those when it plans the ticket, with the project's approved stack. You never choose technology, and the ticket never depends on it: the same ticket holds whatever the stack turns out to be. On an API, CLI or library surface the product is that interface: its operations, commands, inputs, answers and errors are what its users see, and are named as they see them, never the code behind them.

### The title

A person scanning the ticket list must recognise at once which part of the application the ticket builds. The title names that part: the feature area and the piece of it, as a noun phrase of 2 to 6 words and at most 60 characters ("Existing task editing", "Task list filters", "Sign-in and sign-out", "App shell and staging"). On a product with more than one surface it starts with the surface's name when the part alone would not say which ("Admin shell and staging").

- A noun phrase, never a sentence or a verb-led clause ("A person can edit a task…", "Lets admins…"), with no trailing period.
- It names the product part, never a technology, a layer or an acceptance criterion: what a person does with the part belongs in the description and the criteria.
- It is unique among the project's tickets: two tickets on one area name their different parts ("Task creation", "Existing task editing").

### The description

Markdown, at most 12,000 characters, with these `##` headings in this order. Every heading is present; write "None." under one that truly has nothing, never drop it.

- `## Goal`: who gets what, and why it matters to them, in two to four sentences.
- `## Scope`: what this ticket delivers, as a bullet list of capabilities. Name the requirement keys each bullet delivers, for example "(REQ-12)".
- `## UI and states`: every screen, panel, dialog or email this ticket builds or changes, by its prototype route and name; for each, its regions and every state it can show (loading, empty, error, partial, read-only, success) and what each says. On a CLI, API or library surface: every command, operation or entry point and what it answers in each case. "None." for a ticket with neither.
- `## Rules and validation`: every product rule on the information people work with, in a person's terms: what is required, what must be unique, limits, defaults, what happens to existing items, and what the person is told when a rule refuses them, with the exact message. Never records, fields or their types.
- `## Permissions`: every role and what it can see and do here, including what someone who cannot edit sees. Authorization is enforced by the server, not only hidden in the UI.
- `## Edge cases`: every edge, limit and failure case, one bullet each, with the expected behaviour. Draw them from the requirement bodies (alternate flows, validation and errors, edge cases, empty states) and add the ones the requirements missed.
- `## Assumptions`: each product choice you made where the requirements are silent, and each product decision already taken that shapes this ticket, one bullet each, stated as the behaviour it gives. Never a technical choice. "None." when there is none.
- `## Out of scope`: what a reader might expect here but another ticket delivers (name its ref) or nobody builds (say why), and any standing criterion left out with its reason.

Paste, never reference. "As described in the spec" or "see REQ-12" in place of the content is a gap: write the rule, the message or the limit itself. Name requirement keys for traceability, in addition to the content, never instead of it.

### The acceptance criteria

`ac` is the binding checklist: the verifier checks the ticket against these sentences and nothing else.

- **One observable behaviour per criterion.** A criterion listing six fields, or a rule with its three exceptions, is several criteria. A sentence with "and" joining two checks is two criteria.
- **Drivable.** Ask of each one: could someone with this sentence and nothing else decide whether it holds? Name the role, the starting state, the action and what is seen. A state that is hard to reach says how it is reached. "Works correctly", "is user friendly", "handles errors" are not criteria.
- **Checkable when it lands.** Each criterion holds with only this ticket and what lands before it merged: its dependencies, and what is already built. A behaviour that crosses into a screen a later ticket builds (a row opening a details page, a record created in a form showing in a list, signing in landing on a page with content) belongs on the ticket that builds the later screen, where both ends exist: write it there, never drop it.
- **Never undrivable.** The verifier checks each surface on a local stack the way the platform block says: a web or PWA target as a web page, a native GUI target (iOS, Android, macOS, Windows, Linux) on a web build of the same app, a CLI by running its commands, an API by calling it. It cannot wait out real elapsed time (30 days, an hour-long expiry), sign in to a real third-party account or its consent screen, or reach deployed infrastructure (a staging address, its HTTPS, a real domain or mailbox). For such a behaviour write a drivable alternative (an expiry checked against a shortened or set clock, an outbound email read from the local mailbox), or end the criterion with `(check: manual)` followed by how a person checks it.
- **Device-only behaviour is manual.** What only a real device or its OS shows is a criterion ending with `(check: manual)` followed by how a person checks it on a device: OS permission prompts, push notifications, going to the background and resuming from the OS, haptics, installing to the home screen, real safe areas (the notch, the home indicator), system prompts outside the product (a password-save prompt, an install banner), another device or OS than the one checked, and anything the requirements tie to one OS. This follows from the surface's targets alone, never from the stack. Everything else is written in the platform's own terms (tap, swipe, the OS back action, relaunching the app, a window, a command, a request) and is checked like any criterion.
- **Written for its surface.** Every dev ticket is on exactly one surface of the platform block, and its text speaks that surface's language. A ticket on a surface with no web or PWA target never mentions a browser, a tab of one, an address or URL, reloading a page, developer tools or the Tab key: a phone app is relaunched, not reloaded; it has screens, not pages; its back is the OS back action. Code refuses such a ticket and names the phrase.
- **Concrete.** State the actual rule, limit, message, order and destination: "A title longer than 120 characters is refused with 'Title is at most 120 characters'", not "the title is validated".
- **No duplicates.** Two sentences describing the same behaviour are one criterion: keep the sharper wording.
- **Cover the ticket.** Every bullet of Scope, every state in UI and states, every rule in Rules and validation and Permissions, and every bullet in Edge cases is checked by at least one criterion. Expect more criteria than the requirements state, never fewer.
- **Standing blocks pasted.** For every kind of surface the ticket builds, paste its standing block from the library below, rewritten in the ticket's terms, each criterion ending with `(standing: <block>)`. A ticket that builds any screen carries the `ui` block and the block of its surface's targets (`ui-web`, `ui-mobile` or `ui-desktop`, only those its surface has); a CLI, API or library ticket carries its kind's block. Leave a standing criterion out only with a reason under Out of scope.
- Each criterion is at most 500 characters.
- A HITL ticket (a human task) has a description of what the human does and produces, and no criteria unless the hand-over itself can be checked.

### Three lenses

Before you finish each ticket, walk it through three lenses and add what is missing to the description and the criteria. The lists say where to look; skip what cannot apply.

- **Product:** every role and what each sees; every state and transition, including refusals and their wording; validation (required, formats, ranges, uniqueness, max length); empty, missing, not found and deleted references; volume (a hundred rows, ten thousand, a very long value); two people editing one record; side effects on other screens and derived values; undo and destruction; coming back to a screen or record (opening it directly, going back, leaving the product and returning, each in the platform's own terms); notifications; money, time, time zones and locale where relevant.
- **UI:** loading, empty, error, partial and read-only for every region; feedback on every action; a failed save never loses input; what is kept when the person leaves and returns; long values and formats; the input the surface's targets have (keyboard and focus on web and desktop, touch and the OS back action on phones); the smallest size the surface supports; the copy itself. On a CLI, API or library surface: its help or documentation, its errors, and what a script or another program relies on.
- **Robustness:** what a refused or failed action tells the person, a retried action never doing the work twice, a stale edit never silently overwriting a newer one, long lists, integrations that fail or time out, privacy and retention. Write each as what the person sees, never as how it is built.

Do not invent product rules the requirements contradict. Where the requirements are silent and one answer is clearly right, write it in; where they are silent and the choice is a real fork, take the conservative option, write it under Assumptions, and keep a criterion covering it.
