# Project Structure (JP agent flow)

This repository is a **VS Code Copilot Custom Agents** configuration pack: a set of `*.agent.md` definition files plus documentation for installing/publishing them (primarily via GitHub Gist raw URLs) and for running a multi-agent workflow that writes planning artifacts into `.planning/`.

## Top-level layout

```
.
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
│  ├─ debugger.agent.md
│  └─ orchestrator.agent.md.backup
├─ .github/
│  └─ agents/
│     ├─ README.md
│     ├─ orchestrator.agent.md
│     ├─ researcher.agent.md
│     ├─ planner.agent.md
│     ├─ coder.agent.md
│     ├─ designer.agent.md
│     ├─ verifier.agent.md
│     ├─ debugger.agent.md
│     └─ Backup-orchestrator.agent.md.backup
└─ .planning/
   ├─ research/
   │  ├─ AGENTS_DOCUMENTATION.md
   │  └─ VSCODE_INSTALL_FORMAT.md
   ├─ mode-enforcement/
   │  ├─ PLAN-1-orchestrator-researcher.md
   │  └─ PLAN-2-planner-verifier.md
   └─ codebase/
      ├─ (this file)
      ├─ AGENT_MODES_MATRIX.md
      ├─ MODE_INVOCATION_AND_DELEGATION.md
      ├─ ORCHESTRATOR_OVER_UNDER_SPEC_EXAMPLES.md
      ├─ GAPS_AND_MODE_VIOLATIONS.md
      └─ RECOMMENDATIONS_AGENT_AUTONOMY.md
```

## What is “canonical”?

- **Runtime agent directory (VS Code):** `.github/agents/` is the conventional location for Copilot agent definitions in a repo/workspace.
- **Publishing directory (Gist):** `Agents/` is used by `GIST_PUBLISHING_GUIDE.md` to publish agent files to a multi-file Gist.

The repository currently contains *two parallel copies* of the agent definitions (`Agents/` and `.github/agents/`). This is convenient for Gist publishing, but it is a drift risk unless you treat one as the source of truth and keep the other synchronized.

## What lives in `.planning/`?

`.planning/` is used as the **shared artifact bus** for the workflow.

- `research/` — “how to use/publish agents” research notes for this repo.
- `mode-enforcement/` — meta-plans proposing improvements to agent autonomy and mode enforcement.
- `codebase/` — this analysis plus other analysis documents.

In real projects (where these agents are used), additional `.planning/` artifacts are expected to be created (e.g., `ROADMAP.md`, `REQUIREMENTS.md`, per-phase `PLAN.md`, `VERIFICATION.md`, etc.).