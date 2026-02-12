# Agent Modes Matrix (Current)

This inventory is based on the agent specifications in `.github/agents/`.

## Quick map

| Agent | Modes defined? | Mode names | How mode is selected (per agent spec) | Primary outputs (per mode contract) |
|---|---:|---|---|---|
| **Orchestrator** (`.github/agents/orchestrator.agent.md`) | No | — | N/A (routes requests via “Request Routing” table + “10-Step Execution Model”) | *No explicit artifacts owned.* Coordinates other agents; provides delegation prompts; tells user what to review. |
| **Researcher** (`.github/agents/researcher.agent.md`) | Yes | `project`, `phase`, `codebase`, `synthesize` | “The orchestrator or user specifies… or you infer from context.” | **project:** `.planning/research/` → `SUMMARY.md`, `STACK.md`, `FEATURES.md`, `ARCHITECTURE.md`, `PITFALLS.md`  
**phase:** `.planning/phases/<phase>/RESEARCH.md`  
**codebase:** `.planning/codebase/` docs (varies by focus)  
**synthesize:** `.planning/research/SUMMARY.md` (consolidated) |
| **Planner** (`.github/agents/planner.agent.md`) | Yes | `roadmap`, `plan`, `validate`, `gaps`, `revise` | Selected by caller prompt (“Roadmap mode…”, etc.) or inferred by trigger table. | **roadmap:** `.planning/ROADMAP.md`, `.planning/STATE.md`, `.planning/REQUIREMENTS.md`  
**plan:** `.planning/phases/<phase>/PLAN.md` (and/or multiple `PLAN.md` files per task group)  
**validate:** pass/fail with structured issues (YAML-like in response)  
**gaps:** gap-closure `PLAN.md` files in `.planning/phases/<phase>/`  
**revise:** updated `PLAN.md` files |
| **Verifier** (`.github/agents/verifier.agent.md`) | Yes | `phase`, `integration`, `re-verify` | Selected by caller prompt (“Phase mode…”, “Integration mode…”) and by detecting existing `VERIFICATION.md` (“Step 0: Check for Previous Verification”). | **phase:** `.planning/phases/<phase>/VERIFICATION.md`  
**integration:** `.planning/INTEGRATION.md`  
**re-verify:** updated `.planning/phases/<phase>/VERIFICATION.md` |
| **Debugger** (`.github/agents/debugger.agent.md`) | Yes | `find_and_fix` (default), `find_root_cause_only` | Default is `find_and_fix` unless caller specifies otherwise. | Debug session file: `.planning/debug/BUG-[timestamp].md` (mandatory). Also structured “ROOT CAUSE FOUND” / “DEBUG COMPLETE” returns. |
| **Coder** (`.github/agents/coder.agent.md`) | No (explicitly) | — | N/A | Produces code changes + per-task commits; writes `.planning/phases/<phase>/SUMMARY.md` and updates `.planning/STATE.md` when executing plans. |
| **Designer** (`.github/agents/designer.agent.md`) | No | — | N/A | Produces UI/UX code changes; no `.planning/` artifact contract defined. |

## Notes on contract clarity

- The strongest, most explicit “mode → output” contracts are in **Researcher**, **Planner**, and **Verifier**.
- **Debugger** has a smaller mode set, but a very explicit artifact protocol (`.planning/debug/…`).
- **Orchestrator** is not mode-driven; it is flow-driven.
