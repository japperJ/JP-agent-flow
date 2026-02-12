# Code and File Conventions

This project’s conventions are primarily **documentation conventions** and **agent instruction conventions**.

## Agent definition conventions (`*.agent.md`)

### File naming
- Agent files are named `*.agent.md`.
- Agents are duplicated in both `Agents/` and `.github/agents/`.

### YAML frontmatter
Each `*.agent.md` begins with YAML frontmatter containing:
- `name`: agent name (e.g., `Orchestrator`, `Planner`)
- `description`: one-line purpose
- `model`: the target model label (e.g., `GPT-5.2 (copilot)`)
- `tools`: list of allowed tools for the agent

Evidence: any file under `Agents/*.agent.md`.

### Responsibility boundaries
A strong, repeated pattern across agent definitions:
- **Orchestrator**: delegates only; no editing/executing.
- **Researcher/Planner**: write docs and artifacts; do not implement.
- **Coder/Designer**: implement.
- **Verifier**: independently validates; “Task completion ≠ Goal achievement”.
- **Debugger**: hypothesis-driven; persistent debug logs.

### Relative paths are mandatory
Agents are instructed to use **relative paths** in `.planning/` references (e.g., `.planning/research/SUMMARY.md`) rather than absolute filesystem paths.

Evidence: `Agents/orchestrator.agent.md` (“Path References in Delegation”), plus similar rules in other agents.

## Planning artifacts conventions (`.planning/`)

### Directory contract (expected)
The docs repeatedly describe an expected contract:
- `.planning/research/*`
- `.planning/phases/<n>/*`
- `.planning/debug/*`
- `.planning/codebase/*`

### Frontmatter in planning artifacts
Plans and verification outputs are expected to use **YAML frontmatter** to encode structured metadata, especially:
- `must_haves` (Planner)
- `gaps` (Verifier)
- phase identifiers, plan numbers, dependencies

Evidence: examples embedded in `Agents/planner.agent.md` and `Agents/verifier.agent.md`.

### “Plans are prompts”
Planner’s major convention: a `PLAN.md` is an executable prompt designed for **one agent in one session**, generally targeting 2–3 tasks per plan.

Evidence: `Agents/planner.agent.md`.

## Documentation conventions

### Publishing documentation
- Uses GitHub CLI (`gh`) and PowerShell snippets.
- Recommends hosting agent files via **Gist raw URLs** for install-link compatibility.

Evidence: `GIST_PUBLISHING_GUIDE.md` and `.planning/research/VSCODE_INSTALL_FORMAT.md`.

### Install links
Documentation follows the convention:
- Build a deep link (`vscode:chat-agent/install?url=<raw-agent-url>`)
- URL-encode it
- Wrap it with `https://aka.ms/awesome-copilot/install/agent?url=<encoded>`

Evidence: `.planning/research/VSCODE_INSTALL_FORMAT.md`.

## Naming conventions
- Agent names in frontmatter are **Capitalized** (e.g., `Researcher`, `Planner`).
- Many docs warn about “agent name mismatch” and emphasize exact matches.

Evidence: `Agents/README.md`.
