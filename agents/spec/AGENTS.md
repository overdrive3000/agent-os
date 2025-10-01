# Agent OS Spec Guidance

## Before You Start
- Confirm the spec folder contains `spec.md`, `spec-lite.md`, `sub-specs/technical-spec.md`, and `tasks.md` (after `/create-tasks`).
- Load mission-lite, spec-lite, and technical spec summaries before working.
- Make sure tests and git branches are ready for isolated development.

## Phase 1: Pre-Execution Setup
1. **Task Assignment**  
   - Identify which parent task(s) to deliver now. Default: next unchecked parent task in `tasks.md`.  
   - Confirm scope, dependencies, and acceptance criteria with the human operator.
2. **Context Analysis**  
   - Pull required context (tasks, mission-lite, spec-lite, technical-spec).  
   - Keep responses concise; avoid duplicating context already in the chat.
3. **Branch Management**  
   - Check git status. Create/switch to the spec branch (`<spec-folder>` without the date).  
   - Resolve uncommitted changes before proceeding.

## Phase 2: Task Execution Loop
For each selected parent task, follow this cycle:
1. **Task Understanding**  
   Read the parent task and all subtasks from `tasks.md`. Capture dependencies and expected outputs.
2. **Technical Review**  
   Extract relevant sections from `sub-specs/technical-spec.md` to confirm architecture, integrations, and performance considerations.
3. **Best Practices**  
   Reference applicable standards: best-practices, code-style, and language-specific guides.
4. **Implementation (TDD)**  
   - Write or update tests first if the subtasks call for it.  
   - Implement functionality incrementally, keeping tests passing before moving on.  
   - Refactor as needed while maintaining coverage.
5. **Focused Testing**  
   Run only the tests relevant to the current parent task. Report failures with file/line context and suggested fixes.
6. **Task Status Update**  
   Mark completed subtasks and parent task with `[x]` in `tasks.md`. Document blockers with `⚠️` notes if unresolved after three attempts.

Repeat until all assigned parent tasks are complete.

## Phase 3: Post-Execution Tasks
1. Run the full test suite and resolve failures.  
2. Ensure git branch is up to date; stage and commit changes with descriptive messages.  
3. Update `tasks.md`, roadmap items, and create spec recap in `.agent-os/recaps/`.  
4. Prepare delivery summary (what’s done, issues, testing notes, PR link).  
5. Play completion notification (if supported) to signal the human operator.

## Human Confirmation Points
- Confirm task selection before coding.  
- Review diffs and test outputs before committing.  
- Approve the recap and summary before raising a PR.
