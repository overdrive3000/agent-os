# Kubernetes Manifest Style Guide

## File Organization
- Keep base manifests under `k8s/base/` and environment overlays under `k8s/overlays/<env>/` (Kustomize) or Helm values files.
- One resource per file unless they are tightly coupled (e.g., Service + Endpoints).
- Name files after the resource (`deployment-app.yaml`, `service-app.yaml`).

## YAML Conventions
- Use two-space indentation.
- Alphabetize keys within `metadata` and `labels` blocks for readability.
- Prefer full API versions (e.g., `apps/v1`) and stay current with supported versions.

## Resource Guidelines
- Always set resource requests/limits for workloads.
- Include liveness and readiness probes where applicable.
- Use ConfigMaps and Secrets for configuration; mount secrets read-only.
- For controllers (Deployments, StatefulSets), set a rolling update strategy explicitly.

## Validation
- Run `kubectl apply --dry-run=server` or `kubectl diff` before merging.
- Validate manifests with `kubeonform`.
- Document any required manual post-deploy steps in the spec or recap.
