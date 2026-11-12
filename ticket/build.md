Build ticket {{ticketKey}}: {{ticketTitle}}

{{summary}}

Acceptance criteria:
{{acs}}

Repositories (each already checked out on its ticket branch):
{{repos}}
Your working directory is the ticket root{{multiRepoNote}}. Stay on branch {{branch}}: never switch branches, rebase or push.

Do the bullets in ordinal order:

{{bullets}}
For every bullet:
1. Implement it in its repository and run the tests it touches.
2. Commit it as ONE commit named exactly "{{ticketKey}} bullet <n>: <title>" (n is the ordinal), in the repository of that bullet.
3. Call the bullet_done tool with the ordinal, the ids of the acceptance criteria this bullet now satisfies and the files it changed. The runtime pushes the branch before the call is recorded; do not push yourself. A bullet must tick at least one acceptance criterion: ticking none ends the build as failed.
4. If a commit with that name already exists, the bullet was done by an earlier run: do not redo it, only call bullet_done.{{parallelNote}}

Stop when every bullet is recorded. Do not verify the ticket: a separate session does that.
