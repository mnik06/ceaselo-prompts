Break "{{projectName}}" into a work breakdown: tickets, acceptance criteria and dependencies. The Architect chooses the repositories when it plans each ticket.

Requirements (key: title):
{{requirements}}

Prototype screens:
{{prototypeOutline}}

{{presets}}{{note}}

Sprints are {{sprintLengthWeeks}} weeks with {{billableCapacityHours}} billable hours each; size the plan so it fills whole sprints.

Rules, all checked by machine:
- Foundation first, then vertical slices: tickets with foundation=true depend only on foundation tickets.
- Dependencies reference ticket refs, never form a cycle, and never point at a missing ticket.
- Every dev ticket has at least one acceptance criterion. A hitl ticket (a human task) has a dependent ticket; set hitl.dueBeforeRef to the first ticket that needs it.
- effortScore 0-100 (tiny <20, small <45, medium <75, large), estimateHours > 0.

Answer with one JSON object {"tickets":[{ref,title,type,description,ac,effortScore,estimateHours,tags,foundation,dependsOn,hitl?}]} and nothing else.{{rejected}}
