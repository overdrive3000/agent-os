---
description: Rules to execute an infrastructure or operations task using Agent OS
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Task Execution Rules

## Overview

Execute a single SRE task and its subtasks with a focus on predictable infrastructure changes, validated rollouts, and clear operator hand-off. Prioritize formatting, validation, and controlled change plans over automated testing unless the spec explicitly requires tests.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="task_understanding">

### Step 1: Confirm Desired State

Review the parent task, all subtasks, and the related spec documents to understand the target state, blast radius, and environments affected.

<context_sources>
  - `.agent-os/specs/<spec-folder>/tasks.md`
  - `.agent-os/specs/<spec-folder>/spec.md`
  - `.agent-os/specs/<spec-folder>/sub-specs/technical-spec.md`
  - `.agent-os/product/mission-lite.md`
</context_sources>

<instructions>
  ACTION: Summarize the desired state and why the change is needed
  IDENTIFY: Environments impacted (dev/staging/prod/etc.) and any change windows noted
  CHECK: SLOs, SLIs, or compliance notes called out in the spec
  OUTPUT: Short written plan describing scope before touching code
</instructions>

</step>

<step number="2" name="baseline_review">

### Step 2: Inspect Current State

Capture the existing configuration so you can reason about diffs and provide operators with context for rollback.

<baseline_actions>
  - Review current IaC definitions for the resources in scope (Terraform modules, Helm charts, Kubernetes manifests, pipelines)
  - Note critical dependencies (state backends, secrets, external services)
  - Record the current version, replica counts, or resource sizes that will change
</baseline_actions>

<instructions>
  ACTION: Use read-only commands (`terraform show`, `terraform state list`, `kubectl get`, `kubectl describe`, etc.) as needed
  DOCUMENT: Key findings inline in your plan (include commands run and important values)
  AVOID: Making changes until baseline is documented
</instructions>

</step>

<step number="3" name="change_plan">

### Step 3: Plot the Change

Define the concrete edits you will make and how you will validate them before applying.

<planning_requirements>
  - List files/modules/manifests that need updates
  - Decide on validation commands (fmt, validate, plan, policy checks, lint)
  - Note if coordination with another team or ticket is required
  - Call out any manual approval or change-management steps
</planning_requirements>

<instructions>
  ACTION: Write a brief change outline in your response
  INCLUDE: Rollback or remediation notes if the spec requires them
  CONFIRM: You have all information needed before modifying files
</instructions>

</step>

<step number="4" name="implementation">

### Step 4: Implement Infrastructure Changes

Edit Terraform, Kubernetes, or automation files to reflect the desired state.

<implementation_guidelines>
  - Keep changes scoped to the current task
  - Prefer small, reviewable diffs
  - Update variables, modules, and pipeline files together to avoid drift
  - Maintain formatting standards as you edit
</implementation_guidelines>

<instructions>
  ACTION: Modify the necessary files
  MAINTAIN: Idempotency—avoid hard-coding values that differ per environment
  NOTE: Add concise comments only when operationally helpful (e.g., unusual lifecycle blocks)
</instructions>

</step>

<step number="5" name="validate_changes">

### Step 5: Validate Without Deploying

Verify the change with lightweight tooling instead of applying it.

<validation_suite>
  - Run formatters (`terraform fmt`, `kubectl neat`, `yamlfmt`, etc.)
  - Run static checks (`terraform validate`, `terraform plan`, `kubeval`, `konstraint test`, `tflint`, `hadolint`)
  - Compare generated plans or diffs and summarize notable changes
  - Only run automated tests if the spec specifically asks for them
</validation_suite>

<instructions>
  ACTION: Execute relevant linters/validators for the technologies you touched
  CAPTURE: Key plan or diff output so reviewers can see intended impact
  RESOLVE: Warnings that indicate risk or policy violations; otherwise call them out explicitly
</instructions>

</step>

<step number="6" name="document_results">

### Step 6: Document Outcomes and Next Steps

Summarize what changed, how it was validated, and what an operator should do next.

<documentation_requirements>
  - Update the current task’s subtasks with status notes
  - List validation commands run and their outcomes
  - Provide instructions to reproduce validation locally (`terraform plan -var-file=...`, `kubectl diff`, etc.)
  - Mention approvals or tickets still required before apply
</documentation_requirements>

<instructions>
  ACTION: Record status in `tasks.md`
  DELIVER: A concise change summary with validation evidence and any follow-up required
  FLAG: Outstanding risks or unknowns so they can be reviewed before deployment
</instructions>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
