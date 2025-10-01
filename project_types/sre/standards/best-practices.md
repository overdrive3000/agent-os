# SRE Best Practices

## Change Management Principles
- Plan changes in small, reversible increments and document blast radius up front.
- Capture validation commands (plan/diff, lint, policy checks) before opening a review.
- Never apply Terraform or Kubernetes changes without a reviewed plan/diff and explicit approval when production is affected.
- Treat change tickets and pull requests as single sources of truth—link plan outputs, validation notes, and rollout steps in one place.

## Infrastructure as Code
- All infrastructure updates should flow through version-controlled IaC (Terraform, Helm, Ansible, etc.); avoid manual console edits.
- Keep modules and manifests idempotent and environment-agnostic—use variables and workspaces rather than copy-pasting values.
- Prefer composition over giant modules; document ownership for each module or chart.
- Store state in remote backends with locking enabled. Never commit state files.

## Validation & Tooling
- Always run formatters (`terraform fmt`, `yamlfmt`) and validators (`terraform validate`, `tflint`, `kubeval`, `conftest`) before requesting review.
- Include `terraform plan`, `terraform show`, `kubectl diff`, or `helm diff` output in reviews. Summaries must call out destructive operations.
- Policy packs (OPA, Sentinel, Config Sync) should be part of pre-merge CI; surface failures as blockers, not warnings.
- Only run integration/e2e suites when specifically required; prefer fast static validation so feedback cycles stay tight.

## Observability & Reliability
- Every production-impacting change must list the metrics and alerts to monitor during rollout.
- Keep dashboards and alert policies versioned alongside IaC; avoid editing in the UI without backporting into code.
- Track SLOs and error budgets; pause risky rollouts if the budget is exhausted.

## Security & Compliance
- Principle of least privilege for IAM roles and Kubernetes RBAC; justify any broad permissions in the spec.
- Encrypt data at rest and in transit by default; document exceptions with compensating controls.
- Rotate secrets via automated tooling; never paste secrets into specs or code reviews.

## Incident & Rollback Preparedness
- Capture rollback procedures and triggers in every spec (even if the step is “re-run previous manifest”).
- After incidents, document learnings in the roadmap and update runbooks or automation to prevent recurrence.
- Keep on-call documentation current and linked from mission.md or relevant specs.
