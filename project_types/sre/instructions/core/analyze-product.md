---
description: Analyze existing infrastructure and install Agent OS for SRE projects
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Analyze Existing Platform & Install Agent OS

## Overview

Install Agent OS into an existing infrastructure repository or operations workspace and document the current reliability posture.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="infrastructure_assessment">

### Step 1: Assess Current Infrastructure Artifacts

Review the repository to understand how infrastructure and operations are managed today.

<assessment_focus>
  - IaC layout (Terraform modules, Helm charts, Ansible playbooks)
  - Environment structure (dev/staging/prod parity, state backends)
  - Deployment automation (CI/CD workflows, GitOps manifests)
  - Observability configuration (dashboards, alert rules)
  - Security and compliance artifacts (policies, guardrails)
</assessment_focus>

<instructions>
  ACTION: Map what tooling is in use and where change risk concentrates
  DOCUMENT: Notable patterns, gaps, or manual steps
  NOTE: Existing SLOs/SLA docs, incident runbooks, or playbooks found
</instructions>

</step>

<step number="2" name="gather_operational_context">

### Step 2: Gather Operational Context

Ask the user for business and reliability context that code inspection cannot reveal.

<context_questions>
  1. Which services are considered most critical right now?
  2. What reliability goals (SLO/SLA) are we held to?
  3. Are there active incidents, migrations, or compliance audits underway?
  4. How are changes approved (CAB, ticketing, peer review)?
  5. Any tooling preferences or constraints we should preserve?
</context_questions>

<instructions>
  ACTION: Record responses clearly for later reference
  MERGE: Combine with repository findings to build accurate documentation
</instructions>

</step>

<step number="3" name="run_plan_product">

### Step 3: Run SRE Plan-Product Instructions

Execute `@.agent-os/instructions/core/plan-product.md` using the insights gathered.

<execution_inputs>
  - Main service idea and purpose
  - Key workloads already supported
  - Observed tooling and environment setup
  - Reliability targets and guardrails from the user
</execution_inputs>

</step>

<step number="4" name="refine_docs">

### Step 4: Refine Generated Documentation

Adjust the newly created product docs so they match reality.

<refinement_tasks>
  - Update roadmap with completed initiatives (mark them `[x]` under "Phase 0: Completed")
  - Correct tech stack versions and tooling names
  - Add any missing dependencies discovered during assessment
  - Capture known gaps (e.g., missing runbooks, limited monitoring) in mission.md or roadmap notes
</refinement_tasks>

</step>

<step number="5" name="final_summary">

### Step 5: Provide Summary and Next Steps

Verify all files exist and summarize findings for the user.

<verification_checklist>
  - `.agent-os/product/mission.md`
  - `.agent-os/product/mission-lite.md`
  - `.agent-os/product/tech-stack.md`
  - `.agent-os/product/roadmap.md`
</verification_checklist>

<summary_template>
  ## ✅ Agent OS Installed for SRE Workflows
  - **Stack Overview:** [Key tooling identified]
  - **Reliability Goals:** [SLO/SLA summary]
  - **Current Gaps:** [Notable risks or manual steps]
  - **Immediate Opportunities:** [Top 1-2 roadmap items recommended]

  Next steps: Review the generated docs and confirm priorities before starting new specs.
</summary_template>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
