A client sent the feedback below during delivery. Digest it in one pass for the project manager.

Feedback ({{sourceLabel}}):
{{text}}{{linkedTicket}}

Tickets of the project (key: title):
{{tickets}}

Classes: "bug" (something built does not work as agreed), "change" (a new or different requirement), "question" (the client asks something and wants an answer).
Rules:
- digest: ONE line, at most 200 characters, plain language, what the client wants.
- linkedTicketKey: the key of the one ticket the feedback concerns, only when it clearly does; copy it exactly from the list; otherwise null.
- estimateDeltaHours: only for "change", your rough hours estimate of the added work; otherwise null.
- suggestedDelivery: only for "bug": "hotfix" when it blocks real use and cannot wait for the sprint, else "front_of_sprint"; otherwise null.

Answer with one JSON object and nothing else: {"digest":"...","class":"bug"|"change"|"question","linkedTicketKey":null,"estimateDeltaHours":null,"suggestedDelivery":null}
