Break "{{projectName}}" into a work breakdown: the tickets that deliver its MVP, their dependencies and their estimates. Builders and the Architect will work from these tickets alone, so the breakdown must leave nothing of the MVP unclaimed.

## Features and their scope

Only features scoped `mvp` get tickets. Features scoped `later` or `out` get none, and no ticket claims their requirements.

{{features}}

## Requirements, by feature

Every requirement listed here belongs to the MVP. Bodies are shown when they fit; otherwise read any requirement in full with kb_get.

{{requirements}}

## Prototype screens

The approved prototype: each screen's route, name, summary, and the features, roles and states it shows.

{{screens}}{{note}}

## How to cut the breakdown

- **One Foundation ticket, then vertical slices.** Exactly one ticket carries `foundation: true`: the app runs, its shell and navigation are reachable, and it is live on a staging address. Title it for what people get ("The app opens on its staging address with its shell and navigation"), never for a technology. It builds the prototype's app shell as it is (its header, its navigation with every item in order, the screen the app opens on; read it with `prototype_get` screen "shell"), never a shell of its own: its `screens` lists the screen the app opens on, and every route the navigation reaches exists, as a placeholder until the ticket that builds it. It depends on no other ticket, and every other dev ticket depends on it, directly or through another ticket. On an existing codebase (see the note above) the app already runs: plan no Foundation ticket.
- **Every other ticket is a vertical slice:** a capability a person can see working end to end, never a layer ("all the models", "all the endpoints") and never a technical ticket. Sign-up, sign-in, roles and the information a feature keeps are built inside the first slice that uses them: no "data model base", "auth setup" or "deployment" ticket.
- **Product only.** The stack is not yours to choose: no ticket names a library, framework, hosting provider, database, auth provider, table, field type, endpoint or file. The Architect chooses those per ticket, with the project's approved stack.
- **One feature per ticket.** `feature` is the feature slug the ticket belongs to (from the list above), or a short kebab-case slug for foundation or cross-cutting work (`foundation`, `roles`, `notifications`).
- **Traceability.** `reqKeys` lists every requirement key the ticket delivers. **Every requirement listed above is in the `reqKeys` of at least one ticket.** A requirement too big for one ticket is split across several, each claiming it. Never name a key that is not listed. Requirements marked (already built) are not planned again unless a change to them is asked for.
- **Screens.** `screens` lists the prototype routes the ticket builds or changes, exactly as listed above. Every screen is built by some ticket.
- **Size.** A ticket is one to three days of work for one builder: effortScore 0-100 (tiny below 20, small below 45, medium below 75, large above), estimateHours > 0 and consistent with the score. Split anything larger.
- **Dependencies** reference ticket refs, never form a cycle and never point at a missing ticket. A ticket depends on what it consumes, so tickets that do not depend on each other can be built in parallel.
- **HITL tickets** (`type: "hitl"`) are tasks only a human can do: content, legal sign-off, a decision outside the product. Each has a dependent ticket; set `hitl.dueBeforeRef` to the first ticket that needs it. Never write one asking for credentials, API keys or accounts of a technical service (hosting, database, auth, email, payments, analytics): code creates those tickets from the approved stack, and such a ticket is refused.
- **Sprints** are {{sprintLengthWeeks}} weeks with {{billableCapacityHours}} billable hours each; size the plan so it fills whole sprints.
- `ref` is a short unique id ("t1", "t2", ...). `title` is at most 160 characters and says what the user gets. `tags` holds at most a few short labels ("frontend", "api"); feature and foundation are recorded on their own.

## Two ways to answer

**More than 12 tickets:** answer the skeleton only. Each ticket has `ref, title, type, feature, reqKeys, screens, foundation, dependsOn, effortScore, estimateHours, tags` and `hitl` for HITL tickets; leave out `description` and `ac`. Each feature group is detailed afterwards by its own session.

**12 tickets or fewer:** write every ticket in full now: the skeleton fields plus `description` and `ac`, following the rules below. Read the requirement bodies with kb_get where they are not shown.

{{ticketRules}}

{{acLibrary}}

## Checked by machine

The answer is refused, with the reasons, when a listed requirement is in no ticket's `reqKeys`, a `reqKeys` entry or a screen is unknown, a dependency is missing or circular, a new codebase has no foundation ticket, there is more than one, the Foundation ticket depends on another ticket, a HITL ticket has no dependent or asks for a declared service's credentials, or (12 tickets or fewer) a dev ticket lacks a description heading, its `reqKeys`, or at least 3 criteria when its effortScore is 20 or more.

Answer with one JSON object `{"tickets":[{ref,title,type,feature,reqKeys,screens,foundation,dependsOn,effortScore,estimateHours,tags,hitl?,description?,ac?}]}` and nothing else.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading the features, requirements and screens (15, "scope read"), once the tickets are cut (30, "tickets cut"), after the graph and estimates (45, "estimated"), after checking coverage (55, "coverage checked"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.
