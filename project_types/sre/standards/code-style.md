# Infrastructure Code Style Guide

## General Conventions
- Keep whitespace clean and rely on tool-provided formatters (`terraform fmt`, `yamlfmt`, `prettier` for JSON/YAML when available).
- Use descriptive file/module names that reflect the resource (e.g., `networking/ingress.tf`, `k8s/base/ingress.yaml`).
- Prefer explicit versions for providers, modules, and container images.
- Document non-obvious decisions with short comments that explain *why* (not *what*).

## Terraform Guidelines
- Follow the structure defined in `code-style/terraform-style.md`.
- One resource per block whenever possible; group related resources with clear headers.
- Keep variable and output descriptions up to date; defaults must be safe for development environments.

## Kubernetes & YAML Guidelines
- Follow the conventions in `code-style/kubernetes-style.md`.
- Separate base manifests from environment overlays (e.g., Kustomize or Helm values).
- Avoid inline credentials or secrets—reference secret objects instead.

## Automation & Shell Scripts
- Follow `code-style/bash-style.md` for Bash-specific conventions.
- Use `set -euo pipefail` in shell scripts and document required environment variables at the top.
- Prefer declarative pipelines (GitHub Actions, GitLab CI, Argo) over ad-hoc scripts when possible; keep steps small and well-named.
- Run `shellcheck` locally and in CI; treat warnings as blockers unless justified.
- Treat CI lint failures as blockers; do not proceed until lint/plan stages succeed.
