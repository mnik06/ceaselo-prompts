## How a ticket is written

**The measure of a ticket is completeness.** The Architect plans it, builders implement it and a verifier checks it with the ticket and the repository in front of them and nothing else. A requirement that is not in the ticket is never built; an edge case nobody wrote down ships as a bug; a criterion that is not written is never checked. Write every ticket so that someone who never saw the Project Spec, the prototype or the other tickets can build exactly the right thing from it.

### The description

Markdown, at most 12,000 characters, with these `##` headings in this order. Every heading is present; write "None." under one that truly has nothing, never drop it.

- `## Goal`: who gets what, and why it matters to them, in two to four sentences.
- `## Scope`: what this ticket delivers, as a bullet list of capabilities. Name the requirement keys each bullet delivers, for example "(REQ-12)".
- `## UI and states`: every screen, panel, dialog or email this ticket builds or changes, by its prototype route and name; for each, its regions and every state it can show (loading, empty, error, partial, read-only, success) and what each says. "None." for a ticket without UI.
- `## Data and API`: the records, fields, constraints and relationships it creates or changes, and the operations the UI calls with their inputs, outputs and refusals. Rules on data (uniqueness, required, ranges, lengths, defaults, what happens to existing rows) are stated here.
- `## Permissions`: every role and what it can see and do here, including what someone who cannot edit sees. Authorization is enforced by the server, not only hidden in the UI.
- `## Edge cases`: every edge, limit and failure case, one bullet each, with the expected behaviour. Draw them from the requirement bodies (alternate flows, validation and errors, edge cases, empty states) and add the ones the requirements missed.
- `## Out of scope`: what a reader might expect here but another ticket delivers (name its ref) or nobody builds (say why), and any standing criterion left out with its reason.
- `## Notes for the Architect`: dependencies on other tickets and what they provide, reuse, integration details, non-functional needs (performance, security, privacy, accessibility, locale), and the decisions already taken that constrain the build.

Paste, never reference. "As described in the spec" or "see REQ-12" in place of the content is a gap: write the rule, the message or the limit itself. Name requirement keys for traceability, in addition to the content, never instead of it.

### The acceptance criteria

`ac` is the binding checklist: the verifier checks the ticket against these sentences and nothing else.

- **One observable behaviour per criterion.** A criterion listing six fields, or a rule with its three exceptions, is several criteria. A sentence with "and" joining two checks is two criteria.
- **Drivable.** Ask of each one: could someone with this sentence and nothing else decide whether it holds? Name the role, the starting state, the action and what is seen. A state that is hard to reach says how it is reached. "Works correctly", "is user friendly", "handles errors" are not criteria.
- **Concrete.** State the actual rule, limit, message, order and destination: "A title longer than 120 characters is refused with 'Title is at most 120 characters'", not "the title is validated".
- **No duplicates.** Two sentences describing the same behaviour are one criterion: keep the sharper wording.
- **Cover the ticket.** Every bullet of Scope, every state in UI and states, every rule in Data and API and Permissions, and every bullet in Edge cases is checked by at least one criterion. Expect more criteria than the requirements state, never fewer.
- **Standing blocks pasted.** For every kind of surface the ticket builds, paste its standing block from the library below, rewritten in the ticket's terms, each criterion ending with `(standing: <block>)`. A ticket that builds any screen carries the `ui` block. Leave a standing criterion out only with a reason under Out of scope.
- Each criterion is at most 500 characters.
- A HITL ticket (a human task) has a description of what the human does and produces, and no criteria unless the hand-over itself can be checked.

### Three lenses

Before you finish each ticket, walk it through three lenses and add what is missing to the description and the criteria. The lists say where to look; skip what cannot apply.

- **Product:** every role and what each sees; every state and transition, including refusals and their wording; validation (required, formats, ranges, uniqueness, max length); empty, missing, not found and deleted references; volume (a hundred rows, ten thousand, a very long value); two people editing one record; side effects on other screens and derived values; undo and destruction; deep links, reload and back; notifications; money, time, time zones and locale where relevant.
- **UI:** loading, empty, error, partial and read-only for every region; feedback on every action; a failed save never loses input; what survives a reload; long values and formats; keyboard and focus; narrow widths; the copy itself.
- **Architecture:** data constraints, authorization enforced by the server, error contracts, idempotency of anything retried, stale writes, pagination and volume, integrations and their failure modes, privacy and retention.

Do not invent product rules the requirements contradict. Where the requirements are silent and one answer is clearly right, write it in; where they are silent and the choice is a real fork, take the conservative option, write it under Notes for the Architect as an assumption, and keep the criterion.
