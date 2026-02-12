---
phase: meta
plan: 1
type: docs
wave: 1
depends_on: []
files_modified:
  - .github/agents/orchestrator.agent.md
  - .github/agents/researcher.agent.md
autonomous: true
must_haves:
  observable_truths:
    - "Orchestrator delegations no longer prescribe output file names/paths for mode-driven agents (Researcher/Planner/Verifier)."
    - "Researcher enforces mode detection at run start and explicitly ignores caller file-spec instructions that conflict with mode patterns."
  artifacts:
    - path: .github/agents/orchestrator.agent.md
      has:
        - "Mode reference table (agents → modes → output patterns)"
        - "Minimal delegation examples that specify only mode + context"
        - "Rule: let agents handle their own output structure per mode"
        - "Updated existing delegation templates to remove output file prescriptions"
    - path: .github/agents/researcher.agent.md
      has:
        - "Mode detection/enforcement section near top"
        - "Explicit precedence statement: mode > caller instructions"
        - "Rule: ignore file specifications from caller"
  key_links:
    - from: "Orchestrator: Full Flow prompts"
      to: "Researcher: mode output table + enforcement rules"
      verify: "Orchestrator prompt text references mode + objective, and Researcher doc states it will follow its mode output pattern regardless of caller file specs"
---

# Meta, Plan 1: Mode enforcement — Orchestrator + Researcher

## Objective
Stop mode-driven agents from being “output-commandeered” by Orchestrator. Orchestrator should delegate with *mode + context + objective* (no output filenames), and Researcher should treat its mode patterns as authoritative even when a caller specifies output files.

## Tasks

### Task 1: Orchestrator — add mode reference + delegation rules, and remove output prescriptions
- **files:** `.github/agents/orchestrator.agent.md`
- **action:**
  1) **Insert a mode reference table** right after the existing agent capability table under `## CRITICAL: Agent Invocation`.

  **Insert after the table that starts with** `| Agent | Name | Has Edit Tools | Role |` **and before** `### Path References in Delegation`.

  **Exact content to add:**

  ```markdown
  ### Agent Modes & Output Patterns (Reference)

  Use this table to avoid overriding an agent’s mode contract. If you specify mode, the agent owns output structure.

  | Agent | Modes (if any) | Output pattern (owned by agent) | Orchestrator delegation should include | Must NOT include |
  |---|---|---|---|---|
  | Researcher | `project`, `phase`, `codebase`, `synthesize` | Writes to `.planning/` using its mode templates | Mode + scope + constraints + where to find inputs | Specific output filenames/paths; “Wait for: X.md” lists |
  | Planner | `roadmap`, `plan`, `validate`, `gaps`, `revise` | Writes to `.planning/` using its mode templates | Mode + goal + inputs to read + any constraints | Prescribing PLAN file names/locations; dictating plan structure |
  | Verifier | `phase`, `integration`, `re-verify` | Writes verification artifacts to `.planning/` using its mode templates | Mode + what to verify + success criteria source | Dictating verification template/output file names |
  | Coder | (no modes defined) | Produces code changes; may write summaries if their agent spec says so | Goal + acceptance criteria + file scope when needed | Implementation steps unless necessary; overly rigid approach |
  | Designer | (no modes defined) | Produces UI/UX changes | Goal + UX constraints + file scope when needed | Implementation steps; design-by-microinstruction |
  | Debugger | (no modes defined) | Produces diagnosis + fixes via its workflow | Symptoms + repro steps + expected behavior | Prescribing root cause before evidence |
  ```

  2) **Add a “mode enforcement” rule + minimal delegation examples** near the end of the Orchestrator doc, immediately before the existing `## CRITICAL: Never Tell Agents HOW` section.

  **Insert before the heading** `## CRITICAL: Never Tell Agents HOW`.

  **Exact content to add:**

  ```markdown
  ## CRITICAL: Mode Enforcement (Do Not Override)

  **Rule:** If an agent has modes, you may specify the mode and provide context — **but you must let the agent handle its own output structure per mode**.

  - ✅ Do: provide **mode + objective + inputs to read + constraints**
  - ❌ Don’t: specify output filenames/paths, or list “Wait for: …” artifacts for a mode-driven agent

  ### Minimal delegation examples (mode + context only)

  **Researcher (project mode)**
  - prompt: "Project mode. Research the domain + tech options for: **[request]**. Consider constraints: **[constraints]**. Use your standard project-mode outputs."

  **Planner (roadmap mode)**
  - prompt: "Roadmap mode. Using any existing research in `.planning/research/`, produce a phased roadmap for: **[request]**. Use your standard roadmap outputs."

  **Verifier (phase mode)**
  - prompt: "Phase mode. Verify Phase **[N]** against success criteria in `.planning/ROADMAP.md` and any phase plans/summaries. Use your standard phase verification output."
  ```

  3) **Update existing delegation templates** in Orchestrator so they no longer prescribe file outputs for mode-driven agents.

  Apply the following replacements (keep the step structure, but remove explicit “write X file”/“wait for X file” directives):

  - In **Step 1: Project Research** replace the `prompt:` value with:

    ```text
    Project mode. Research the domain, technology options, architecture patterns, and pitfalls for: **[user's request]**. Use your standard project-mode outputs.
    ```

    And **delete** the `Wait for:` line that lists specific filenames.

  - In **Step 2: Synthesize Research** replace the `prompt:` value with:

    ```text
    Synthesize mode. Read existing research under `.planning/research/` and produce your standard consolidated summary output.
    ```

    And **delete** the `Wait for:` line that names `.planning/research/SUMMARY.md`.

  - In **Step 3: Create Roadmap** replace the `prompt:` value with:

    ```text
    Roadmap mode. Using the research summary (if present) under `.planning/research/`, create a phased roadmap for: **[user's request]**. Use your standard roadmap outputs.
    ```

    And **delete** the `Wait for:` line that lists roadmap filenames.

  - In **Step 4: Phase Research** replace the `prompt:` value with:

    ```text
    Phase mode. Research implementation details for Phase [N]: '[phase name]'. Read `.planning/ROADMAP.md` for phase goals and `.planning/research/` for stack decisions. Use your standard phase research output.
    ```

    And **delete** the `Wait for:` line that lists `.planning/phases/[N]/RESEARCH.md`.

  - In **Step 5: Create Phase Plan** replace the `prompt:` value with:

    ```text
    Plan mode. Create task-level plans for Phase [N]. Read phase research and roadmap success criteria. Use your standard plan outputs.
    ```

    And **delete** the `Wait for:` line that lists `.planning/phases/[N]/PLAN.md`.

  - In **Step 8: Verify Phase** replace the `prompt:` value with:

    ```text
    Phase mode. Verify Phase [N] against success criteria in `.planning/ROADMAP.md` and evidence in the repo. Use your standard phase verification output.
    ```

    And **delete** the `Wait for:` line that names `.planning/phases/[N]/VERIFICATION.md`.

  - In **Gap-Closure Loop → Planner (gaps mode)** replace the `prompt:` value with:

    ```text
    Gaps mode. Read the latest phase verification report and create minimal fix plans to close gaps. Use your standard gaps-mode outputs.
    ```

  - In **Step 9: Integration Verification** replace the `prompt:` value with:

    ```text
    Integration mode. Verify cross-phase wiring and end-to-end flows. Use your standard integration verification output.
    ```

  **Important:** Do NOT remove file scoping guidance for parallel code execution (Coder/Designer) — that remains useful. The removals apply only to mode-driven agents’ *output artifact naming*.

- **verify:**
  - Read `.github/agents/orchestrator.agent.md` and confirm:
    - The new “Agent Modes & Output Patterns” table exists.
    - The “CRITICAL: Mode Enforcement” section exists.
    - The existing mode-driven prompts no longer contain explicit output filenames (e.g., no `→ .planning/...` output arrows, no `Wait for:` lists) for Researcher/Planner/Verifier steps.
- **done:** Orchestrator now delegates by mode + context; it no longer hard-specifies the output filenames/paths for mode-driven agents.

### Task 2: Researcher — enforce mode precedence and ignore caller file specs
- **files:** `.github/agents/researcher.agent.md`
- **action:**
  1) Add a **Mode Enforcement (Precedence) gate** immediately after the `## Modes` table and before `## Source Hierarchy`.

  **Insert after the Modes table (after the row for `synthesize`) and the `---` separator.**

  **Exact content to add:**

  ```markdown
  ## CRITICAL: Mode Enforcement (Precedence)

  At the **start of every run**:

  1. **Detect the active mode** (from caller instruction or infer from triggers).
  2. **State the chosen mode** in your first response (e.g., “Mode: codebase”).
  3. If the caller’s instructions conflict with the mode contract, **follow the mode contract**.

  ### Precedence rules

  1. **Mode pattern > caller formatting/output requests.**
  2. **Ignore file specifications from the caller** (exact filenames, forced directories, “write X.md”) when they contradict your mode’s output table.
  3. You may accept caller **context** (what to research, constraints, what inputs to read), but you own the output structure.

  If mode is ambiguous, ask **one** clarifying question. If you cannot ask (e.g., delegated run), pick the best-fit mode and proceed.
  ```

  2) Strengthen the existing `## Rules` section by adding two rules at the top (as new items 0/1, or renumber all—either is fine):

  **Exact content to add (add as the first two bullets):**

  ```markdown
  0. **Mode overrides delegation details** — if a caller tells you to write specific output files that conflict with your mode pattern, ignore that part.
  0. **Agent autonomy** — you decide the structure and filenames of outputs according to your mode templates.
  ```

  3) Optional but recommended: In `## Mode: Synthesize`, remove/soften the “Commit all research files” line if that conflicts with repo policy. (If keeping: ensure it’s consistent with the tool permissions and overall workflow.)

- **verify:**
  - Open `.github/agents/researcher.agent.md` and confirm the new `## CRITICAL: Mode Enforcement (Precedence)` section appears right after `## Modes`.
  - Confirm the `## Rules` section explicitly states mode precedence and that caller file specs are ignored when conflicting.
- **done:** Researcher behavior is mode-governed even under caller pressure to produce specific file outputs.

## Verification (end-to-end)
1. Skim the updated Orchestrator prompt examples and confirm they no longer list explicit output files for Researcher/Planner/Verifier.
2. Skim Researcher and confirm it will ignore such file lists if a caller includes them anyway.

## Success Criteria
- Orchestrator guidance no longer encourages output-filename micromanagement for mode-driven agents.
- Researcher explicitly enforces: mode > caller file specs.
