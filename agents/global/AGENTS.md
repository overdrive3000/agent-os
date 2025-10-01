# Agent OS Global Guidance

## Standards First
- Keep your local standards up to date in `~/.agent-os/standards/`.
- Use the tech stack, code style, and best practices files as canonical references.
- When you customize standards, re-run project installation so teams inherit the updates.

## Command-Driven Workflow
1. `/plan-product` or `/analyze-product` to align on product context.
2. `/create-spec` to capture requirements and technical approach.
3. `/create-tasks` to translate specs into a TDD-friendly task list.
4. `/execute-tasks` to implement and deliver the feature.
5. `/post-execution-tasks` automatically runs inside `/execute-tasks` to finalize work.

## Meta Rules
- Always review generated documents before moving to the next command.
- Maintain human oversight: confirm plans, adjust tasks, and sign off on tests.
- Keep context lean by referencing lite versions when available (mission-lite, spec-lite, etc.).

## Tool Usage
- Cursor and Codex users should install the Agent OS command packs so `/` commands or saved prompts map to this workflow.
- Commands load layered `AGENTS.md` files from global, project, and spec directories—longest path wins.
- MCP integrations or Cursor rules can supplement these instructions but do not replace them.
