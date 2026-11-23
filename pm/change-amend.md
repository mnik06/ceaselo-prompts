Fold a confirmed change to "{{projectName}}" into the existing tickets below: rewrite each one's description and acceptance criteria so the ticket, read alone, describes the product after the change. No new ticket is created. The Architect, the builders and the verifier will work from these tickets alone.

## The product's surfaces

{{platform}}

## The change

{{summary}}

Effort score of the change: {{effortScore}}. The change was settled with the member before this card was confirmed: every decision above is settled. State each as a fact of the product in the ticket it belongs to and turn each into acceptance criteria; never write "defaults", "assumed" or "unless you say otherwise", and never reopen a decision.

## The tickets to amend, as they are now

{{tickets}}

## Requirements of the project (key: title)

{{requirements}}

Read the requirements, decisions and screens this change touches in full with kb_search, kb_get and doc_section before writing. Like every ticket the result is product only: it never names a library, framework, hosting provider, database, auth provider, table, field type, endpoint or file.

## What is true, in this order

1. The change above, with the grill answers it carries: settled, never reopened.
2. The code: the project's repos at their default-branch head, under "## Code this turn" at the end of this prompt. Before writing, read the files of the screens and behaviour this change touches. The ticket describes the product as the code builds it today: never a behaviour or element the code no longer has, even when a requirement or decision still names it. With no "## Code this turn" section the code was not readable this time: work from the change and the knowledge base.
3. The knowledge base (requirements, decisions, screens), for what the code does not show.

## Revisions and Kip's calls

- `revisions`: when code you read contradicts a requirement or decision about how the product behaves today, revise it: `{"key":"REQ-n","body":"<the item's whole body, rewritten to match the code>","path":"<owner/repo>:<the file you read>"}`. Never one about behaviour not built yet (its feature has no code, or its tickets are not done), and never for what this change itself alters: that is the ticket's job. At most 8; none is the usual case.
- `calls`: a fork you had to settle that no grill answer, decision of the change or knowledge base item covers: `{"title":"<at most 120 characters>","decision":"<what you settled, at most 500>","why":"<one line>"}`. Code records each as Kip's call on the ticket and lists it under Assumptions: never write them there yourself. At most 8; none is fine.

{{scopeRule}}

{{ticketRules}}

{{acLibrary}}

## How to amend

- Change only what the change touches. Keep every other part of a description word for word, and every criterion the change does not affect exactly as it is, so its status (a met criterion stays met) is kept.
- A dev ticket keeps the eight description headings. A HITL ticket keeps its own shape: what the person provides and how.
- Each criterion of your answer is either an existing one, by its number `n` (its text unchanged, or reworded when the change alters it: a reworded criterion is checked again), or a new one without `n`. A criterion you leave out is deleted: drop only what the change removes. Order them as they should read.
- A dev ticket keeps at least one criterion and at most 40; a change that moves work from one ticket to another removes it from the first and adds it to the second.
- Give `description` only for a ticket whose description changes; omit it to keep the description as it is.
- Each ticket stays on its surface (named with it above) and in that surface's terms: a ticket on a surface with no web or PWA target never gains a mention of a browser, a tab, an address or URL, a page reload, developer tools or the Tab key.

Answer with one JSON object `{"tickets":[{"key":"<ticket key>","description":"<the full new description, only when it changes>","ac":[{"n":1,"text":"..."},{"text":"a new criterion"}]}],"revisions":[],"calls":[]}` holding every ticket above exactly once and nothing else. It must be valid JSON: escape every double quote inside a string as \" and every newline as \n.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading what the change touches (30, "context read"), once the amendments are decided (50, "change planned"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
