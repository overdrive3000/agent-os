---
description: Service Planning Rules for SRE-focused projects
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Service Planning Rules

## Overview

Create foundational documentation for an SRE-oriented project. Capture reliability goals, environments, infrastructure tooling, and roadmap items that focus on operational excellence.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="gather_service_input">

### Step 1: Gather Service Input

Collect core information before generating documentation. Ask numbered questions until you have:

<required_inputs>
  - Primary service/platform description
  - Critical user journeys or workloads
  - Target environments (dev/staging/prod/etc.)
  - Reliability goals (SLO/SLA targets or uptime expectations)
  - Compliance or security constraints
  - Infrastructure tooling preferences (cloud, IaC, deployment pipeline)
</required_inputs>

<fall_back_sources>
  1. `@.agent-os/standards/tech-stack.md`
  2. `@.agent-os/standards/best-practices.md`
  3. Tool-specific configuration (Cursor rules, CLAUDE.md)
</fall_back_sources>

<missing_info_template>
  Please provide the following to initialize the service plan:
  1. Service or platform name & brief description
  2. Critical workloads or user journeys it must support
  3. Environments we manage (dev/staging/prod/etc.)
  4. Target SLO/SLA or uptime goal
  5. Preferred cloud/IaC/deployment tooling stack
</missing_info_template>

</step>

<step number="2" name="create_structure">

### Step 2: Create Documentation Structure

Ensure the `.agent-os/product/` directory exists with the following files:

<file_structure>
  .agent-os/
  └── product/
      ├── mission.md
      ├── mission-lite.md
      ├── tech-stack.md
      └── roadmap.md
</file_structure>

</step>

<step number="3" name="create_mission_md">

### Step 3: Create mission.md

Populate `mission.md` with an SRE-focused template.

<file_template>
  <header>
    # Service Mission
  </header>
  <sections>
    - Service Overview
    - Critical Consumers & Workloads
    - Reliability Goals
    - Key Dependencies
    - Compliance & Guardrails
  </sections>
</file_template>

<section name="overview">
  <template>
    ## Service Overview
    [Service name] provides [capability] for [audience]. The service currently operates in [environments].
  </template>
</section>

<section name="consumers">
  <template>
    ## Critical Consumers & Workloads
    - **[Consumer]** – [Why they rely on the service]
    - **[Workload]** – [Peak usage details]
  </template>
</section>

<section name="reliability">
  <template>
    ## Reliability Goals
    - SLO Target: [Availability or latency target]
    - Error Budget: [Monthly/Quarterly allowance]
    - Recovery Objectives: RTO [value], RPO [value]
  </template>
</section>

<section name="dependencies">
  <template>
    ## Key Dependencies
    - [Dependency] – [Impact if unavailable]
  </template>
</section>

<section name="compliance">
  <template>
    ## Compliance & Guardrails
    - [Control requirement] – [Process/tool]
  </template>
</section>

</step>

<step number="4" name="create_tech_stack_md">

### Step 4: Create tech-stack.md

Document the infrastructure tooling and operational ecosystem.

<file_template>
  <header>
    # Infrastructure Stack
  </header>
</file_template>

<required_items>
  - cloud_provider
  - IaC_tooling (Terraform, Pulumi, Crossplane, etc.)
  - configuration_management (Ansible, Chef, etc.)
  - deployment_pipeline (GitHub Actions, ArgoCD, Spinnaker)
  - container_or_runtime (Kubernetes, ECS, VMs)
  - secrets_management
  - observability_tooling (metrics, logs, tracing)
  - incident_management (PagerDuty, Opsgenie)
  - compliance_tooling or policy controls
  - backup_and_restore strategy
</required_items>

<data_resolution>
  IF an item is missing:
    1. Check `.agent-os/standards/tech-stack.md`
    2. Check `.agent-os/standards/best-practices.md`
    3. Ask the user for confirmation or alternatives
</data_resolution>

<missing_items_template>
  Please provide details for these tech stack items:
  [NUMBERED_LIST]

  Respond with the chosen tool/service or "n/a" if not applicable.
</missing_items_template>

</step>

<step number="5" name="create_mission_lite_md">

### Step 5: Create mission-lite.md

Generate a concise reference for quick context loads.

<file_template>
  <header>
    # Service Mission (Lite)
  </header>
</file_template>

<content_template>
  [One-sentence elevator pitch from mission.md]

  [1-2 sentences covering target consumers, primary reliability goal, and notable guardrails.]
</content_template>

</step>

<step number="6" name="create_roadmap_md">

### Step 6: Create roadmap.md

Lay out operational initiatives across phases.

<file_template>
  <header>
    # Operational Roadmap
  </header>
</file_template>

<phase_structure>
  <phase_template>
    ## Phase [NUMBER]: [Name]

    **Goal:** [Operational improvement]
    **Risk Level:** [Low/Medium/High]

    ### Initiatives
    - [ ] [Initiative] – [Outcome] `[Effort: S/M/L]`

    ### Dependencies
    - [Prerequisite or coordination]
  </phase_template>
</phase_structure>

<phase_guidelines>
  - Phase 1: Stabilize baseline (monitoring, backups, access controls)
  - Phase 2: Improve resilience (auto-healing, scaling, failover)
  - Phase 3: Optimize operations (automation, toil reduction, cost)
</phase_guidelines>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
