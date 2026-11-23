## Standing acceptance criteria

Reusable criteria, one block per kind of surface the product has. A ticket that builds a surface **inherits that surface's block**: paste every criterion of the block into the ticket's `ac`, rewritten with the ticket's real nouns (the record, the role, the screen, the command), and end each pasted criterion with its tag, for example `(standing: list)`.

**Paste, never reference.** "Usual list behaviour applies" or "see the form block" is how a screen ships without the affordance everyone assumed it had. The builder and the verifier see the ticket's criteria and nothing else: a criterion that is not written is a behaviour that is not built.

**Excluding a criterion is allowed and must be explicit:** leave it out of `ac` and say why under `## Out of scope` in the description ("No sorting: the list never holds more than five rows"). Silence is not exclusion.

A ticket that builds several surfaces pastes several blocks. A criterion two blocks share is pasted once. A GUI ticket pastes `ui` and the block of its surface's targets (`ui-web`, `ui-mobile`, `ui-desktop`); a CLI, API or library ticket pastes its kind's block. Only the blocks of this product's surfaces are listed below.

**A criterion that crosses surfaces is pasted where both exist.** "Opening a row lands on that record" needs the record's screen; "a record created in the form appears in the list" needs the form and the list. Paste such a criterion only into the ticket that builds the later of the two; on the earlier ticket, name that ticket under `## Out of scope` instead.
