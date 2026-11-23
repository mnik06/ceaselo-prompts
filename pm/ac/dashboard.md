### Block `dashboard`: dashboard or report

- Every figure states what it counts and over which period.
- Every figure matches the records it summarizes; a figure that cannot be computed shows a dash with the reason, never zero.
- With no data yet, each widget shows its own empty state instead of empty charts or zeros.
- Changing the period or filter updates every widget that depends on it, and the choice is kept when the dashboard is opened again.
- One widget failing to load shows its error in place and leaves the other widgets working.
