# plan-mode.md

Plan mode guidelines.

## Strategy

Treat each plan as a task ticket. Split the work into **analysis** (identify the code that needs changing) and **coding** (write the changes).

Then split the coding into phases. Each phase contains a list of bullet points. Each bullet point specifies the sub-agent responsible:
* Architect
* Navigator
* Tester
* Designer
* Committer

Every phase ends with a commit:
```markdown
* [Committer] Commit
```

### Bullet point format

Every bullet point must name the sub-agent in brackets, describe the action, and list the affected files. Paths below are dummy examples.

**Good**:

```markdown
* [Architect] Create all involved files (`UserView.tsx`, `UserViewModel.ts`, `UserViewModel.test.ts`)
* [Designer] Create View (`UserView.tsx`)
* [Tester] Write happy-path unit tests for `UserViewModel` (`UserViewModel.test.ts`)
* [Architect] Implement ViewModel and make tests pass (`UserViewModel.ts`)
```

**Bad**:

```markdown
* Create View
* Create unit tests for happy path
* Create ViewModel and make tests succeed
```

## Flows

Choose the flow that matches the task. When the task spans multiple flows (e.g. new UI backed by new business logic), combine phases from both — business logic first, then UI.

### New feature with views

Use when the task introduces a new screen or a significant new UI component with its own state management.

1. **Scaffolding**: create all files (models, state, events, controller/ViewModel skeleton, empty test class)
2. **Happy-path tests**: write failing unit tests for the happy path
3. **Happy-path implementation**: implement logic to make happy-path tests pass
4. **Validation tests**: write failing validation unit tests
5. **Validation implementation**: implement validation logic to make tests pass
6. **Corner-case tests**: write failing corner-case unit tests
7. **Corner-case implementation**: implement corner-case logic to make tests pass
8. **UI**: create the View / component
9. **Navigation**: wire the View / component into the app navigation

Tests and implementation may be combined into a single phase when the scope is small, but each phase always ends with its own commit.

### UI only

Use when the task modifies only the UI layer (layout, styling, animations) without changing business logic.

1. **Analysis**: identify the Views / components to modify
2. **UI changes**: apply the visual modifications
3. **Snapshot updates** (if applicable): update or add snapshot tests for the changed Views / components

No business logic tests are needed because no business logic changes.

### Business logic only

Use when the task modifies controller / ViewModel logic, services, repositories, or models without any UI changes.

1. **Analysis**: identify the classes / modules and methods to modify
2. **Failing tests**: write failing unit tests that describe the expected new behaviour
3. **Implementation**: modify the production code to make the tests pass
4. **Corner cases**: add failing tests for edge cases, then make them pass

## General guidelines

- Always use TDD for business logic changes
- Each phase ends with a commit
- Keep phases granular — one type of work per phase

## Examples

> Adapt these examples to the project's language, framework, and file conventions.

**Good** (new feature with views):

```markdown
# Implement User Profile screen

## Quick overview

* A profile page showing user details with an edit button.
* Tapping edit opens an inline form.
* A save button persists changes.

## 1 — Scaffolding

* [Architect] Create all files (`UserProfile.tsx`, `UserProfileViewModel.ts`, `UserProfileViewModel.test.ts`, `User.ts`)
* [Committer] Commit

## 2 — Happy path

* [Tester] Write happy-path unit tests for `UserProfileViewModel` (`UserProfileViewModel.test.ts`)
* [Architect] Implement ViewModel and make tests pass (`UserProfileViewModel.ts`)
* [Committer] Commit

## 3 — Corner cases

* [Tester] Write corner-case unit tests (`UserProfileViewModel.test.ts`)
* [Architect] Implement corner-case logic and make tests pass (`UserProfileViewModel.ts`)
* [Committer] Commit

## 4 — UI

* [Designer] Create View (`UserProfile.tsx`)
* [Committer] Commit

## 5 — Navigation

* [Navigator] Wire `UserProfile` into the navigation (`routes.ts`)
* [Committer] Commit
```

**Good** (business logic only):

```markdown
# Fix retry logic in NetworkService

## Quick overview

* The retry logic does not respect the backoff delay after the second attempt.

## 1 — Failing tests

* [Tester] Write failing tests that assert correct backoff delays (`NetworkService.test.ts`)
* [Committer] Commit

## 2 — Fix

* [Architect] Fix retry logic and make tests pass (`NetworkService.ts`)
* [Committer] Commit
```

**Bad**:

```markdown
# Plan for new simple feature

Long and unnecessary analysis

## Phase 1

* Create View
* Create ViewModel unit tests for happy path
* Create ViewModel and make tests succeed
```
