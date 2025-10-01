---
description: Finalize infrastructure work and deliver operational hand-off
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Task Completion Rules

## Overview

After finishing SRE tasks, capture validation evidence, update checklists, and prepare operators for rollout. Emphasize reproducible plans over automated test suites.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="validation_evidence">

### Step 1: Collect Validation Evidence

Run the agreed validation commands and record summaries.

<validation_actions>
  - Execute formatters (`terraform fmt`, `yamlfmt`) if changes were made
  - Run validators/linters (`terraform validate`, `tflint`, `kubeval`, `conftest`, etc.)
  - Generate plans or diffs (`terraform plan`, `kubectl diff`, `helm diff`)
  - Capture noteworthy output for reviewers (planned resource changes, manifest diffs)
</validation_actions>

<instructions>
  ACTION: Document commands executed and key findings in your response
  NOTE: Only run automated integration/e2e tests if explicitly requested in the spec or by the user
  FLAG: Any warnings that require human review before applying changes
</instructions>

</step>

<step number="2" name="change_management">

### Step 2: Update Change Records and Version Control

Prepare the change for review and deployment.

<change_management_items>
  - Stage and commit changes with a descriptive message (if using git)
  - Update change tickets or request IDs referenced in the spec
  - Store plan/diff artifacts if your process requires attachments
  - Push the branch only when validation evidence is captured
</change_management_items>

<instructions>
  ACTION: Run `git status` to ensure only intended files are staged
  INCLUDE: Validation summary in the commit or PR description
  OPTIONAL: Provide PR URL if one is created
</instructions>

</step>

<step number="3" name="tasks_check">

### Step 3: Update tasks.md

Ensure every parent task and subtask in `tasks.md` is checked off or marked as blocked.

<instructions>
  ACTION: Mark completed steps with `[x]`
  RECORD: Use `⚠️ Blocking:` notes if follow-up work is still required (e.g., awaiting approval)
  VERIFY: Validation notes are referenced from the appropriate subtasks
</instructions>

</step>

<step number="4" name="roadmap_update">

### Step 4: Roadmap Update (Conditional)

Only update `.agent-os/product/roadmap.md` if the completed tasks satisfy a roadmap milestone or operational goal.

<instructions>
  ASSESS: Whether the roadmap item was fully addressed
  UPDATE: Mark items `[x]` and add concise notes when applicable
  SKIP: If work is partial or needs production rollout to complete
</instructions>

</step>

<step number="5" name="recap_document">

### Step 5: Create Recap Document

Create `.agent-os/recaps/<spec-folder>.md` summarizing the change and validation steps.

<recap_template>
  # [yyyy-mm-dd] Recap: [Spec Name]

  This summarizes the infrastructure change documented at .agent-os/specs/[spec-folder]/spec.md.

  ## Change Summary
  - [High-level outcome]
  - [Key resources touched]
  - [Validation commands executed]

  ## Operational Notes
  - Rollout window / deployment steps
  - Required approvals or tickets
  - Rollback guidance

  ## Context
  [Copy summary from spec-lite.md]
</recap_template>

<instructions>
  ACTION: Populate the recap with the latest information
  ENSURE: Operators can understand the status without re-reading the entire spec
</instructions>

</step>

<step number="6" name="completion_summary">

### Step 6: Deliver Completion Summary

Provide the user with a concise report covering the work performed, validation evidence, and next steps.

<summary_template>
  ## ✅ Work Completed
  1. **[CHANGE_1]** – [RESULT]
  2. **[CHANGE_2]** – [RESULT]

  ## 🔍 Validation
  - [COMMAND] → [OUTCOME]
  - [COMMAND] → [OUTCOME]

  ## 🚦 Ready to Roll Out
  - [Manual step or approval still needed]
  - [Links to plan artifacts or tickets]

  ## 📦 Pull Request / Ticket
  [PR or change record link if created]
</summary_template>

<instructions>
  ACTION: Highlight remaining approvals or follow-up work
  INCLUDE: Links to plans, diffs, or documentation updates
  STATE: If the change is safe to apply or requires further validation
</instructions>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
