Break "{{projectName}}" into a work breakdown: epics, tickets, acceptance criteria and dependencies.

Requirements (key: title):
{{requirements}}

Prototype screens:
{{prototypeOutline}}

Repositories (use these names in "repos"):
{{repos}}{{presets}}

Sprints are {{sprintLengthWeeks}} weeks with {{billableCapacityHours}} billable hours each; size the plan so it fills whole sprints.

Rules, all checked by machine:
- Foundation first, then vertical slices: tickets with foundation=true depend only on foundation tickets.
- Dependencies reference ticket refs, never form a cycle, and never point at a missing ticket.
- Every dev ticket has at least one acceptance criterion. A hitl ticket (a human task) has hitl.role and a dependent ticket; set hitl.dueBeforeRef to the first ticket that needs it.
- effortScore 0-100 (tiny <20, small <45, medium <75, large), estimateHours > 0.
- clientTitle (at most 80 characters) and clientSummary (at most 200) are written for the client: no jargon, no internal names.

Answer with one JSON object {"epics":[{ref,title,requirementKeys}],"tickets":[{ref,epicRef,title,type,description,ac,repos,effortScore,estimateHours,tags,foundation,clientTitle,clientSummary,dependsOn,hitl?}]} and nothing else.{{rejected}}
