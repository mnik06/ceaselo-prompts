### Block `api`: an API surface

Every operation the ticket adds or changes, as a client calls it.

- A successful call answers the status the ticket names for it (for example 201 with the created record, 204 with no body).
- Input that breaks a rule is refused with a validation error naming each field and the rule it broke, and nothing is written.
- A call without credentials is refused as unauthenticated; a call whose credentials lack the right is refused as forbidden (or not found where the ticket hides existence), and never returns the data.
- A record that does not exist, or the caller may not see, answers not found.
- A list operation answers one page at a time with a stated maximum page size and a way to the next page that reaches the last item.
- Retrying a create or change with the same request (or the same idempotency key, where the ticket names one) does the work once and answers the same result.
- Every error answer carries a stable machine-readable code and a human-readable message, never a stack trace or internal detail.
