# Codebase Stack

This repository is primarily **Markdown configuration** for VS Code Copilot “Custom Agents” (agent definition files), plus documentation for publishing them via GitHub Gist and installing them via VS Code deep links.

| Layer | Technology | Version / Identifier | Where seen | Notes |
|---|---|---|---|---|
| Platform | Visual Studio Code / VS Code Insiders | N/A | `AGENTS_GIST.md`, `.planning/research/VSCODE_INSTALL_FORMAT.md` | Uses Copilot agent install deep links (`vscode:chat-agent/install?...`). |
| AI Feature | GitHub Copilot Chat – Custom Agents | N/A | `.github/agents/*.agent.md` frontmatter | Agent definitions are Markdown with YAML frontmatter. |
| Agent Packaging | GitHub Gist (multi-file) | N/A | `GIST_PUBLISHING_GUIDE.md`, `AGENTS_GIST.md` | Uses `gist.githubusercontent.com/.../raw/.../*.agent.md` URLs for installability. |
| Docs/Markup | Markdown + YAML frontmatter | N/A | All `*.agent.md` | Frontmatter keys: `name`, `description`, `model`, `tools`. |
| “Tooling integration” | Context7 MCP extension | `Upstash.context7-mcp` | `AGENTS_GIST.md`, agent docs | Used conceptually by Researcher/Planner/Coder/Designer/Debugger via `context7/*` tool entries. |
| “Tooling integration” | GitHub MCP tools | `github/*` | `coder.agent.md` tools list | Available to Coder when supported by the Copilot environment. |
| CLI | GitHub CLI (`gh`) | v2+ implied | `GIST_PUBLISHING_GUIDE.md` | Used to publish a multi-file Gist (`gh gist create ...`). |
| Shell | PowerShell | 5.1+ (doc claim) | `GIST_PUBLISHING_GUIDE.md` | Publishing guide uses PowerShell line continuations and cmdlets. |

## Models referenced (metadata)

Agent files declare models in frontmatter (examples):
- Orchestrator: `Claude Sonnet 4.5 (copilot)`
- Researcher/Planner: `GPT-5.2 (copilot)`
- Coder/Debugger: `Claude Opus 4.6 (copilot)`
- Designer: `Gemini 3 Pro (Preview) (copilot)`
- Verifier: `Claude Sonnet 4.5 (copilot)`

These should be treated as **intent/positioning metadata**; actual availability depends on the user’s Copilot plan, org policy, and VS Code build.

## Important repo-specific note

The repo includes `.github/agents/` but also has `.gitignore` ignoring `.github/` entirely, which can prevent sharing the “canonical” agent folder via git. See `.planning/codebase/CONCERNS.md`.