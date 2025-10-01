# /analyze-product

Analyze an existing repository and backfill Agent OS product documentation.

## When to run
- Installing Agent OS mid-project.
- Updating product docs after significant manual changes.

## Steps
1. Load layered guidance: `@AGENTS.md` (global) and project `@./AGENTS.md`.
2. Answer the agent’s questions about current state, roadmap, and standards.
3. Review generated product docs and adjust Phase 0/roadmap status to match reality.
4. Commit updates before creating new specs or tasks.

## References
- `@.agent-os/instructions/core/analyze-product.md`
- `@.agent-os/product/`
