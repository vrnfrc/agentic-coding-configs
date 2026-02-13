# `settings.json`

Documents the Claude Code `settings.json` template.

## `attribution`

Strings appended to commit messages and PR descriptions to identify AI-generated changes.

## `permissions`

Controls which tool invocations are auto-approved, denied, or require user confirmation.

- **`allow`** — runs without asking. Use for safe, read-only or routine commands:
  - `Bash(ls *)`
  - `Bash(git add *)`
  - `Bash(find *)`
- **`deny`** — blocked entirely. Use for destructive or irreversible operations:
  - `Bash(rm *)`
  - `Bash(git * push *)`
- **`ask`** — prompts the user before running. Use for actions that are safe but should be intentional:
  - `Bash(git commit *)`
  - `Bash(brew*)`

## `enabledPlugins`

Plugins providing additional tool capabilities (e.g., LSP integration for code intelligence).
