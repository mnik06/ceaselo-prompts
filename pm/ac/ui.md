### Block `ui`: any GUI surface

Every screen, panel, modal, drawer, sheet or step the ticket adds or changes, on any target.

- While its data loads, the surface shows a loading state that says what is loading, never a blank region.
- With no data, the surface shows an empty state that says why it is empty and offers the next action when there is one.
- When loading fails, the surface shows the error in place, in words the user understands, with a way to try again.
- Every failure the user can cause is shown on screen, in place or as a notification naming what failed; nothing fails silently.
- A control the viewer's role cannot use is not offered, and the server refuses the action when it is called anyway.
- At the smallest size the product supports, nothing overlaps or is cut off.
- Long values (names, titles, emails, numbers) wrap or truncate with the full value available, never widening the layout.
- Labels, messages and empty-state copy use the product's own terms, the same words the rest of the product uses for the same thing.
