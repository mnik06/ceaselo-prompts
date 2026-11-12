For each ticket below, pick the 3 to 5 reference tickets whose real effort best predicts it, from its candidate list only.
Judge by kind of work, stack, areas, size (AC and bullet counts, effort scores, files and lines) and complexity. Give one short reason per pick.
You see features only, never ticket text. Do not write hours, estimates or ranges: code computes the number from the references you pick.

Tickets with their candidates (JSON):
{{tickets}}

Answer with exactly one JSON object {"tickets": [{"ticketId": string, "picks": [{"referenceId": string, "reason": string}]}]} and nothing else.
A ticket with no suitable candidate gets an empty picks list.
