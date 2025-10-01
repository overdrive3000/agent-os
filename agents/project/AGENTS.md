# Agent OS Project Guidance

## Project Setup
- Ensure `.agent-os/product/` contains `mission.md`, `mission-lite.md`, `tech-stack.md`, and `roadmap.md`.
- For existing products run `/analyze-product`; for net-new products run `/plan-product`.
- Update generated docs immediately after each command so future runs stay accurate.

## Command Catalog
- `/plan-product` — builds mission, roadmap, and tech stack docs for new products.
- `/analyze-product` — inspects an existing codebase and backfills product docs.
- `/create-spec` — scaffolds `.agent-os/specs/<date>-<name>/` with spec + technical docs.
- `/create-tasks` — writes `tasks.md` for the active spec using numbered parent/subtasks.
- `/execute-tasks` — executes one or more parent tasks, looping through `execute-task` and finishing with post-execution.

## Review Checkpoints
- After `/create-spec`, verify SRD, technical spec, and scope before creating tasks.
- After `/create-tasks`, confirm subtask order, TDD coverage, and acceptance criteria.
- During `/execute-tasks`, monitor progress, approve test outputs, and handle blockers.

## Standards Overrides
- Customize `.agent-os/standards/` inside the project to override global defaults.
- Document deviations in `product/tech-stack.md` or `product/decisions.md` so future specs stay aligned.

## Collaboration Notes
- Commit `.agent-os/` contents so teammates share the same instructions.
- Encourage teammates to run `/execute-tasks` only after confirming branch status and task selection with the human lead.
