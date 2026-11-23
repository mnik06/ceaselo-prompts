### Block `list`: list or table

Any surface whose main content is a list or table of records.

- Only records the viewer may see are listed; records of another account, organization or role are never shown.
- The default order is stated and holds: <the ticket names it, for example newest first>.
- Only when the ticket offers sorting: every column offered as sortable sorts in both directions, and the active sort is visible.
- Only when the ticket offers filters or search: every filter and search offered narrows the rows, shows how many match, and offers a way to clear it.
- Only when the ticket offers paging: with more rows than one page holds, pagination or progressive loading reaches the last record without loading everything at once.
- Only when the ticket offers filters or search: with filters that match nothing, the list says no record matches and offers to clear the filters, distinct from the empty state.
- Opening a row lands on that record, and returning to the list keeps the previous position and every sort and filter the ticket offers.
- A record created, changed or deleted by this user appears, updates or disappears in the list without the user refreshing it.
