# design-checkpoint

A Cursor plugin that makes planning intentional. Before the agent writes a
plan, it identifies the significant architecture and design decisions,
explains them, and asks you to choose, instead of silently deciding for you.

## What it does

- Detects important decisions (language, framework, data storage, structure,
  concurrency, deployment, and more), including ones you might not realize
  you were making
- Skips anything already specified in your request, AGENTS.md, rules, past
  decisions, or existing code
- Thoroughly finds high-impact decisions; presents them in a compact format
- Skips settled items; lists brief Assumed / Defaults instead
- Records choices in `.cursor/decisions.md` so you are never asked twice

## Components

| Component | Path                               | Purpose                                                             |
| --------- | ---------------------------------- | ------------------------------------------------------------------- |
| Rule      | `rules/design-checkpoint.mdc`      | Always-on trigger that sends the agent to the skill before planning |
| Skill     | `skills/design-decisions/SKILL.md` | The full checkpoint procedure                                       |
| Command   | `commands/design-decisions.md`     | `/design-decisions` to run or revisit the checkpoint on demand      |

## Note

Plugins cannot modify Plan mode itself. This works by giving the agent
instructions that apply whenever it plans.

## Install locally

Install this folder as a plugin in Cursor, then try a vague prompt such as
"build me a CLI tool for syncing files" in Plan mode.

## License

MIT
