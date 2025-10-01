# /execute-tasks

Implement the spec by iterating through parent tasks, using TDD and the full Agent OS workflow.

## When to run
- A spec has approved `tasks.md` entries ready for delivery.
- You’re prepared to manage branches, tests, and post-execution steps.

## Steps
1. Load guidance: `@AGENTS.md`, `@./AGENTS.md`, spec `@.agent-os/specs/<spec-folder>/AGENTS.md`, and optional task file guidance.
2. Confirm which parent task(s) to execute. Default: next unchecked parent task.
3. Follow the three-phase loop (pre-execution setup, per-task execution, post-execution wrap-up).
4. Review diffs, tests, and recaps with the human operator before final delivery.

## References
- `@.agent-os/instructions/core/execute-tasks.md`
- `.agent-os/specs/<spec-folder>/tasks.md`
- `.agent-os/recaps/`
