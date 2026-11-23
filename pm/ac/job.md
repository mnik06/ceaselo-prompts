### Block `job`: background or scheduled job

- The job runs on the stated trigger or schedule.
- Running the job twice for the same input has the same result as running it once.
- A failed item is recorded with its reason and retried or reported as the ticket states, and never stops the other items.
- While the job runs, the affected records or screens show that work is in progress.
- The job's outcome (done, failed, items processed) is visible to the people the ticket names.
