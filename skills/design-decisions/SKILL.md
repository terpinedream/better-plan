---
name: design-decisions
description: Identify architecture and design decisions the user should make
  deliberately, and present options with trade-offs before a plan is written.
  Use at the start of planning for new projects, new features, or any change
  that touches structure, technology choices, or data flow.
---

# Design Decision Checkpoint

Goal: the user, not the agent, makes every significant architecture/design
decision. Be thorough when finding and ranking decisions; be condensed when
presenting them. Many users don't realize which choices are significant, so
surface them — but as a compact chooser, not an essay.

**Presentation:** Prefer an interactive question tool when available. No
preamble, no recap of the request, no plan in the same message as questions.

## 1. Gather what is already decided

Check these sources, in order:

1. The user's current request
2. AGENTS.md and any project rules
3. `.cursor/decisions.md` (the decisions log, see step 5)
4. The existing code: language, framework, dependencies, directory structure,
   config files, and manifests (package.json, pyproject.toml, Cargo.toml, etc.)

Anything established by these sources is settled. Do not re-ask it. List it
under **Assumed** (compact) so the user can override.

## 2. Identify the decisions that matter

A decision is significant if it is costly to reverse later, shapes much of the
rest of the code, or involves real trade-offs. Scan these areas:

- Language/runtime (performance vs portability vs development speed)
- Framework and major libraries
- Application structure (monolith vs services, layering, module boundaries)
- Data: storage engine, schema approach, state management, caching
- Interfaces: API style, protocols, file and wire formats
- Concurrency and execution model
- Error handling, configuration, logging
- Testing approach, CI, and deployment target
- Security and auth model
- Platform, licensing, or compliance constraints
- Build vs buy for any non-trivial component

Also surface decisions the user may not realize are decisions (e.g. implies a
persistent store, needs a plugin boundary, sync vs async). Always know *why*
it matters for this project — even if the reply states that in one line.

## 3. Rank and limit

- Ask only the **3–6** highest-impact open decisions per round.
- Group minor ones into **Defaults** (one line each: `X — reason`).
- Never pad with trivia. If nothing is open, say so in one line and plan.

## 4. Present (condensed format)

Think through full pros/cons; **show** a tight version:

```markdown
**Assumed:** `A`; `B`; `C`

**Defaults:** `X — reason`; `Y — reason`

### 1. <Question>?
*<one-line why it matters here>*
- **A)** <label> — <pro>; <con>
- **B)** <label> — <pro>; <con>
- **C)** <label> — <pro>; <con>   ← optional 4th
→ **Suggest: A** — <one-line reason>
```

Per decision:

- 2–4 real options; each option = **one line** (pro and con folded in).
- No separate "when to use" paragraphs; fold into that line.
- Include an "other / not sure, explain more" path (tool or final line).
- Recommend, but do not choose for the user on significant decisions.
- If the user asks for more detail on an option, then expand — don't lead with it.

## 5. Record and proceed

1. Write answers to `.cursor/decisions.md`, creating it if needed:

   ```markdown
   ## <Decision title>

   - **Choice:** <what the user picked>
   - **Date:** <YYYY-MM-DD>
   - **Rationale:** <why, in the user's words where possible>
   - **Alternatives considered:** <brief list>
   ```

2. Write the plan, referencing each decision where it affects the work.
3. If an answer opens a new significant fork, run a short follow-up round
   (same thoroughness, same condensed format, same 3–6 limit) before finalizing.

## When NOT to run

Skip the full checkpoint for small, local changes (bug fixes, renames, single
functions, copy changes, dependency bumps). If unsure, run a minimal version:
list assumptions in one short paragraph and ask only if something is
genuinely consequential.
