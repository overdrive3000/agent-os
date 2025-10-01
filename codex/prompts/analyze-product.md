# Analyze Product (Codex Prompt)

## Usage
```
codex exec --prompt analyze-product
```

## Goal
Inspect an existing repository and document its current state in `.agent-os/product/`.

## Guidance
- Load layered AGENTS: global `@AGENTS.md`, project `@./AGENTS.md`.
- Provide answers about completed work, roadmap status, and technical decisions.
- Validate generated documentation, especially Phase 0 roadmap entries.

### References
- `@.agent-os/instructions/core/analyze-product.md`
- `.agent-os/product/`
