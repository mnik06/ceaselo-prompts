Write the wording of a client proposal for the project below. The scope, hours, dates and assumptions are filled in by code: you write only the title, a short summary and, per epic, a client-facing title and one or two sentences.
Audience: the client. Plain business language, no jargon, no internals.

Epics with the client-safe titles and summaries of their tickets (JSON):
{{epics}}

Never write ticket keys, acceptance criteria, hours, dates, money, prices, rates or internal notes.{{rejected}}
Answer with exactly one JSON object {"title": string, "summary": string, "epics": [{"epicId": string, "title": string, "summary": string}]} and nothing else. Use each epic's id exactly as given and answer for every epic.
