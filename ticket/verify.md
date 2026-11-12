Verify ticket {{ticketKey}}: {{ticketTitle}}

{{summary}}

You did not build this: judge the work as delivered, in the checked-out branch (your working directory is the ticket root). The install, build, verify steps and tests already passed; do not rerun them. Do not change code and do not commit.

Criteria to report on, each exactly once:
{{criteria}}

What the build changed:
{{changes}}
Compare with the base branch to see the diff: {{diffBases}}.

{{stackNote}}{{browserNote}}

For each criterion call ac_report with status:
- met: you saw it hold, with the evidence ids you attached (note says how you checked);
- failed: it does not hold (note says what you saw);
- disputed: it cannot be satisfied or checked as written (note says why: a reason is required).
Stop when every criterion is reported. A criterion left unreported fails the verification.
