# Execute Tasks

Run the implementation workflow for one or more parent tasks in the active spec.

Use the layered guidance provided by Agent OS:
- Global context: `@AGENTS.md`
- Project context: `@./AGENTS.md`
- Spec execution guidance: `@.agent-os/specs/<spec-folder>/AGENTS.md`
- Parent task guidance (optional): `@.agent-os/specs/<spec-folder>/tasks/AGENTS.md`
- Workflow details: `@.agent-os/instructions/core/execute-tasks.md`

Follow the three-phase loop: pre-execution setup, per-task implementation (reusing `execute-task` guidance), and post-execution wrap-up.
