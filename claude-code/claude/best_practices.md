# Best practices for building agents

## Show, don't tell

Examples are more effective than instructions. An agent that sees a concrete **Good** and **Bad** snippet will replicate the pattern far more reliably than one that reads a paragraph of rules.

Structure your examples like this:

```markdown
**Good**:

<concrete code or output example>

**Bad**:

<concrete code or output example>
```

Always place **Good** before **Bad** — the model anchors on what it sees first.

### Why this works

- LLMs are pattern-matching machines — a concrete example is an unambiguous pattern
- Written rules are open to interpretation; code is not
- A **Bad** example prevents the most common misinterpretation of the rule

### Example: commit messages

**Good**:

```
feat: add retry logic to payment service
```

**Bad**:

```
Updated payment stuff and added some retry things
```


## Other best practices

### Be specific about file paths

Always reference the files the agent should read or modify. Vague instructions lead to guesswork.

**Good**:

```markdown
* [Architect] Create ViewModel (`src/features/auth/LoginViewModel.ts`)
```

**Bad**:

```markdown
* [Architect] Create the ViewModel
```

### One responsibility per agent

Each agent should own a single concern. If an agent prompt mixes architecture enforcement with UI styling and test writing, it will do all three poorly.

### Keep prompts short

Long prompts dilute the important parts. If a section doesn't change the agent's behaviour, remove it. Prefer a few well-chosen examples over a wall of rules.

### Use sections the agent can skip

Structure the prompt with clear headings. The agent will focus on the section relevant to the current task and skim the rest. Flat, unstructured text forces it to parse everything every time.

### Define boundaries explicitly

State what the agent is **not** allowed to do. Without boundaries, agents tend to be "helpful" in ways you didn't ask for — committing unrelated files, refactoring surrounding code, adding documentation.

**Good**:

```markdown
## Rules

- You are only allowed to run `git status`, `git diff`, `git add`, and `git commit`
- If there are no changes to commit, say so and stop
```

**Bad**:

```markdown
## Rules

- Be careful with git commands
```

