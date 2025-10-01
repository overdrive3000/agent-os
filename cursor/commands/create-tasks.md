# /create-tasks

Translate the active spec into a TDD-oriented task list.

## When to run
- Immediately after reviewing the spec output.
- Before any implementation begins.

## Steps
1. Load guidance: `@AGENTS.md`, `@./AGENTS.md`, and spec `@.agent-os/specs/<spec-folder>/AGENTS.md`.
2. Ask the agent to break work into numbered parent tasks with decimal subtasks (tests first, implementation, verification).
3. Review `tasks.md` for coverage, ordering, and acceptance criteria.
4. Adjust tasks manually if business rules or edge cases are missing.

## References
- `@.agent-os/instructions/core/create-tasks.md`
- `.agent-os/specs/<spec-folder>/tasks.md`
