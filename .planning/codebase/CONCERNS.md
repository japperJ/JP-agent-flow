# Concerns & Tech Debt

| Concern | Severity | Location | Description |
|---|---|---|---|
| `.github/` is ignored | High | `.gitignore` | `.gitignore` contains `.github/`, which means `.github/agents/*` is likely not tracked/committed. This undermines repository-scoped agent distribution (and can create confusion about the canonical source of truth). |
| Duplicate agent sources | Medium | `Agents/` vs `.github/agents/` | The same 7 `*.agent.md` files exist in two places. Without an explicit “canonical” statement, edits can drift or be applied to the wrong copy. |
| Orchestrator invocation naming inconsistency | High | `Agents/orchestrator.agent.md` | The Orchestrator text says “Use the exact agent name (lowercase) from the table above”, but the table shows capitalized names and the repo’s README says to use capitalized names. This can break orchestration calls depending on the actual tool’s expectations. |
| Orchestrator file appears partially corrupted / duplicated | Medium | `Agents/orchestrator.agent.md` | There are duplicated lines and a garbled sentence (e.g., “`.planning/phases/[N]/SUMMARY.md`st it — verify independently…”). This is likely an edit/merge artifact and could confuse users and the Orchestrator agent. |
| `.planning/` contract is described but not present in repo | Low | `.planning/` | The system expects `ROADMAP.md`, `STATE.md`, phases, etc., but this repository currently contains only `.planning/research/*` plus newly created `.planning/codebase/*`. This is fine for an “agent template” repo, but new users may assume those artifacts exist. |
| No explicit license | Medium | `AGENTS_GIST.md` | `AGENTS_GIST.md` has a “License” section that is a placeholder (“[Specify your license here]”). If this is intended for public sharing, the licensing terms are unclear. |
| Lack of automated validation | Low | repo-wide | There are no CI workflows, linting, or checks to ensure the two agent copies match, frontmatter is valid, or docs links remain correct. |

## Suggested follow-ups (non-implementation)
- Decide and document **one canonical agent source** (`Agents/` *or* `.github/agents/`).
- If repo-scoped agents are desired, consider removing `.github/` from `.gitignore` (or narrowing it) so `.github/agents/` is tracked.
- Fix Orchestrator naming text to be internally consistent with the README guidance.
- Clean up the duplicated/garbled lines in `orchestrator.agent.md` to reduce operational risk.
- Add a clear license.
