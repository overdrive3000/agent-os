# Agent OS Parent Task Guidance

Use this guide when executing a single parent task from `tasks.md`.

## Step 1: Understand the Task
- Read the parent task and all subtasks in `tasks.md`.
- Capture inputs, outputs, dependencies, and test expectations.

## Step 2: Technical Alignment
- Search `sub-specs/technical-spec.md` for sections that mention this functionality.
- Confirm integration points, data flows, and performance requirements.

## Step 3: Standards Reminder
- Review relevant sections from best-practices and code-style guides.
- Pull language-specific style references if editing HTML/CSS/JS or other languages.

## Step 4: Execute Subtasks in Order
1. Write or update tests (if first subtask). Ensure they fail for the right reason.
2. Implement functionality step-by-step, keeping tests green after each change.
3. Run focused tests (unit/integration) for the affected components.
4. Update docs or supporting files if subtasks call for it.
5. Mark each subtask `[x]` upon completion. Use `⚠️` for blockers after three attempts.

## Step 5: Verify & Report
- Re-run targeted tests; share pass/fail context.
- Summarize changes, note issues, and highlight follow-up work before moving to the next parent task.
