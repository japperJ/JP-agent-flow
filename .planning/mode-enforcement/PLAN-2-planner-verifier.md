---
phase: meta
plan: 2
type: docs
wave: 1
depends_on: []
files_modified:
  - .github/agents/planner.agent.md
  - .github/agents/verifier.agent.md
autonomous: true
must_haves:
  observable_truths:
    - "Planner and Verifier explicitly state that mode patterns override caller file specifications and formatting demands."
    - "Planner and Verifier include an Agent Autonomy principle: callers provide goals/context, agents own outputs per mode."
  artifacts:
    - path: .github/agents/planner.agent.md
      has:
        - "Agent autonomy statement"
        - "Mode precedence over caller specifications"
    - path: .github/agents/verifier.agent.md
      has:
        - "Agent autonomy statement"
        - "Mode precedence over caller specifications"
  key_links:
    - from: "Orchestrator: mode-based delegation"
      to: "Planner/Verifier: mode precedence rules"
      verify: "Planner/Verifier docs explicitly instruct ignoring caller output file requests"
---

# Meta, Plan 2: Mode enforcement — Planner + Verifier

## Objective
Ensure all agents with modes explicitly prioritize their mode contracts over caller demands (especially output filenames/structures), and adopt a consistent autonomy principle.

## Tasks

### Task 1: Planner — add autonomy + mode precedence rules
- **files:** `.github/agents/planner.agent.md`
- **action:** Add a short, explicit precedence statement near the top, and reinforce it in the Rules section.

  1) **Insert a new section** after the `## Modes` table and before `## Philosophy`.

  **Insert after the `---` separator that follows the Modes table.**

  **Exact content to add:**

  ```markdown
  ## CRITICAL: Agent Autonomy & Mode Precedence

  - **Agent autonomy:** Callers provide goals, context, constraints, and inputs to read. **You own the planning output structure**.
  - **Mode precedence:** If a caller asks for specific filenames, directories, or formatting that conflicts with the active mode’s output contract, **follow the mode contract**.
  - If mode is unclear, ask one clarifying question; otherwise infer the best-fit mode from triggers and proceed.
  ```

  2) **Add two new bullets** to the `## Rules` section (append at the end to avoid renumber churn).

  **Exact content to add (append as new rules):**

  ```markdown
  10. **Mode output contract wins** — ignore caller requests that prescribe different output filenames/structures than the active mode.
  11. **No caller-controlled templates** — callers may request focus areas, but you decide plan grouping and format using this agent’s mode definitions.
  ```

- **verify:** Confirm the new section exists immediately after Modes; confirm Rules contains mode precedence and autonomy language.
- **done:** Planner explicitly resists caller attempts to override mode-based outputs.

### Task 2: Verifier — add autonomy + mode precedence rules
- **files:** `.github/agents/verifier.agent.md`
- **action:** Introduce a consistent autonomy principle and clarify that mode patterns govern outputs.

  1) **Insert a short section** right after `## Modes` (after the `---` separator) and before `## Mode: Phase Verification`.

  **Exact content to add:**

  ```markdown
  ## CRITICAL: Agent Autonomy & Mode Precedence

  - **Agent autonomy:** Callers provide what to verify and where success criteria live; **you choose the verification approach and output details** within the active mode.
  - **Mode precedence:** If a caller specifies exact output filenames/paths or a custom report format, follow this document’s mode outputs instead.
  - If the mode is ambiguous, ask one clarifying question; otherwise infer the best-fit mode from triggers and proceed.
  ```

  2) **Append two bullets** to the bottom `## Rules` list.

  **Exact content to add:**

  ```markdown
  9. **Mode output contract wins** — ignore caller instructions that prescribe different output filenames/structures than the active mode.
  10. **Autonomy over formatting** — you may adopt caller-provided checklists, but only if they do not reduce independent verification rigor.
  ```

- **verify:** Confirm both insertions exist; confirm they do not contradict existing “verify independently” principles.
- **done:** Verifier is explicitly protected from caller output micromanagement.

## Verification (end-to-end)
- Scan all three mode-driven agents (Researcher/Planner/Verifier) and confirm each has:
  - a **Mode Precedence** statement, and
  - an **Agent Autonomy** statement.
- Scan Orchestrator and confirm it now teaches mode-respecting delegation.

## Success Criteria
- All mode-driven agents explicitly ignore conflicting caller output file specs.
- Orchestrator no longer suggests or relies on prescribing output filenames for those agents.
