Write the full description and acceptance criteria of these tickets of "{{projectName}}". The work breakdown is already decided: titles, scope, dependencies and estimates stay as they are. Your job is to make every ticket complete enough that the Architect, the builders and the verifier need nothing else.

## The product's surfaces

{{platform}}

## Your tickets

Each ticket with its surface, its feature, the requirement keys it delivers, the prototype screens it builds, the tickets it depends on, and, from the dependency graph, the screens that exist when it lands and the screens not built yet with the ticket that builds each. A criterion of a ticket only reaches screens that exist when it lands; one that needs a screen not built yet is written on the ticket that builds that screen.

{{tickets}}

## The rest of the breakdown

Other tickets of the project, for context only: name them under Out of scope when they deliver something a reader might expect here. Dependencies are already the ticket graph; do not restate them.

{{otherTickets}}

## Requirements your tickets deliver, in full

Every rule, flow, state, validation, edge case and empty state in these bodies ends up in a ticket's description and criteria. A requirement shared by several of your tickets is divided between them: each ticket carries the part it delivers.

{{requirements}}

## Screens your tickets build

{{screens}}{{note}}

A Foundation ticket, when it is yours, is written like every other, for its own surface as its title says, never the technology behind it. A GUI surface's Foundation: what a person can open, see and reach once it runs, and its UI and states describe that surface's prototype app shell as the prototype has it (read it with `prototype_get` screen "shell" for the primary surface, "shell:<surface id>" for another: the header, every navigation item in order with its label, the active item, the screen it opens on), its criteria checking them; the shell is taken from the prototype, never invented. A CLI's Foundation: it installs and prints its help. An API's: it answers its first call. A library's: it installs and its entry point imports.

Write every ticket in its own surface's terms (the platform block above): a ticket on a surface with no web or PWA target never mentions a browser, a tab, an address or URL, a page reload, developer tools or the Tab key.

Read anything else you need with kb_search, kb_get and doc_section (decisions, assumptions, the Project Spec). Do not rely on memory of other tickets' content.

{{scopeRule}}

{{ticketRules}}

{{acLibrary}}

## Checked by machine

The answer is refused, with the reasons, when a ticket of yours is missing or a ticket that is not yours appears, a dev ticket's description lacks one of the eight headings or exceeds 12,000 characters, a dev ticket has no criterion, a dev ticket with effortScore 20 or more has fewer than 3, a dev ticket with screens has no `(standing: ui)` criterion, a ticket has more than 40 criteria, or a ticket on a surface with no web or PWA target mentions a browser, a tab, an address or URL, a page reload, developer tools or the Tab key (the reason names the phrase).

Answer with one JSON object `{"tickets":[{"ref":"...","description":"...","ac":["..."]}]}` covering exactly your tickets, and nothing else.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading your tickets' requirements and screens (20, "requirements read"), once every ticket's content is decided (45, "tickets planned"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
