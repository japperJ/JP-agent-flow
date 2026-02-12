# Project Structure

## Top-level

```
JP agent flow/
├─ AGENTS_GIST.md
├─ GIST_PUBLISHING_GUIDE.md
├─ Agents/
│  ├─ README.md
│  ├─ orchestrator.agent.md
│  ├─ researcher.agent.md
│  ├─ planner.agent.md
│  ├─ coder.agent.md
│  ├─ designer.agent.md
│  ├─ verifier.agent.md
│  └─ debugger.agent.md
├─ .github/
│  └─ agents/
│     ├─ README.md
│     ├─ orchestrator.agent.md
│     ├─ researcher.agent.md
│     ├─ planner.agent.md
│     ├─ coder.agent.md
│     ├─ designer.agent.md
│     ├─ verifier.agent.md
│     └─ debugger.agent.md
├─ .planning/
│  ├─ research/
│  │  ├─ AGENTS_DOCUMENTATION.md
│  │  └─ VSCODE_INSTALL_FORMAT.md
│  └─ codebase/
│     ├─ STACK.md
│     ├─ ARCHITECTURE.md
│     ├─ STRUCTURE.md
│     ├─ CONVENTIONS.md
│     └─ CONCERNS.md
└─ .gitignore
```

## Directory purposes

### `Agents/`
Canonical, repo-visible copy of the 7 agent definition files and a small README. This is the set referenced by publishing instructions and the gist workflow.

### `.github/agents/`
A second copy of the agent files in the location commonly used by VS Code for repository-scoped agents.

### `.planning/`
Planning artifact workspace used by the agents during real projects. In this repository it is used for:
- `research/`: meta-docs about agent publishing and install-link format.
- `codebase/`: (this output) codebase mapping docs.

### Docs at repo root
- `AGENTS_GIST.md`: the user-facing “landing page” style documentation intended to be published as a GitHub Gist with install badges.
- `GIST_PUBLISHING_GUIDE.md`: step-by-step instructions for creating/editing a multi-file gist and updating the gist ID placeholders.

## Notable file: `.gitignore`
Currently ignores the entire `.github/` directory.

This is important because it can prevent `.github/agents/*` from being committed/published with the repository.
