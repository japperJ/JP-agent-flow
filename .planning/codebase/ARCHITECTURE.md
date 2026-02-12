# Codebase Architecture

This project is an **agent workflow system**: a set of Copilot agent specifications plus a file-based workflow (the `.planning/` directory) that agents use to coordinate across research → planning → implementation → verification → debugging.

## Pattern: Orchestrated, artifact-driven multi-agent workflow

### Key idea
- The **Orchestrator** never edits code directly. It delegates work to specialist agents via `runSubagent(...)`.
- Specialist agents produce/consume **shared artifacts** under `.planning/` to keep the workflow traceable and resumable.

### Primary control loop (as defined in `orchestrator.agent.md`)
1. **Research**: Researcher (`project` mode) produces research artifacts.
2. **Synthesize**: Researcher (`synthesize` mode) consolidates research into a summary.
3. **Roadmap**: Planner (`roadmap` mode) produces `ROADMAP.md`, `REQUIREMENTS.md`, `STATE.md`.
4. Per-phase loop:
   - Researcher (`phase` mode) produces per-phase research.
   - Planner (`plan` mode) produces per-phase executable plan(s).
   - Planner (`validate` mode) validates plans.
   - Coder/Designer execute tasks (potentially in parallel with file-scope boundaries).
   - Verifier verifies outcomes (`phase` mode) and may generate structured gaps.
   - Gap-closure loop: Planner (`gaps`) → Coder → Verifier (`re-verify`).
5. **Integration**: Verifier (`integration`) checks cross-phase wiring.
6. **Report**: Orchestrator summarizes what happened.

## Components and their responsibilities

### 1) Agent definition files (the “runtime configuration”)
Located in `.github/agents/*.agent.md` (and duplicated under `Agents/`). Each file defines:
- `name` (invocation key)
- `tools` (capability boundary)
- instructions: roles, modes, workflows, output contracts

### 2) Artifact bus (`.planning/`)
`.planning/` is the shared filesystem contract. Agents rely on **file presence and conventions** rather than in-memory state:
- Planner creates top-level roadmap + requirements + state.
- Plans contain frontmatter `must_haves` used by Verifier.
- Verifier writes gaps in YAML frontmatter consumed by Planner (gaps mode).
- Debugger uses append-only debug logs in `.planning/debug/`.

This is effectively a lightweight, file-based “workflow engine”.

### 3) Mode-driven behaviors
Several agents have explicit “modes” that act like sub-protocols:
- Researcher: `project`, `phase`, `codebase`, `synthesize`
- Planner: `roadmap`, `plan`, `validate`, `gaps`, `revise`
- Verifier: `phase`, `integration`, `re-verify`
- Debugger: `find_and_fix`, `find_root_cause_only`

Mode selection is currently driven by **natural language prompts** (e.g., “Project mode. …”) and (for Verifier) by **file presence** (existing `VERIFICATION.md`).

## Key relationships (who depends on what)

| Producer | Produces | Consumer(s) | Coupling type |
|---|---|---|---|
| Researcher | `.planning/research/*` | Planner (roadmap/plan) | loose: file-based |
| Planner | `.planning/ROADMAP.md`, `.planning/REQUIREMENTS.md`, `.planning/STATE.md` | Researcher (phase), Coder, Verifier | medium: file-based |
| Planner | `.planning/phases/N/PLAN.md` | Coder/Designer, Verifier | tight: plan contract |
| Coder | code + `.planning/phases/N/SUMMARY.md` + `STATE.md` updates | Orchestrator, Verifier | medium |
| Verifier | `.planning/phases/N/VERIFICATION.md`, `.planning/INTEGRATION.md` | Planner (gaps), Orchestrator | tight: YAML gap schema |
| Debugger | `.planning/debug/BUG-*.md` | user + future debug sessions | loose |

## Architectural strengths
- **Clear capability boundaries** via `tools:` in frontmatter (e.g., Orchestrator cannot edit).
- **Traceability**: artifacts persist, enabling resumption and audit.
- **Closed-loop quality control**: verification + gap-closure loop.

## Architectural risks (high level)
- Duplicate agent directories (`Agents/` vs `.github/agents/`) can drift.
- Verification examples are bash-centric; Windows users may not be able to reproduce commands.
- Mode enforcement is informal; several meta-plans exist to strengthen it.