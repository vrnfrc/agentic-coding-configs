# CLAUDE.md

## Project overview

> High-level description of what this project is about. Import or refer to the README.

### Environment

> Language versions, dependency manager, CI system, automation tools.

## Commands

### Build

> How to build the project. Include the most common invocations.
> ```bash
> # How to build the app
> ```

### Test

> How to run the full test suite, individual module tests, and a single test class/method.
> ```bash
> # How to run tests
> ```

### Lint

> Linter command and auto-fix. Note any known issues with the linter config.
> ```bash
> # How to lint
> ```

### Code generation

> Commands for mock generation, asset generation, etc. Note any obsolete tools.
> ```bash
> # How to generate code
> ```

### Setup

> Bootstrap / first-run commands after cloning the repo.
> ```bash   
> # How to set up the project
> ```

## Architecture

> High-level architecture overview. Reference sub-agents if they document patterns in detail.
>
> Describe the module/package structure, build configuration system, external SDKs, and testing infrastructure. Focus on the "big picture" that requires reading multiple files to understand — don't list every file.

### Project structure

> Summarized folder structure of the project. Only include the top-level directories and key subdirectories — don't list every file.
> 
> ```
> ├── src/
> │   ├── core/          # App entry point, DI, services
> │   ├── features/      # Feature modules (one folder per feature)
> │   ├── shared/        # Shared utilities, extensions, models
> │   └── resources/     # Assets, strings, configs
> ├── tests/
> │   ├── unit/          # Unit tests mirroring src/ structure
> │   └── integration/   # Integration / E2E tests
> ├── scripts/           # Build and automation scripts
> └── config/            # Environment and build configuration
> ```

## Conventions

> Reference sub-agents that own specific conventions.

### Code style

> Style guide, linter rules, key limits, naming conventions.

## Boundaries

> List explicit constraints that AI agents must respect. Examples:
>
> - To remove files, move them to trash instead of deleting permanently: `mv <file> ~/.Trash/`.
> - Ask the user before adding, removing, or upgrading dependencies.
> - Changes to CI/CD pipeline or build configuration files require explicit user approval.
