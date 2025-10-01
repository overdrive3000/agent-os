---
description: Create a tasks list for infrastructure and operations work
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Task Planning Rules

## Overview

Translate the approved SRE spec into a reviewable `tasks.md` organized around small, independently verifiable changes. Keep work items focused on infrastructure state updates, automation, and operational readiness.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="create_tasks">

### Step 1: Create tasks.md

Create `tasks.md` inside the current spec folder. Use the template below and tailor it to the change, keeping subtasks limited to operationally meaningful steps.

<file_template>
  <header>
    # Spec Tasks
  </header>
</file_template>

<task_structure>
  <major_tasks>
    - 1-5 parent tasks grouped by environment or resource boundary
    - Use numbered checklist format
  </major_tasks>
  <subtasks>
    - Up to 6 per parent task
    - Use decimal notation (1.1, 1.2)
    - Begin with state capture & validation planning
    - End with documentation/approvals rather than “run all tests”
  </subtasks>
</task_structure>

<task_template>
  ## Tasks

  - [ ] 1. [MAJOR_TASK_DESCRIPTION]
    - [ ] 1.1 Capture current state & outline validation commands
    - [ ] 1.2 Implement configuration changes (Terraform/Kubernetes/etc.)
    - [ ] 1.3 Run linters/validators and review plans or diffs
    - [ ] 1.4 Document rollout plan, approvals, and follow-up actions

  - [ ] 2. [MAJOR_TASK_DESCRIPTION]
    - [ ] 2.1 Capture current state & outline validation commands
    - [ ] 2.2 Implement configuration changes
    - [ ] 2.3 Validate and record results
    - [ ] 2.4 Prepare operator notes / change ticket update
</task_template>

<ordering_guidelines>
  - Group work by blast radius or dependency chain (network → compute → services)
  - Split risky changes into multiple parent tasks so each can be reviewed independently
  - Call out manual approvals or change windows as individual subtasks
  - Include contingency items (rollback prep, feature flags) when required by the spec
</ordering_guidelines>

</step>

<step number="2" name="execution_readiness">

### Step 2: Confirm Ready-to-Execute Plan

Share the first parent task with the user, emphasizing validation strategy and operational risk.

<readiness_summary>
  <present>
    - Spec name & objective
    - First parent task title with quick rationale
    - Key validation commands you plan to run
    - Any approvals or coordination needed before executing
  </present>
</readiness_summary>

<execution_prompt>
  PROMPT: "The SRE task plan is ready. The first work item is:

  **Task 1:** [FIRST_TASK_TITLE]
  [SUMMARY OF KEY SUBTASKS AND VALIDATION STEPS]

  I will execute Task 1 once you confirm. Let me know if you want any adjustments before we proceed."
</execution_prompt>

<instructions>
  ACTION: Wait for explicit user approval before running `/execute-tasks`
  ADJUST: Update the checklist if the user requests changes
</instructions>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
