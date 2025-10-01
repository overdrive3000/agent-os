---
description: Create an SRE spec for infrastructure and operations changes
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Spec Creation Rules

## Overview

Capture the information required to deliver a safe, reviewable infrastructure change. Emphasize desired state, validation, rollout, and observability updates over application feature narratives.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="spec_initiation">

### Step 1: Spec Initiation

Either select the next roadmap item tagged for SRE work or accept the user’s stated change request. Treat migrations, infrastructure upgrades, runbook automation, and reliability improvements as valid inputs.

<option_a>
  <trigger>user asks "what's next?"</trigger>
  <actions>
    1. Review `.agent-os/product/roadmap.md` for open SRE initiatives
    2. Choose the next unchecked item
    3. Confirm with the user before proceeding
  </actions>
</option_a>

<option_b>
  <trigger>user provides a specific reliability or infrastructure request</trigger>
  <actions>
    - Accept the request as-is
    - Continue to context gathering
  </actions>
</option_b>

</step>

<step number="2" name="context_gathering">

### Step 2: Context Gathering (Conditional)

Load the minimum context needed to understand operational expectations.

<context_sources>
  - `.agent-os/product/mission-lite.md`
  - `.agent-os/product/tech-stack.md`
  - `.agent-os/product/roadmap.md` (if the item links to future phases)
  - Existing runbooks or observability notes referenced in the roadmap/spec request
</context_sources>

<instructions>
  ACTION: Summarize relevant SLOs, compliance needs, and environment details
  LIMIT: Do not duplicate large documents in the prompt—extract only the parts tied to this change
</instructions>

</step>

<step number="3" name="requirements_clarification">

### Step 3: Requirements Clarification

Ask targeted questions (numbered) to close gaps. Prioritize clarity on blast radius, environments, validation, and approvals.

<clarification_topics>
  - Target environments (dev/staging/prod)
  - Expected reliability or capacity improvements
  - Change window/maintenance considerations
  - Required approvals (CAB, security, compliance)
  - Observability updates (alerts, dashboards)
</clarification_topics>

</step>

<step number="4" name="date_determination">

### Step 4: Determine Date

Capture the current date (`date +%Y-%m-%d`) for folder naming.

</step>

<step number="5" name="spec_folder_creation">

### Step 5: Create Spec Folder

Create `.agent-os/specs/YYYY-MM-DD-spec-name/` with a descriptive kebab-case name (max 5 words). The name should reflect the infrastructure change, e.g., `aws-alb-upgrade` or `cluster-autoscaler-tuning`.

</step>

<step number="6" name="create_spec_md">

### Step 6: Create spec.md

Create `.agent-os/specs/YYYY-MM-DD-spec-name/spec.md` using this template:

<file_template>
  <header>
    # SRE Change Spec

    > Spec: [SPEC_NAME]
    > Created: [CURRENT_DATE]
  </header>
  <sections>
    - Overview
    - Objectives & Success Criteria
    - Scope
    - Out of Scope
    - Dependencies & Coordination
    - Validation Plan
    - Rollback & Contingency
  </sections>
</file_template>

<section name="overview">
  <template>
    ## Overview
    [1-2 sentence summary of the desired state and motivation]
  </template>
</section>

<section name="objectives">
  <template>
    ## Objectives & Success Criteria
    1. [Objective tied to SLO/capacity/security]
    2. [Objective tied to automation or toil reduction]
  </template>
</section>

<section name="scope">
  <template>
    ## Scope
    - [Environment or system touched]
    - [Resources/modules updated]
    - [Automation or pipelines impacted]
  </template>
</section>

<section name="out_of_scope">
  <template>
    ## Out of Scope
    - [Related areas explicitly untouched]
  </template>
</section>

<section name="dependencies">
  <template>
    ## Dependencies & Coordination
    - [Approvals, change tickets, or cross-team coordination]
    - [External systems or secrets required]
  </template>
</section>

<section name="validation">
  <template>
    ## Validation Plan
    - [Command] – [Purpose]
    - [Command] – [Purpose]
  </template>
</section>

<section name="rollback">
  <template>
    ## Rollback & Contingency
    - [Rollback path or feature flags]
    - [Monitoring signals to watch]
  </template>
</section>

</step>

<step number="7" name="create_spec_lite">

### Step 7: Create spec-lite.md

Create `.agent-os/specs/YYYY-MM-DD-spec-name/spec-lite.md` summarizing the change in 2-3 sentences, focusing on why it matters and how success will be verified.

</step>

<step number="8" name="create_technical_spec">

### Step 8: Create technical-spec.md

Create `sub-specs/technical-spec.md` capturing the technical implementation details for the change.

<file_template>
  <header>
    # Technical Specification

    This file describes the planned implementation for @.agent-os/specs/YYYY-MM-DD-spec-name/spec.md
  </header>
  <sections>
    - Resources & Modules
    - Configuration Changes
    - Tooling Commands
    - Observability / Policy Updates
  </sections>
</file_template>

<section name="resources">
  <template>
    ## Resources & Modules
    - [Terraform module or manifest path] – [Role]
    - [Pipeline or automation name] – [Change]
  </template>
</section>

<section name="configuration">
  <template>
    ## Configuration Changes
    - [Parameter] from `[current]` to `[target]`
  </template>
</section>

<section name="tooling">
  <template>
    ## Tooling Commands
    - `terraform plan -var-file=...`
    - `kubectl apply --server-side --dry-run=client`
  </template>
</section>

<section name="observability">
  <template>
    ## Observability / Policy Updates
    - [Alert or dashboard adjustments]
    - [Policy checks or guardrails]
  </template>
</section>

</step>

<step number="9" name="operational_readiness">

### Step 9: Create operational-readiness.md (Conditional)

If the change requires detailed rollout instructions, create `sub-specs/operational-readiness.md`.

<decision_tree>
  IF change impacts production or requires coordination:
    CREATE file
  ELSE:
    SKIP
</decision_tree>

<file_template>
  <header>
    # Operational Readiness

    This file outlines rollout, monitoring, and rollback checkpoints for the change in @.agent-os/specs/YYYY-MM-DD-spec-name/spec.md
  </header>
  <sections>
    - Rollout Steps
    - Approval Checklist
    - Monitoring & Alerting
    - Rollback Triggers
  </sections>
</file_template>

</step>

<step number="10" name="security_considerations">

### Step 10: Create security-review.md (Conditional)

If the change introduces new public endpoints, adjusts IAM, or alters encryption settings, create `sub-specs/security-review.md` summarizing required controls and reviews.

</step>

<step number="11" name="user_review">

### Step 11: Request User Review

Present the generated files for review and await approval or revisions.

<review_prompt>
  I've prepared the SRE change documentation:
  - Spec: @.agent-os/specs/YYYY-MM-DD-spec-name/spec.md
  - Summary: @.agent-os/specs/YYYY-MM-DD-spec-name/spec-lite.md
  - Technical Spec: @.agent-os/specs/YYYY-MM-DD-spec-name/sub-specs/technical-spec.md
  [INCLUDE_OPTIONAL_FILES_CREATED]

  Please review and let me know if updates are needed before I create the task checklist.
</review_prompt>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
