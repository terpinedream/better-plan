---
name: design-decisions
description: Identify architecture and design decisions the user should make
  deliberately, and present options with trade-offs before a plan is written.
  Use at the start of planning for new projects, new features, or any change
  that touches structure, technology choices, or data flow.
---

# Design Decision Checkpoint

Goal: the user, not the agent, makes every significant architecture/design
decision. Many users don't realize which choices are significant, so surface
them, explain them, and let the user choose.

## 1. Gather what is already decided

Check these sources, in order:

1. The user's current request
2. AGENTS.md and any project rules
3. `.cursor/decisions.md` (the decisions log, see step 5)
4. The existing code: language, framework, dependencies, directory structure,
   config files, and manifests (package.json, pyproject.toml, Cargo.toml, etc.)

Anything established by these sources is settled. Do not re-ask it. List it
under "Assumed from existing project" so the user can override it if they want.

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

Also surface decisions the user may not realize are decisions. Examples: "this
feature implies a persistent data store", "this needs a plugin or extension
boundary", "this implies a choice between sync and async". Always explain why
the decision matters for THIS specific project.

## 3. Rank and limit

- Ask only the 3-6 highest-impact open decisions per round.
- Group the minor ones into a "Defaults I'll use unless you object" list, each
  with a one-line reason.
- Never pad with trivial choices. Too many questions makes the checkpoint
  annoying and people will disable it.

## 4. Present each decision

For each decision include:

- The question, in plain language, and why it matters for this project
- 2-4 real options, each with: pros, cons, and when it is the best fit
- Your recommendation with reasoning, clearly labeled as a suggestion
- An "other / not sure, explain more" path

If an interactive question tool (multiple choice) is available, use it so the
user can answer quickly. Do not bury the choices in long prose.

Do not choose for the user on a significant decision, even when one option
seems obvious. Recommend, but let them confirm.

## 5. Record and proceed

1. Write the answers to `.cursor/decisions.md`, creating it if needed. Use
   this format per decision:

   ```markdown
   ## <Decision title>

   - **Choice:** <what the user picked>
   - **Date:** <YYYY-MM-DD>
   - **Rationale:** <why, in the user's words where possible>
   - **Alternatives considered:** <brief list>
   ```

2. Write the plan, referencing each decision where it affects the work.
3. If an answer opens a new significant fork, run a short follow-up round
   (same rules, same limits) before finalizing the plan.

## When NOT to run

Skip the full checkpoint for small, local changes (bug fixes, renames, single
functions, copy changes, dependency bumps). If unsure, run a minimal version:
list your assumptions in one short paragraph and ask only if something is
genuinely consequential.
