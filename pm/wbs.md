Break "{{projectName}}" into a work breakdown: the tickets that deliver its MVP, their dependencies and their estimates. Builders and the Architect will work from these tickets alone, so the breakdown must leave nothing of the MVP unclaimed.

## Features and their scope

Only features scoped `mvp` get tickets. Features scoped `later` or `out` get none, and no ticket claims their requirements.

{{features}}

## Requirements, by feature

Every requirement listed here belongs to the MVP. Bodies are shown when they fit; otherwise read any requirement in full with kb_get.

{{requirements}}

## Prototype screens

The approved prototype: each screen's route, name, summary, and the features, roles and states it shows.

{{screens}}{{presets}}{{note}}

## How to cut the breakdown

- **Foundation first, then vertical slices.** Foundation tickets (scaffold, data model base, authentication, shared layout and navigation, deployment) carry `foundation: true` and depend only on other foundation tickets. Every other ticket is a vertical slice: a capability a user can see working end to end (data, API and UI together), never a layer ("all the models", "all the endpoints").
- **One feature per ticket.** `feature` is the feature slug the ticket belongs to (from the list above), or a short kebab-case slug for foundation or cross-cutting work (`foundation`, `roles`, `notifications`).
- **Traceability.** `reqKeys` lists every requirement key the ticket delivers. **Every requirement listed above is in the `reqKeys` of at least one ticket.** A requirement too big for one ticket is split across several, each claiming it. Never name a key that is not listed. Requirements marked (already built) are not planned again unless a change to them is asked for.
- **Screens.** `screens` lists the prototype routes the ticket builds or changes, exactly as listed above. Every screen is built by some ticket.
- **Size.** A ticket is one to three days of work for one builder: effortScore 0-100 (tiny below 20, small below 45, medium below 75, large above), estimateHours > 0 and consistent with the score. Split anything larger.
- **Dependencies** reference ticket refs, never form a cycle and never point at a missing ticket. A ticket depends on what it consumes, so tickets that do not depend on each other can be built in parallel.
- **HITL tickets** (`type: "hitl"`) are tasks only a human can do: credentials, accounts, content, legal sign-off, a decision outside the product. Each has a dependent ticket; set `hitl.dueBeforeRef` to the first ticket that needs it.
- **Sprints** are {{sprintLengthWeeks}} weeks with {{billableCapacityHours}} billable hours each; size the plan so it fills whole sprints.
- `ref` is a short unique id ("t1", "t2", ...). `title` is at most 160 characters and says what the user gets. `tags` holds at most a few short labels ("frontend", "api"); feature and foundation are recorded on their own.

## Two ways to answer

**More than 12 tickets:** answer the skeleton only. Each ticket has `ref, title, type, feature, reqKeys, screens, foundation, dependsOn, effortScore, estimateHours, tags` and `hitl` for HITL tickets; leave out `description` and `ac`. Each feature group is detailed afterwards by its own session.

**12 tickets or fewer:** write every ticket in full now: the skeleton fields plus `description` and `ac`, following the rules below. Read the requirement bodies with kb_get where they are not shown.

{{ticketRules}}

{{acLibrary}}

## Checked by machine

The answer is refused, with the reasons, when a listed requirement is in no ticket's `reqKeys`, a `reqKeys` entry or a screen is unknown, a dependency is missing or circular, a foundation ticket depends on a non-foundation one, a HITL ticket has no dependent, or (12 tickets or fewer) a dev ticket lacks a description heading, its `reqKeys`, or at least 3 criteria when its effortScore is 20 or more.

Answer with one JSON object `{"tickets":[{ref,title,type,feature,reqKeys,screens,foundation,dependsOn,effortScore,estimateHours,tags,hitl?,description?,ac?}]}` and nothing else.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: after reading the features, requirements and screens (20, "scope read"), after cutting the tickets (50, "tickets cut"), after the graph and estimates (80, "estimated"), after checking coverage (95, "coverage checked"). Never call it more often, never report 100 (the end of the task says that), and skip it if the tool is not listed.
