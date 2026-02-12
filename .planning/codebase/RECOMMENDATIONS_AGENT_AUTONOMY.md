# Recommendations: Strengthen Mode Enforcement & Agent Autonomy

These are improvement recommendations derived from the current agent specs and the existing meta-plans under `.planning/mode-enforcement/`.

## 1) Adopt a universal mode handshake

For mode-driven agents (Researcher/Planner/Verifier/Debugger), require:
- agent declares selected mode in first response (e.g., “Mode: phase”)
- agent states which inputs it will read
- agent states what artifacts it will produce *per its own contract*

This reduces ambiguity and makes delegation auditable.

## 2) Make “mode precedence” explicit in every mode-driven agent

The repo already has draft plans to do this:
- `.planning/mode-enforcement/PLAN-1-orchestrator-researcher.md`
- `.planning/mode-enforcement/PLAN-2-planner-verifier.md`

Extend the same idea to Debugger (and optionally Coder’s “execution model”):
- caller constraints are accepted
- caller output micromanagement is ignored when it conflicts with mode

## 3) Remove Orchestrator artifact micromanagement for mode-driven agents

Shift Orchestrator from:
- “Write X file; wait for Y file”

to:
- “<Mode> mode. Objective: … Inputs: … Constraints: … Use your standard outputs.”

This aligns with the existing meta-plan intent.

## 4) Fix the Researcher `SUMMARY.md` ambiguity

Choose one of these and make it consistent:
- Option A: project mode produces the four satellite docs only; synthesize produces `SUMMARY.md`
- Option B: project mode produces a “draft summary”; synthesize upgrades it and is the only step that finalizes it

## 5) Improve Windows-friendly verification guidance

For Verifier (and Debugger examples), add a PowerShell-friendly alternative to the bash/grep patterns, or clarify prerequisites (Git Bash, ripgrep, etc.).

Goal: keep verification reproducible and avoid “verification drift” due to unusable command snippets.

## 6) Eliminate or clearly document the duplicate agent spec directory

Right now, `.github/agents/` and `Agents/` both exist.

To reduce drift:
- declare one directory as canonical
- or keep both but add explicit “generated/mirrored” guidance + a sync mechanism

## 7) Standardize delegation prompt templates

A robust minimal template for Orchestrator to use with mode-driven agents:

- **Mode:** `<mode>`
- **Objective:** what must be true when done
- **Inputs to read:** paths or sources
- **Constraints:** budget/time/stack decisions
- **Non-goals:** what not to do

This reduces both over-specification (micromanagement) and under-specification (vague delegation).
