# Codebase Architecture

## Purpose & functionality
This repository packages a reusable **agent team** for GitHub Copilot Chat in VS Code. Its core functionality is:

- Provide **ready-to-install agent definitions** (`*.agent.md`) for Orchestrator/Researcher/Planner/Coder/Designer/Verifier/Debugger.
- Define a **repeatable, phase-based workflow** for software projects using `.planning/` artifacts as the shared interface.
- Provide **distribution guidance** (GitHub Gist publishing and install-link format) so others can install the agents into VS Code.

## What this project is
JP-agent-flow is a **multi-agent development system** implemented as a set of **Copilot custom agent definitions** (`*.agent.md`). The “architecture” is therefore:

1. **Agent roles and tool permissions** (declared in YAML frontmatter)
2. **A prescribed lifecycle workflow** (Research → Plan → Execute → Verify → Debug → Iterate)
3. **A planning artifact filesystem contract** under `.planning/`

There is no traditional executable application code; the repo is a configuration/documentation “control plane” for agent collaboration.

## Major subsystems

### 1) Agent layer (definition files)
The system defines **7 specialized agents**, each with a clear responsibility boundary.

| Agent | Primary purpose | Key capability boundary | Evidence |
|---|---|---|---|
| `Orchestrator` | Delegates and coordinates across phases | **Cannot implement directly**; delegates via `runSubagent` | `Agents/orchestrator.agent.md` frontmatter/tools + body rules |
| `Researcher` | Research + codebase mapping | “Research only”; Context7-first; writes `.planning/*` | `Agents/researcher.agent.md` |
| `Planner` | Roadmaps + plans + plan validation | Produces `ROADMAP.md`, `REQUIREMENTS.md`, `STATE.md`, `PLAN.md` | `Agents/planner.agent.md` |
| `Coder` | Implementation agent | Executes plans; commits per task; Context7-first | `Agents/coder.agent.md` |
| `Designer` | UI/UX design | Prioritizes usability/accessibility/aesthetics | `Agents/designer.agent.md` |
| `Verifier` | Goal-backward verification | Verifies wiring and “observable truths”; writes `VERIFICATION.md` | `Agents/verifier.agent.md` |
| `Debugger` | Scientific debugging | Hypothesis testing + persistent `.planning/debug/*` logs | `Agents/debugger.agent.md` |

### 2) Workflow layer (lifecycle orchestration)
The Orchestrator defines a **10-step execution model**:

1. Researcher: project research → `.planning/research/*`
2. Researcher: synthesize → `.planning/research/SUMMARY.md`
3. Planner: roadmap → `.planning/ROADMAP.md`, `.planning/REQUIREMENTS.md`, `.planning/STATE.md`
4–8. Per-phase loop: Research → Plan → Validate → Execute (Coder/Designer) → Verify (Verifier)
9. Verifier: integration verification → `.planning/INTEGRATION.md`
10. Orchestrator: report to user

Evidence: `Agents/orchestrator.agent.md`.

### 3) Artifact layer (`.planning/` contract)
Agents communicate and coordinate through **files**, not hidden state.

- Research outputs: `.planning/research/*`
- Phase work: `.planning/phases/<n>/*`
- Verification reports: `.planning/phases/<n>/VERIFICATION.md` + `.planning/INTEGRATION.md`
- Debug logs: `.planning/debug/*`

Evidence: described across multiple agent files and summarized in `AGENTS_GIST.md`.

## Key architectural patterns

### Separation of duties via tool permissions
The most important “architecture” control is **tool scoping**:
- Orchestrator tools are limited (`read/readFile`, `agent`, `memory`) to force delegation.
- Implementers (Coder/Designer) include `edit` + `execute`.
- Research/plan agents include `context7/*` and `web` for freshness.

### File-overlap parallelism
The Orchestrator promotes parallel execution only when **tasks do not overlap files**, otherwise it forces sequential work.

Evidence: “Parallelization Rules” and “File Conflict Prevention” sections in `Agents/orchestrator.agent.md`.

### Goal-backward planning and verification
- Planner derives **must-haves** from phase success criteria.
- Verifier checks “observable truths”, “artifacts”, and “key links” and can emit structured YAML gaps.

Evidence: `Agents/planner.agent.md` + `Agents/verifier.agent.md`.

## Two agent-definition locations
This repo contains agents in both:
- `Agents/` (repo-visible, used by publishing docs)
- `.github/agents/` (VS Code’s typical per-repo agent location)

The contents appear duplicated.

Evidence: directory listings show the same 7 filenames in both folders.

## Key components (files) and their roles

| File | Role |
|---|---|
| `AGENTS_GIST.md` | Primary end-user documentation intended to be published as a Gist; contains install badges/links and detailed agent breakdown. |
| `GIST_PUBLISHING_GUIDE.md` | Step-by-step workflow for creating/editing the multi-file gist and updating the gist ID placeholders. |
| `Agents/*.agent.md` | The agent definitions (YAML frontmatter + instructions). |
| `.github/agents/*.agent.md` | Duplicate copy of agent definitions in the conventional per-repo agent location for VS Code. |
| `Agents/README.md` and `.github/agents/README.md` | Notes about orchestration naming and general usage; emphasizes capitalization for agent names. |
| `.planning/research/VSCODE_INSTALL_FORMAT.md` | Documents the deep-link + `aka.ms` wrapper format and the observed `raw.githubusercontent.com` redirect rejection. |
| `.planning/research/AGENTS_DOCUMENTATION.md` | Prior internal inventory of agent files and gist structure recommendations. |

## Documentation inventory

- **Install/publishing docs:** `AGENTS_GIST.md`, `GIST_PUBLISHING_GUIDE.md`
- **Agent usage notes:** `Agents/README.md` (+ duplicate under `.github/agents/README.md`)
- **Research notes about agents:** `.planning/research/AGENTS_DOCUMENTATION.md`
- **Install-link format reference:** `.planning/research/VSCODE_INSTALL_FORMAT.md`
