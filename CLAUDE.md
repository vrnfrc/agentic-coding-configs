# CLAUDE.md

## Purpose

This is a template repository of reusable agentic coding configuration files. The configs here are designed to be copied and adapted into other project repositories. There is no build system, test suite, or application code — only configuration and documentation.

## Repository structure

Configs are organized by agentic coding provider.

### Claude Code configs (`claude-code/`)

- `EXAMPLE_CLAUDE.md` — A skeleton CLAUDE.md template with standard sections (project overview, commands, architecture, conventions). Copy this into a target repo and fill in the project-specific details.
- `claude_agents/settings.json` — Claude Code permission rules and plugin config. Maps to `.claude/settings.json` in the target repo.
- `claude_agents/agents/` — Sub-agent definitions (Markdown with YAML frontmatter). Each file defines a specialized role:
  - **Architect** — Architecture enforcement (official SwiftUI+ViewModel pattern vs legacy UIKit+Coordinator)
  - **Navigator** — Navigation wiring (Router/Destination pattern for new screens, Coordinator for legacy)
  - **Designer** — SwiftUI view decomposition and styling
  - **Tester** — TDD workflow, test structure conventions, async testing with Dispatcher
  - **Committer** — Git commit formatting (Conventional Commits) and branch naming
  - **Teacher** — Concept explanation and Q&A
- `claude_agents/rules/plan-mode.md` — Plan mode strategy: how to structure phased plans with sub-agent assignments, commit boundaries, and TDD flow selection (new feature / UI only / business logic only)

### Agent file format

Agent `.md` files use YAML frontmatter for metadata (`name`, `description`, `model`, `color`, `memory`, `tools`) followed by the system prompt body. These map to `.claude/agents/<Name>.md` in the target repo.

## How to add a new provider

1. Create a top-level directory named after the provider (e.g., `cursor/`, `copilot/`, `windsurf/`)
2. Add example config files matching that provider's conventions
3. Keep agent roles generic where possible (Architect, Tester, Committer patterns transfer across providers)
