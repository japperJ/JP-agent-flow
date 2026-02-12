# Mode Invocation & Delegation Flow (Current)

This documents how modes are currently *triggered* and *communicated* across agents, using `.github/agents/*` as the source of truth.

## How modes are currently invoked

### Primary mechanism: natural-language “<Mode> mode” in delegation prompts

The Orchestrator uses delegation prompts like:
- “Project mode. Research…” → Researcher
- “Roadmap mode. Using the research…” → Planner
- “Phase mode. Verify…” → Verifier

This is visible throughout `.github/agents/orchestrator.agent.md` in the “10-Step Execution Model” sections.

### Secondary mechanism: inference from context (Researcher)

The Researcher explicitly allows inference:
> “The orchestrator or user specifies which mode, or you infer from context.” (`.github/agents/researcher.agent.md`, `## Modes`)

Implication: if the Orchestrator prompt is vague (“research this”), the Researcher may still choose a mode based on trigger heuristics.

### Implicit mode switching: file presence (Verifier)

Verifier’s “Phase Verification” has a built-in switch:
- If `VERIFICATION.md` already exists, it treats the run as a re-verification (“Step 0”).

This can override or complement whatever the caller said.

### Debugger mode selection

Debugger defines:
- `find_and_fix` (default)
- `find_root_cause_only`

The Orchestrator does **not** currently reference these mode names when routing bugs (“Bug report → runSubagent(Debugger) directly”).

## Delegation flow (what gets delegated to whom)

### Orchestrator’s canonical lifecycle

Declared lifecycle: **Research → Plan → Execute → Verify → Debug → Iterate**.

The Orchestrator doc defines a full 10-step flow, including:
- Researcher (`project` → `synthesize`)
- Planner (`roadmap` → `plan` → `validate` → optional `revise`)
- Coder/Designer (execute)
- Verifier (`phase` → optional gap-closure loop → `integration`)

### Gap-closure loop (delegation loop)

Orchestrator defines a loop:
1) Planner “gaps mode”
2) Coder executes fix plans
3) Verifier re-verifies

This is a strong delegation pattern and the best “closed loop” in the system.

## Output handoffs (“who consumes whose output”)

| Producer | Artifact | Expected consumer(s) | Evidence |
|---|---|---|---|
| Researcher | `.planning/research/*` | Planner (roadmap), Planner (plan) | Orchestrator Step 3 prompt tells Planner to use `.planning/research/SUMMARY.md` (or research in `.planning/research/`). |
| Planner | `.planning/ROADMAP.md`, `REQUIREMENTS.md`, `STATE.md` | Researcher (phase), Coder (execute), Verifier (phase/integration) | Orchestrator Step 4+ references `.planning/ROADMAP.md`; Verifier “Load Context” requires ROADMAP/REQUIREMENTS/STATE. |
| Planner | `.planning/phases/<phase>/PLAN.md` | Coder/Designer, Verifier | Orchestrator Step 7 tells Coder to “Execute PLAN.md”; Verifier extracts `must_haves` from plan frontmatter. |
| Coder | `.planning/phases/<phase>/SUMMARY.md` | Verifier, Orchestrator, user report-out | Verifier: “Do NOT trust SUMMARY.md claims” but does read it for context; Orchestrator Step 10 uses phase summaries for reporting. |
| Verifier | `.planning/phases/<phase>/VERIFICATION.md` | Planner (gaps), Orchestrator | Orchestrator gap-closure loop starts from VERIFICATION.md. |
| Debugger | `.planning/debug/BUG-…` | User + future debugging sessions | Debugger spec: mandatory persistent debug file. |

## “Mode enforcement” intent already exists in-repo

There is an existing meta-planning effort under `.planning/mode-enforcement/`:
- `PLAN-1-orchestrator-researcher.md`
- `PLAN-2-planner-verifier.md`

These plans explicitly target a key current behavior: Orchestrator prescribing output file names/paths for mode-driven agents, and adding “mode precedence” rules to mode-driven agents.

Interpretation: the repo already recognizes “mode enforcement” as an improvement area; it appears not yet applied to the agent specs (the Orchestrator still contains “Wait for: …” lists).
