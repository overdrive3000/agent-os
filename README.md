<img width="1280" height="640" alt="agent-os-og" src="https://github.com/user-attachments/assets/f70671a2-66e8-4c80-8998-d4318af55d10" />

## Your system for spec-driven agentic development.

[Agent OS](https://buildermethods.com/agent-os) transforms AI coding agents from confused interns into productive developers. With structured workflows that capture your standards, your stack, and the unique details of your codebase, Agent OS gives your agents the specs they need to ship quality code on the first try—not the fifth.

Use it with:

✅ Claude Code, Cursor, or any other AI coding tool.

✅ New products or established codebases.

✅ Big features, small fixes, or anything in between.

✅ Any language or framework.

### Command-Driven Workflow

Agent OS ships layered `AGENTS.md` instructions plus command packs for Cursor and Codex so humans can trigger the same `/plan-product`, `/create-spec`, `/create-tasks`, and `/execute-tasks` flows in any tool. Install the base system, customize `~/.agent-os/agents/`, and run the provided installers to copy the packs into each project.

### Using Agent OS with Cursor

- **Base install (once per machine)**
  ```bash
  curl -sSL https://raw.githubusercontent.com/overdrive3000/agent-os/main/setup/base.sh | bash -s -- --cursor
  ```
  This seeds `~/.agent-os/` with standards, instructions, layered AGENTS templates, and the Cursor command pack.
- **Customize defaults**: edit `~/.agent-os/standards/` and `~/.agent-os/agents/` so future projects inherit your opinions.
- **Project install**:
  ```bash
  cd /path/to/project
  ~/.agent-os/setup/project.sh --cursor
  ```
  The script copies Agent OS into `.agent-os/` and places reusable chat commands in `.cursor/commands/`.
- **Run commands**: inside Cursor chat type `/plan-product`, `/create-spec`, `/create-tasks`, `/execute-tasks`, or `/analyze-product`. Each command loads the layered AGENTS files plus the detailed instructions from `.agent-os/instructions/core/`.
- **Keep in sync**: when standards or AGENTS change, rerun the project installer (with `--overwrite-*` flags as needed) so `.cursor/commands/` stays current.

### Using Agent OS with Codex CLI

- **Base install** (adds Codex prompt pack alongside standards/agents):
  ```bash
  curl -sSL https://raw.githubusercontent.com/buildermethods/agent-os/main/setup/base.sh | bash -s --
  ```
  Add `--cursor` or `--claude-code` if you also use those tools.
- **Customize defaults**: edit `~/.agent-os/standards/` and `~/.agent-os/agents/` for your global guidance.
- **Project install**:
  ```bash
  cd /path/to/project
  ~/.agent-os/setup/project.sh
  ```
  The project copy lives in `.agent-os/` and includes prompt templates under `.agent-os/codex/prompts/`.
- **Prompts are synced automatically**: the installer copies Agent OS prompts to `.agent-os/codex/prompts/` and mirrors them to `~/.codex/prompts/`. Restart Codex CLI if it was already running.
- **Invoke workflows**: launch `codex` and use slash commands `/plan-product`, `/analyze-product`, `/create-spec`, `/create-tasks`, and `/execute-tasks`. Each prompt pulls in the layered AGENTS plus `.agent-os/instructions/core/` guidance.
- **Refresh when updating**: after modifying AGENTS or standards, rerun the project installer (with overwrite flags as needed) so both the project copy and `~/.codex/prompts/` stay current.

---

### Documentation & Installation

Docs, installation, useage, & best practices 👉 [It's all here](https://buildermethods.com/agent-os)

---

### Created by Brian Casel @ Builder Methods

Created by Brian Casel, the creator of [Builder Methods](https://buildermethods.com), where Brian helps professional software developers and teams build with AI.

Get Brian's free resources on building with AI:
- [Builder Briefing newsletter](https://buildermethods.com)
- [YouTube](https://youtube.com/@briancasel)

