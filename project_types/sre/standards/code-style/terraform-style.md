# Terraform Style Guide

## Structure
- Use one module per directory with `main.tf`, `variables.tf`, `outputs.tf`, and optional `locals.tf`.
- Group related resources using comment headers (`# Networking`, `# IAM`).
- Keep modules small and composable; avoid 1000+ line modules.

## Formatting
- Always run `terraform fmt` before committing.
- Align `=` signs only via `terraform fmt`; do not hand-format.
- Use double quotes for strings and avoid trailing spaces.

## Variables & Outputs
- Declare variables in `variables.tf` with descriptions and type hints.
- Provide sensible defaults for non-production values; require explicit input for production-critical parameters.
- Outputs must be prefixed to avoid collisions when consumed by other stacks.

## State & Backends
- Configure remote state with locking (S3 + DynamoDB, GCS + Firestore).
- Never change backends without an explicit migration plan documented in the spec.
- When adding new workspaces, document their purpose and initialization steps.

## Validation & Policies
- Validate code with `tflint`.
- Keep provider and module versions pinned using the `required_providers` and `required_version` blocks.
- Summarize `terraform plan` output in reviews; highlight create/replace/destroy operations.
