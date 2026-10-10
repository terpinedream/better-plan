---
name: design-decisions
description: Run the design-decision checkpoint now, or review and revisit
  previously recorded decisions
---

# Design Decisions

Use the `design-decisions` skill.

1. Read `.cursor/decisions.md` if it exists and summarize the decisions
   recorded so far.
2. Look at the user's current goal and the existing project, and identify any
   significant decisions that are still open.
3. Present the open decisions following the skill's rules (3-6 at most, with
   options, trade-offs, and a recommendation).
4. If the user wants to change a past decision, explain what else in the
   project it would affect, then update `.cursor/decisions.md` once they confirm.

If the user passed arguments, treat them as the topic to focus on.
