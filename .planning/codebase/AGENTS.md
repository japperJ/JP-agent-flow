# Agent System Design

This file documents the **7-agent** system defined in `.github/agents/` (with duplicates under `Agents/`).

## Agent inventory

| Agent | Definition file | Primary role | Tools boundary (from frontmatter) |
|---|---|---|---|
| Orchestrator | `.github/agents/orchestrator.agent.md` | Coordinator; delegates everything; never implements | `read/readFile`, `agent` (runSubagent), `memory` |
| Researcher | `.github/agents/researcher.agent.md` | Research + codebase mapping + source verification | `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory` |
| Planner | `.github/agents/planner.agent.md` | Roadmaps + phase plans + plan validation + gap plans | `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`, `todo` |
| Coder | `.github/agents/coder.agent.md` | Implements plans; commits per task; updates state | `vscode`, `execute`, `read`, `context7/*`, `github/*`, `edit`, `search`, `web`, `memory`, `todo` |
| Designer | `.github/agents/designer.agent.md` | UI/UX implementation; accessibility + usability | `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`, `todo` |
| Verifier | `.github/agents/verifier.agent.md` | Goal-backward verification; finds wiring gaps | `vscode`, `execute`, `read`, `edit`, `search`, `memory` |
| Debugger | `.github/agents/debugger.agent.md` | Scientific debugging; hypothesis testing; persistent logs | `vscode`, `execute`, `read`, `edit`, `search`, `web`, `memory`, `context7/*` |

## Modes and outputs (by agent contract)

- **Researcher**
  - `project` → `.planning/research/` (summary + stack/features/arch/pitfalls; note ambiguity discussed in `CONCERNS.md`)
  - `phase` → `.planning/phases/<phase>/RESEARCH.md`
  - `codebase` → `.planning/codebase/` (stack/structure/etc)
  - `synthesize` → `.planning/research/SUMMARY.md`

- **Planner**
  - `roadmap` → `.planning/ROADMAP.md`, `.planning/STATE.md`, `.planning/REQUIREMENTS.md`
  - `plan` → `.planning/phases/<phase>/PLAN.md` (and possibly multiple plan files)
  - `validate` → pass/fail + structured issues (returned text)
  - `gaps` → additional minimal `PLAN.md` files for gap closure
  - `revise` → updated plan(s)

- **Verifier**
  - `phase` → `.planning/phases/<phase>/VERIFICATION.md`
  - `integration` → `.planning/INTEGRATION.md`
  - `re-verify` → updated `.planning/phases/<phase>/VERIFICATION.md`

- **Debugger**
  - `find_and_fix` (default) → `.planning/debug/BUG-[timestamp].md` plus fixes
  - `find_root_cause_only` → `.planning/debug/BUG-[timestamp].md` plus diagnosis only

## Coordination protocol (how agents work together)

1. **Delegation** happens through Orchestrator calling `runSubagent(<AgentName>, <prompt>)`.
2. **State** is stored in `.planning/STATE.md` and per-phase artifacts.
3. **Quality gates** happen through Verifier; gaps are written in structured YAML frontmatter.
4. **Iteration**: gap-closure loop is codified as Planner (gaps) → Coder → Verifier.

## Configuration and naming requirements

- Agent names must match frontmatter `name:` exactly (capitalization matters). This is called out explicitly in `.github/agents/README.md`.
- Delegated prompts should use **relative paths** (e.g., `.planning/ROADMAP.md`), not absolute file paths.

## Notable design decisions

- Capability segregation: Orchestrator lacks `edit` and `execute` tools.
- File-based contracts: avoids hidden state and makes work auditable.
- “Task completion ≠ goal achievement”: Verifier’s core principle.
- “Plans are prompts”: Planner’s core principle (WHAT not HOW).