# External Integrations

This repo is itself mostly documentation + agent definitions, but the agent system is designed to integrate with several tools/services when used in a real workspace.

| Integration | Type | Where configured/mentioned | Notes |
|---|---|---|---|
| VS Code Copilot Custom Agents | Platform feature | `.github/agents/*.agent.md` | Agents are installed/recognized by VS Code from agent definition markdown files. |
| `runSubagent` (Copilot agent tool) | Orchestration primitive | `orchestrator.agent.md` | Orchestrator delegates to other agents using this tool (capitalization matters). |
| Context7 MCP | Docs/knowledge tool | `Researcher/Planner/Coder/Designer/Debugger` tools include `context7/*`; also described in `AGENTS_GIST.md` | Recommended to get up-to-date library docs; extension mentioned: `Upstash.context7-mcp`. |
| Web access | Research tool | Tools list includes `web` for several agents | Used by Researcher/Planner/Coder/Designer/Debugger for official docs and web search. |
| GitHub MCP | Repo operations tool | `coder.agent.md` includes `github/*` | Used for GitHub operations when available in the environment. |
| Memory tool | Persistent memory | Orchestrator and others include `memory` | Memory is described as potentially experimental; agents should degrade gracefully. |
| GitHub Gist | Distribution/hosting | `GIST_PUBLISHING_GUIDE.md`, `AGENTS_GIST.md` | Recommended host for raw agent files to avoid `raw.githubusercontent.com` redirect restrictions in install wrapper. |
| GitHub CLI (`gh`) | Publishing automation | `GIST_PUBLISHING_GUIDE.md` | Used to create public multi-file Gists from `Agents/*.agent.md`. |

## Integration patterns

### Install link pattern
Documented in `.planning/research/VSCODE_INSTALL_FORMAT.md`:
- Build deep link: `vscode:chat-agent/install?url=<https_raw_agent_url>` (or `vscode-insiders:`)
- URL-encode deep link
- Wrap with `https://aka.ms/awesome-copilot/install/agent?url=<encoded>` for GitHub-friendly links

### Artifact handoff pattern
All substantive agent-to-agent handoffs are done via **files**, not hidden state:
- `.planning/research/*` → roadmap decisions
- `.planning/phases/N/PLAN.md` → execution
- `.planning/phases/N/VERIFICATION.md` gaps → gap-closure planning

### Shell/tooling portability
Verifier examples rely heavily on bash utilities (`grep`, `wc`, `test -f`). In Windows-first environments, this implicitly integrates with:
- Git Bash, WSL, or third-party GNU tools, **or**
- a need to provide PowerShell-native equivalents.

This is tracked as a concern in `CONCERNS.md`.