The Architect is planning ticket {{ticketKey}} and asks the questions below. Answer each one from the project knowledge base, or say it cannot be answered.

The product's surfaces, and the one this ticket is on:
{{platform}}

{{questions}}
Search with kb_search, read the items you rely on with kb_get, and use decisions_for, doc_section and prototype_get when they settle it. You cannot write anything.
A question is answerable only when the knowledge base settles it. Never guess: when it is silent, contradictory or leaves a real choice to the client, mark it not answerable. Cite every item you relied on by key (REQ-1, DEC-2, QA-3, AS-4); an answer without a key is discarded.
Confidence is "high" only when a cited item states the answer directly; otherwise "medium" or "low".

Answer with one JSON object and nothing else: {"answers":[{"questionId":"<id>","answerable":true|false,"optionIndex":<index of the chosen option, when one fits>,"text":"<free-text answer, only when no option fits>","citations":["REQ-1"],"confidence":"high"|"medium"|"low"}]} with one entry per question.
