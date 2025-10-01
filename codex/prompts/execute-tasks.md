# Execute Tasks (Codex Prompt)

## Usage
```
codex exec --prompt execute-tasks
```

## Goal
Drive the full implementation loop for one or more parent tasks in the spec.

## Guidance
- Load layered AGENTS: global, project, spec, and optional parent-task guidance.
- Confirm which parent task(s) to ship. Default: next unchecked parent task.
- Follow the three-phase workflow (setup, per-task execution, post-execution wrap-up).
- Review diffs, tests, and recap summaries before final delivery.

### References
- `@.agent-os/instructions/core/execute-tasks.md`
- `.agent-os/specs/<spec-folder>/tasks.md`
- `.agent-os/recaps/`
