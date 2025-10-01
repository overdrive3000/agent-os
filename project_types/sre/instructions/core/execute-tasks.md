---
description: Rules to execute a set of SRE tasks using Agent OS
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Task Execution Rules

## Overview

Execute SRE tasks for a given spec in three phases that keep changes reviewable and operationally safe:
1. Pre-execution alignment
2. Task execution loop with validation-first mindset
3. Post-execution hand-off

Complete every phase before finishing.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

## Phase 1: Pre-Execution Alignment

<step number="1" name="task_selection">

### Step 1: Identify Work Scope

Determine which parent tasks to execute from the spec (using `spec_srd_reference` and optional `specific_tasks`). Default to the next unchecked parent task.

<instructions>
  ACTION: Confirm the task IDs you will work on
  SUMMARIZE: Desired outcomes and environments touched
  FLAG: Dependencies that require coordination before you begin
</instructions>

</step>

<step number="2" name="context_refresh">

### Step 2: Load Operational Context

Gather the minimal context required to safely execute changes.

<context_sources>
  - `.agent-os/specs/<spec-folder>/spec.md` and `spec-lite.md`
  - `.agent-os/specs/<spec-folder>/sub-specs/technical-spec.md`
  - `.agent-os/product/mission-lite.md`
  - `.agent-os/product/roadmap.md` (only if tasks affect roadmap items)
</context_sources>

<instructions>
  ACTION: Refresh yourself on SLOs, guardrails, and environment notes relevant to the selected tasks
  LIMIT: Avoid loading unrelated specs or historical context
  RESULT: Written context recap that justifies the planned changes
</instructions>

</step>

<step number="3" name="workspace_readiness">

### Step 3: Prepare Workspace Safely

Ensure you are working on an isolated git branch (if using git) and that local tooling for validation is available.

<instructions>
  ACTION: Run `git status`
  BRANCH: Create/switch to `<spec-branch>` if not already on it
  VERIFY: Required CLIs (terraform, kubectl, helm, lint tools) are installed; note missing tooling early
  CLEAN: Remove or stash unrelated changes
</instructions>

</step>

## Phase 2: Task Execution Loop

<step number="4" name="sre_task_loop">

### Step 4: Execute Each Task with Validation-First Workflow

Load `@.agent-os/instructions/core/execute-task.md` once, then loop through each selected parent task.

<execution_flow>
  LOAD: SRE execute-task instructions
  FOR each parent task selected:
    RUN: execute-task flow (plan, implement, validate, document)
    UPDATE: `tasks.md` with status and notes
  END FOR
</execution_flow>

<instructions>
  ACTION: Maintain change plans and validation results per task
  PAUSE: If a task requires approvals or cross-team coordination, stop and surface the blocker
  ENSURE: All subtasks complete before moving on
</instructions>

</step>

## Phase 3: Post-Execution Hand-off

<step number="5" name="post_execution">

### Step 5: Finalize Operational Deliverables

After all assigned tasks are complete, run `@.agent-os/instructions/core/post-execution-tasks.md` to capture validation evidence, change summaries, and rollout notes.

<instructions>
  ACTION: Execute the SRE post-execution flow without skipping steps
  FOCUS: Validation outputs, change windows, and operator instructions rather than automated test results
  CONFIRM: User approval before closing the loop if anything remains uncertain
</instructions>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
