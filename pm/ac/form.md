### Block `form`: create or edit form

- Every required field is marked, and submitting without it shows a message on that field naming what is missing.
- Every format, range and length rule shows its message on the field that broke it, naming what to fix.
- A value the server refuses (duplicate, conflict, rule) is shown on the field or the form with the server's reason.
- While submitting, the submit control shows progress and cannot be pressed again; a double submit never creates two records.
- A failed submit keeps everything the user entered.
- A successful submit confirms visibly and lands where the ticket says (the record, the list, the next step).
- Leaving the form with unsaved changes asks for confirmation, or the changes are already saved.
- An edit form opens with the record's current values.
- Saving an edit to a record someone else changed since it was opened is refused with a message, never silently overwriting the other change.
- A secret entered in the form (password, token, key) is never shown back after saving.
