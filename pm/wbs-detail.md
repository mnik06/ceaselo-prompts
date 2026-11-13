Write the full description and acceptance criteria of these tickets of "{{projectName}}". The work breakdown is already decided: titles, scope, dependencies and estimates stay as they are. Your job is to make every ticket complete enough that the Architect, the builders and the verifier need nothing else.

## Your tickets

Each ticket with its feature, the requirement keys it delivers, the prototype screens it builds and the tickets it depends on:

{{tickets}}

## The rest of the breakdown

Other tickets of the project, for context only: name them under Out of scope when they deliver something a reader might expect here, and under Notes for the Architect when yours depends on them.

{{otherTickets}}

## Requirements your tickets deliver, in full

Every rule, flow, state, validation, edge case and empty state in these bodies ends up in a ticket's description and criteria. A requirement shared by several of your tickets is divided between them: each ticket carries the part it delivers.

{{requirements}}

## Screens your tickets build

{{screens}}{{note}}

Read anything else you need with kb_search, kb_get and doc_section (decisions, assumptions, the Project Spec). Do not rely on memory of other tickets' content.

{{ticketRules}}

{{acLibrary}}

## Checked by machine

The answer is refused, with the reasons, when a ticket of yours is missing or a ticket that is not yours appears, a dev ticket's description lacks one of the eight headings or exceeds 12,000 characters, a dev ticket has no criterion, a dev ticket with effortScore 20 or more has fewer than 3, a dev ticket with screens has no `(standing: ui)` criterion, or a ticket has more than 40 criteria.

Answer with one JSON object `{"tickets":[{"ref":"...","description":"...","ac":["..."]}]}` covering exactly your tickets, and nothing else.{{rejected}}
