# Bash Script Style Guide

## General Practices
- Target POSIX shells when portable; otherwise state the required shell in the shebang (e.g., `#!/usr/bin/env bash`).
- Keep scripts idempotent and safe to re-run; rely on functions instead of long linear flows.
- Fail fast with `set -euo pipefail` and use `IFS=$'\n\t'` when iterating over user-provided data.
- Quote **all** variables (`"$VAR"`) unless word-splitting is explicitly desired.

## Structure
- Organize scripts into sections: header, configuration, functions, main execution block.
- Place global constants in all-caps near the top and document required environment variables.
- Use functions for logical units of work; include short comments when intent is non-obvious.
- Exit explicitly with meaningful status codes (`exit 0`, `exit 1`).

## Safety & Error Handling
- Validate inputs using guard clauses before acting (`[[ -n "$VAR" ]] || { echo "..."; exit 1; }`).
- Prefer `[[ ... ]]` for tests, avoiding legacy `[ ... ]` semantics when using bash.
- Use `trap` to clean up temporary files or to reset state on exit.
- When invoking destructive commands, add dry-run/confirmation options and log actions.

## Tooling & Validation
- Run `shellcheck` locally and in CI; treat warnings as blockers unless justified.
- Use `shfmt` or a consistent formatter to enforce indentation and spacing (2 or 4 spaces, avoid tabs).
- Log commands being executed for troubleshooting (`set -x` or custom logging function) but disable verbose output before handling secrets.
- Keep scripts executable (`chmod +x`) and add integration tests only when the spec requires them.

## Portability & Dependencies
- Avoid bash-specific features when POSIX compliance is needed; otherwise leverage arrays and `mapfile` for clarity.
- Check for required binaries at startup and emit friendly error messages.
- Store reusable helpers in a `lib/` directory and source them with path validation (`source "$(dirname "$0")/../lib/common.sh"`).

## Documentation
- Include usage/help text (`usage()` function) and support `-h|--help` flags.
- Document exit codes and side effects at the top of the script.
- Keep README or inline comments up to date when operational procedures change.
