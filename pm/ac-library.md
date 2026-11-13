## Standing acceptance criteria

Reusable criteria, one block per kind of surface. A ticket that builds a surface **inherits that surface's block**: paste every criterion of the block into the ticket's `ac`, rewritten with the ticket's real nouns (the record, the role, the screen), and end each pasted criterion with its tag, for example `(standing: list)`.

**Paste, never reference.** "Usual list behaviour applies" or "see the form block" is how a screen ships without the affordance everyone assumed it had. The builder and the verifier see the ticket's criteria and nothing else: a criterion that is not written is a behaviour that is not built.

**Excluding a criterion is allowed and must be explicit:** leave it out of `ac` and say why under `## Out of scope` in the description ("No sorting: the list never holds more than five rows"). Silence is not exclusion.

A ticket that builds several surfaces pastes several blocks. A criterion two blocks share is pasted once.

### Block `ui`: any UI surface

Every screen, panel, modal, drawer or step the ticket adds or changes.

- While its data loads, the surface shows a loading state that says what is loading, never a blank region.
- With no data, the surface shows an empty state that says why it is empty and offers the next action when there is one.
- When loading fails, the surface shows the error in place, in words the user understands, with a way to try again.
- Every failure the user can cause is shown on screen, in place or as a notification naming what failed; nothing fails silently.
- A control the viewer's role cannot use is not offered, and the server refuses the action when it is called anyway.
- Every interactive control is reachable by keyboard and shows visible focus.
- At the narrowest width the product supports, nothing overlaps or is cut off, and the page has no horizontal scroll.
- Long values (names, titles, emails, numbers) wrap or truncate with the full value available, never widening the layout.
- Labels, messages and empty-state copy use the product's own terms, the same words the rest of the product uses for the same thing.

### Block `list`: list or table

Any surface whose main content is a list or table of records.

- Only records the viewer may see are listed; records of another account, organization or role are never shown.
- The default order is stated and holds: <the ticket names it, for example newest first>.
- Every column offered as sortable sorts in both directions, and the active sort is visible.
- Every filter and search offered narrows the rows, shows how many match, and offers a way to clear it.
- With more rows than one page holds, pagination or progressive loading reaches the last record without loading everything at once.
- With filters that match nothing, the list says no record matches and offers to clear the filters, distinct from the empty state.
- Opening a row lands on that record, and returning to the list keeps the previous sort, filters and page.
- A record created, changed or deleted by this user appears, updates or disappears in the list without a manual reload.

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

### Block `wizard`: multi-step flow

- The steps and the current step are visible at all times.
- Moving to the next step is blocked while the current step is incomplete, and the block names what is missing.
- Going back keeps everything entered on earlier steps.
- Opening a later step directly without the earlier steps done redirects to the first incomplete step.
- Leaving and returning resumes at the step reached with the entered values kept, or the ticket states that progress is discarded.
- The final step ends on a distinct done or failed screen, never a silent return to the start.

### Block `detail`: record detail page

- The record's identity (name, key or title) is visible without scrolling.
- Every field the record has is shown, with an explicit placeholder for an empty field.
- A record that does not exist, was deleted, or the viewer may not see shows a not-found page with a way back, never a broken page.
- A deep link to the record opens it directly, and reload keeps the viewer on it, including the active tab.
- Edits made on the page persist and survive a reload.
- Deleting asks for confirmation naming the record and what else is removed with it, then lands on the list with a confirmation.

### Block `board`: board with columns

- Every card sits in the column its current state names.
- Moving a card to another column changes the record's state, and the change survives a reload.
- A move the rules forbid is refused visibly with the reason, and the card returns to its column.
- An empty column still shows its heading and a drop area, with no gap left between columns.
- A column with many cards scrolls on its own without moving the rest of the board.

### Block `dashboard`: dashboard or report

- Every figure states what it counts and over which period.
- Every figure matches the records it summarizes; a figure that cannot be computed shows a dash with the reason, never zero.
- With no data yet, each widget shows its own empty state instead of empty charts or zeros.
- Changing the period or filter updates every widget that depends on it, and the choice survives a reload.
- One widget failing to load shows its error in place and leaves the other widgets working.

### Block `auth`: sign-up, sign-in, recovery, session

- Wrong credentials are refused with one message that does not reveal whether the account exists.
- Repeated failed sign-ins are slowed or blocked after a stated number of attempts.
- A password shorter or weaker than the stated rule is refused on the field with the rule named.
- A signed-out visitor opening a protected page is sent to sign-in and, once signed in, returns to that page.
- Signing out ends the session; going back in the browser does not show protected content.
- An expired session sends the user to sign-in without losing the page they were on.
- A recovery or verification link works once, expires after the stated time, and an expired or used link says so and offers a new one.

### Block `upload`: file upload

- Allowed file types and the size limit are stated next to the upload control.
- A file of another type or over the limit is refused before uploading, naming the rule it broke.
- Upload progress is visible, and a failed upload says why and can be retried without choosing the file again.
- A file uploaded twice is handled as the ticket states (replaced, kept as a copy, or refused).
- An uploaded file can be opened or downloaded by the people allowed to see it, and by nobody else.
- Removing an uploaded file asks for confirmation and removes it everywhere it is shown.

### Block `notification`: email, in-app or push notification

- The notification is sent once per triggering event, to exactly the recipients the ticket names.
- It names what happened and links to the record it is about; the link opens that record for a recipient who is allowed to see it.
- A recipient who opted out, or no longer has access, does not receive it.
- A failed send is retried or recorded, and never blocks the action that triggered it.
- An email renders readably in plain text as well as HTML, and contains no data the recipient may not see.

### Block `job`: background or scheduled job

- The job runs on the stated trigger or schedule.
- Running the job twice for the same input has the same result as running it once.
- A failed item is recorded with its reason and retried or reported as the ticket states, and never stops the other items.
- While the job runs, the affected records or screens show that work is in progress.
- The job's outcome (done, failed, items processed) is visible to the people the ticket names.

### Block `integration`: third-party service

- A request the service refuses or times out on shows a message naming the service, and leaves no half-written data.
- Credentials for the service are stored server-side and never sent to the browser.
- An incoming webhook or callback is verified as coming from the service; an unverified one is refused.
- A webhook delivered twice is processed once.
- When the service is down, the rest of the product keeps working and the affected feature says it is unavailable.

### Block `settings`: admin and settings

- Only the roles the ticket names can open the settings; everyone else gets not-found or forbidden from the server too.
- Every setting shows its current value and the effect of changing it.
- A saved change takes effect where the ticket says, without a restart or redeploy.
- A destructive change (removing a member, deleting data, changing a plan) asks for confirmation naming the consequence.
- Every change is recorded with who made it and when, where the ticket says audit applies.
