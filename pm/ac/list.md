### Block `list`: list or table

Any surface whose main content is a list or table of records.

- Only records the viewer may see are listed; records of another account, organization or role are never shown.
- The default order is stated and holds: <the ticket names it, for example newest first>.
- Every column offered as sortable sorts in both directions, and the active sort is visible.
- Every filter and search offered narrows the rows, shows how many match, and offers a way to clear it.
- With more rows than one page holds, pagination or progressive loading reaches the last record without loading everything at once.
- With filters that match nothing, the list says no record matches and offers to clear the filters, distinct from the empty state.
- Opening a row lands on that record, and returning to the list keeps the previous sort, filters and position.
- A record created, changed or deleted by this user appears, updates or disappears in the list without the user refreshing it.
