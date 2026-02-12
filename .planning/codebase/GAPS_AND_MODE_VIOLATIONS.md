# Gaps in Mode Enforcement & Delegation Patterns (Current)

This is a gap/violation catalog focused on mode contracts and delegation behavior across Orchestrator, Researcher, Planner, Verifier, Debugger.

## 1) Orchestrator overrides mode-driven agents’ output contracts

**What happens now**

In `.github/agents/orchestrator.agent.md`, many delegations include:
- mandated output locations (e.g., “Write output to `.planning/research/`”)
- explicit artifact expectations (“Wait for: …”) and arrows like `→ .planning/research/*`

**Why it’s a gap**

Mode-driven agents (Researcher/Planner/Verifier) already define their output patterns. When the Orchestrator also dictates output filenames/paths, it:
- reduces agent autonomy
- increases fragility (if an agent evolves its mode templates)
- makes compliance ambiguous when Orchestrator and agent contracts disagree

**Evidence of recognized gap**

`.planning/mode-enforcement/PLAN-1-orchestrator-researcher.md` explicitly states the desired change:
- “Orchestrator delegations no longer prescribe output file names/paths for mode-driven agents…
- Researcher enforces mode detection… ignores caller file-spec instructions…”

## 2) Researcher mode contract has an internal ambiguity about `SUMMARY.md`

Researcher’s mode table claims **project mode outputs include** `.planning/research/SUMMARY.md`.

But the Orchestrator flow treats summary as a separate step:
- Step 1: project research → expects `STACK.md`, `FEATURES.md`, `ARCHITECTURE.md`, `PITFALLS.md`
- Step 2: synthesize → expects `SUMMARY.md`

This mismatch can cause:
- duplicated work (two summaries)
- confusion about which summary is authoritative

## 3) Debugger modes exist, but Orchestrator doesn’t select them

Debugger supports:
- `find_and_fix` (default)
- `find_root_cause_only`

Orchestrator routing says “Bug report → runSubagent(Debugger) directly” without specifying which behavior is desired.

Consequence: The Debugger will likely run `find_and_fix` even when the user wanted diagnosis only.

## 4) Re-verification naming is inconsistent in orchestration prompts

Orchestrator uses language like “Re-verify Phase [N]” but the Verifier has an explicit `re-verify` mode.

This is a minor gap, but matters if you later add stricter “mode parsing” that expects exact mode tokens.

## 5) Verifier’s command examples are shell-specific (bash/grep) vs Windows reality

Verifier relies heavily on `grep`, `wc`, `test -f`, and bash pipelines in its examples.

In a Windows-first workspace, these examples can:
- fail outright (if no GNU tools)
- reduce verifier effectiveness
- lead to “verification drift” (agent claims verification without reproducible commands)

This is a **mode quality risk** rather than a logical mode mismatch.

## 6) Duplicate agent spec directories increase drift risk

There are two parallel sets of agent specs:
- `.github/agents/*`
- `Agents/*`

They are largely similar, but the Orchestrator frontmatter/tooling differs (e.g., `.github/agents/orchestrator.agent.md` declares `agent/runSubagent`, while `Agents/orchestrator.agent.md` has a different tool list).

Risk:
- edits applied to one directory may not affect the active agent runtime
- readers may follow the wrong doc

## 7) Planner “WHAT not HOW” philosophy can be undermined by plan templates

Planner’s plan format includes an `action:` field in tasks.

The examples sometimes cross into “how” (implementation specifics like exact endpoints + JWT choices), even while the doc says:
- “WHAT not HOW — describe outcomes…”

This is subtle, but it can encourage Orchestrator/Planner to pre-decide implementation details that the Coder could otherwise choose.

## 8) Missing explicit, universal “mode handshake”

Currently, the system relies on informal text (“Project mode…”) rather than a strict handshake:
- no required first-line “Mode: X” acknowledgement (except proposed in `.planning/mode-enforcement/PLAN-1…`)
- no enforcement that agents announce chosen mode

Consequence: mode confusion is more likely under delegation pressure or long prompts.

## 9) Delegation boundary is strong for tools, weaker for responsibilities

Orchestrator correctly says:
- it cannot implement and must delegate using `runSubagent`

But Orchestrator also contains highly detailed step-by-step instructions for subagents (including expected artifacts). This creates a “responsibility blur”: the Orchestrator becomes a pseudo-spec writer rather than a coordinator.

This aligns with the existing “mode-enforcement” plans that attempt to push output ownership back to the mode-driven agents.
