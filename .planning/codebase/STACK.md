# Codebase Stack (JP-agent-flow)

## Summary
This repository is primarily a **documentation + configuration** project for a **VS Code GitHub Copilot Chat multi-agent workflow**. It defines a set of Copilot custom agents using `*.agent.md` files with YAML frontmatter, plus documentation for publishing/installation via GitHub Gist.

## Technology Inventory

| Layer | Technology | Where / Evidence | Notes |
|---|---|---|---|
| Primary artifact format | Markdown (`.md`) | Repo root + `Agents/` + `.planning/research/` | All “code” here is instructional content and templates. |
| Agent definition format | Copilot agent Markdown + **YAML frontmatter** | `Agents/*.agent.md`, `.github/agents/*.agent.md` | Frontmatter keys like `name`, `description`, `model`, `tools`. |
| Agent runtime / host | VS Code / VS Code Insiders + GitHub Copilot Chat Agents | Implied by install links and agent file format in `AGENTS_GIST.md` and `.planning/research/VSCODE_INSTALL_FORMAT.md` | The system targets Copilot’s agent framework inside VS Code. |
| Agent-to-agent orchestration | `runSubagent` tool | `Agents/orchestrator.agent.md` | Orchestrator delegates lifecycle tasks to other agents; Orchestrator itself has no edit/execute tools. |
| Planning artifact convention | `.planning/` directory contract | `Agents/*` (multiple) and `.planning/research/AGENTS_DOCUMENTATION.md` | Standardized research/roadmap/phase artifacts; many are templates. |
| External documentation retrieval | Context7 MCP, web search | Declared in multiple agent `tools:` lists (e.g., `context7/*`, `web`) | Researcher/Planner/Coder/Designer expect Context7 usage (“Context7 first”). |
| Shell / scripting (supporting) | PowerShell | `GIST_PUBLISHING_GUIDE.md` | Instructions use `gh` and PowerShell for publishing/updating docs. |
| Publishing / distribution | GitHub Gist (raw file hosting) | `AGENTS_GIST.md`, `GIST_PUBLISHING_GUIDE.md`, `.planning/research/VSCODE_INSTALL_FORMAT.md` | Install links rely on `gist.githubusercontent.com` raw URLs. |
| CLI tooling | GitHub CLI (`gh`) | `GIST_PUBLISHING_GUIDE.md` | Used to create/edit multi-file gists. |
| Version control | Git | Mentioned in `Coder` agent + publishing guide | Repo itself includes `.git/`; Coder agent expects per-task conventional commits. |

## “Frameworks” / Libraries
There are **no application frameworks** (Node/Python/.NET/etc.) in this repo; no `package.json`, `requirements.txt`, `pyproject.toml`, etc. The “system” is the **agent instruction set**, not a running app.

## Key Integration Points
- **VS Code agent install deep links** (HTTP wrapper → `vscode:` / `vscode-insiders:`): documented in `.planning/research/VSCODE_INSTALL_FORMAT.md`.
- **Gist raw hosting**: documented in `AGENTS_GIST.md` + `GIST_PUBLISHING_GUIDE.md`.
