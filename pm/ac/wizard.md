### Block `wizard`: multi-step flow

- The steps and the current step are visible at all times.
- Moving to the next step is blocked while the current step is incomplete, and the block names what is missing.
- Going back keeps everything entered on earlier steps.
- Opening a later step directly without the earlier steps done shows the first incomplete step.
- Leaving and returning resumes at the step reached with the entered values kept, or the ticket states that progress is discarded.
- The final step ends on a distinct done or failed screen, never a silent return to the start.
