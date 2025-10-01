# Create Tasks (Codex Prompt)

## Usage
```
codex exec --prompt create-tasks
```

## Goal
Produce a TDD-oriented checklist in `tasks.md` for the active spec.

## Guidance
- Load layered AGENTS: global, project, spec.
- Request numbered parent tasks with decimal subtasks (tests → implementation → verification).
- Validate ordering, dependencies, and coverage before implementation.

### References
- `@.agent-os/instructions/core/create-tasks.md`
- `.agent-os/specs/<spec-folder>/tasks.md`
