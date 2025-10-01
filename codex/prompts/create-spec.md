# Create Spec (Codex Prompt)

## Usage
```
codex exec --prompt create-spec
```

## Goal
Generate a dated spec folder with requirements, technical approach, and related docs.

## Guidance
- Load layered AGENTS: global, project, and spec (`@.agent-os/specs/<spec-folder>/AGENTS.md`).
- Supply feature context, user stories, constraints, and acceptance criteria.
- Review SRD, technical spec, and supporting files before creating tasks.

### References
- `@.agent-os/instructions/core/create-spec.md`
- `.agent-os/specs/<spec-folder>/`
