### Block `notification`: email, in-app or push notification

- The notification is sent once per triggering event, to exactly the recipients the ticket names.
- It names what happened and links to the record it is about; the link opens that record for a recipient who is allowed to see it.
- A recipient who opted out, or no longer has access, does not receive it.
- A failed send is retried or recorded, and never blocks the action that triggered it.
- An email renders readably in plain text as well as HTML, and contains no data the recipient may not see.
