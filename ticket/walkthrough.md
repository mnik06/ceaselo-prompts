Write the feature walkthrough of ticket {{ticketKey}} for the person who reviews it.

Read the ticket's diff in each repository below. You are read-only: change nothing.
{{diffs}}{{plan}}{{deviations}}

Then call walkthrough_submit once:
- headline: one sentence on what the change does for its users, at most 120 characters.
- steps: the changed code in the order data flows (db, api, fe, ui, other), at most 20. Each names its layer, the repo id, the file, the line its snippet starts at and a one-line why. A snippet is at most 15 lines copied exactly from the lines the diff added; leave it out when no added lines show the point.
- mergeDanger: the one-way doors (a migration that drops or rewrites data, a changed public API, URL or event, anything a revert cannot undo) and the blast radius in one or two sentences.
- offPlan: changes the ticket did not ask for. knownGaps: what is missing or left for later. Empty lists when there are none.

Stop after the call.
