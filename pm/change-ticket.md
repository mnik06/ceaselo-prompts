Write the ticket of a confirmed change to "{{projectName}}": its title, its full description and its acceptance criteria. The Architect, the builders and the verifier will work from this ticket alone.

## The product's surfaces

{{platform}}

## The change

{{summary}}

Effort score: {{effortScore}}. The change was grilled with the member before this card was confirmed: every decision above is settled. State each as a fact of the product in the description and turn each into acceptance criteria; never write "defaults", "assumed" or "unless you say otherwise", and never reopen a decision.

## Requirements of the project (key: title)

{{requirements}}

Read the requirements, decisions and screens this change touches in full with kb_search, kb_get and doc_section before writing. The ticket describes the product after the change: what changes, what stays, and every existing behaviour the change could break. Like every ticket it is product only: it never names a library, framework, hosting provider, database, auth provider, table, field type, endpoint or file.

{{scopeRule}}

{{ticketRules}}

{{acLibrary}}

## This ticket

- Acceptance criteria are mandatory: as many as the change needs to be fully checked, at most 20, and at least 3 when the effort score is 20 or more. Every decision above becomes at least one criterion. A change that touches a screen carries that screen's standing blocks for the parts it changes, never for a control it does not name: code refuses a `(standing: list)` criterion on sorting, filters or paging when the change and its requirements name none.
- `surface` names the one surface of the platform block this ticket builds, by its id or exact name; the ticket is written in that surface's terms (a surface with no web or PWA target: no browser, tab, address or URL, page reload, developer tools or Tab key). A change that spans two surfaces is written for the surface it mostly changes, and its Out of scope names what the other surface still needs.
- `reqKeys` lists the keys of the requirements this change modifies or delivers, only keys listed above; empty when none applies.
- The title follows the title rule above: the part of the product this change builds or changes, a noun phrase of 2 to 6 words, at most 60 characters, no trailing period, never the member's request verbatim and never the title of another ticket of the project.

Answer with one JSON object `{"title":"<noun phrase, at most 60 characters>","surface":"<surface id or exact name>","description":"<markdown with the eight headings>","reqKeys":["REQ-n"],"ac":["..."]}` and nothing else. It must be valid JSON: escape every double quote inside a string as \" and every newline as \n.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading what the change touches (30, "context read"), once the description and the acceptance criteria are decided (50, "change planned"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
