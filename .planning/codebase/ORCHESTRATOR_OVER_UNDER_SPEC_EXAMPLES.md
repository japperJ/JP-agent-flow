# Orchestrator Over-Specification vs Under-Specification (Examples)

Examples are sourced from `.github/agents/orchestrator.agent.md` and interpreted through the mode contracts of other agents.

## Over-specification patterns

### 1) Prescribing outputs for mode-driven agents

**Pattern:** Orchestrator includes explicit artifact expectations for Researcher/Planner/Verifier steps.

**Example (Project research + synthesize + roadmap):**
- “Write all output to `.planning/research/`.”
- “Wait for: `.planning/research/STACK.md`, …”
- “Write `ROADMAP.md`, `REQUIREMENTS.md`, and `STATE.md`…”

**Why it’s ‘over’:** these agents already define their output contracts; the Orchestrator is duplicating (and potentially conflicting with) those contracts.

**Related repo intent:** `.planning/mode-enforcement/PLAN-1-orchestrator-researcher.md` is explicitly trying to remove this.

### 2) Controlling how execution is organized (beyond coordination)

**Pattern:** Orchestrator instructs internal execution mechanics that belong to the executing agent.

**Example:** In Step 7, it includes:
- “Parse the PLAN.md for task assignments. Determine parallelization using file overlap rules…”

**Why it’s ‘over’:** Coder/Designer can own the execution mechanics; Orchestrator can constrain scope and dependencies without narrating execution strategy.

### 3) Scoping examples that become ‘mini-plans’

**Pattern:** “File Conflict Prevention” examples provide detailed file creation/modification instructions.

**Example:**
- “Implement the theme context. Create `src/contexts/ThemeContext.tsx` and `src/hooks/useTheme.ts`. Do NOT touch any other files.”

**Why it’s borderline:** This is useful for avoiding conflicts, but it also starts to look like the Orchestrator is writing micro-plans (naming files, deciding structure). It’s a valid *coordination tool*, but should be used sparingly and ideally sourced from Planner plans.

## Under-specification patterns

### 1) “Quick code change” routing lacks acceptance criteria

**Pattern:** Orchestrator says:
- “Quick code change (single file, obvious) → runSubagent(Coder) directly”

**What’s missing:**
- concrete acceptance criteria
- constraints (tests to run, behavior to preserve)
- file-scope boundaries (even a quick fix can spill into multiple files)

### 2) Bug routing doesn’t specify Debugger mode / desired outcome

**Pattern:**
- “Bug report → runSubagent(Debugger) directly”

**What’s missing:**
- whether to fix or only identify root cause
- required reproduction info
- desired output: debug file + summary

Given Debugger defaults to `find_and_fix`, this can lead to unintended code edits.

### 3) “Verify existing work” routing lacks verification scope

**Pattern:**
- “Verify existing work → runSubagent(Verifier) directly”

**What’s missing:**
- what “done” means (phase? integration? a specific user story?)
- where success criteria live (ROADMAP? issue description? tests?)

Without these, the Verifier must infer scope, which can create partial or misaligned verification.

## Practical implication

These over/under patterns are two sides of the same coin:
- when Orchestrator has a *strong mental model*, it tends to over-prescribe artifacts and structure
- when it has a *weak/ambiguous model*, it delegates too vaguely

A stronger mode handshake + standardized delegation prompt pattern (mode + objective + inputs + constraints) would reduce both failure modes.
