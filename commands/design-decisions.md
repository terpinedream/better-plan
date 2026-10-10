---
name: design-decisions
description: Run the design-decision checkpoint now, or review and revisit
  previously recorded decisions
---

# Design Decisions

Use the `design-decisions` skill. Be thorough on analysis; keep the reply condensed.

1. Read `.cursor/decisions.md` if it exists and summarize recorded decisions briefly.
2. Look at the user's goal and project; identify significant decisions still open.
3. Present open decisions in the skill's condensed format (3–6 max, options,
   trade-offs, recommendation).
4. If the user wants to change a past decision, explain impact briefly, then
   update `.cursor/decisions.md` once they confirm.

If the user passed arguments, treat them as the topic to focus on.
