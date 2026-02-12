# Concerns & Improvement Opportunities

This catalog focuses on gaps that affect correctness, portability, and maintainability of the agent workflow system.

| Concern | Severity | Location | Description / Impact | Recommendation |
|---|---|---|---|---|
| `.github/` is gitignored | High | `.gitignore` | The repo ignores `.github/` entirely (`.github/`). If `.github/agents/` is intended to be the canonical, shareable location for agent specs, this prevents them from being committed and shared. | Decide the canonical source of truth and adjust `.gitignore` accordingly (or document clearly that `Agents/` is canonical and `.github/agents/` is local-only). |
| Duplicate agent directories (drift risk) | High | `Agents/` vs `.github/agents/` | Two parallel copies of each agent file increases the risk of mismatched behavior and documentation. | Pick canonical dir + add a sync mechanism or explicit guidance. |
| Mode enforcement is informal | Medium | `.github/agents/*` + `.planning/mode-enforcement/*` | Mode selection and output patterns are enforced via text conventions (“Project mode...”). Meta-plans exist but aren’t applied to agent specs yet. | Implement the “mode handshake” + “mode precedence” rules proposed in `.planning/mode-enforcement/`. |
| Researcher `SUMMARY.md` ambiguity | Medium | `researcher.agent.md` vs `orchestrator.agent.md` | Researcher project mode output table includes `SUMMARY.md`, but Orchestrator treats summary as synthesize step. Can cause duplicate/conflicting summaries. | Make summary production consistent (either only synthesize creates it, or define draft/final semantics). |
| Debugger mode not explicitly selected | Medium | `orchestrator.agent.md` | Orchestrator routes bugs to Debugger but doesn’t specify `find_and_fix` vs `find_root_cause_only`. Default may cause unintended code changes. | Add routing that selects mode based on user intent (“diagnose only” vs “fix”). |
| Windows shell incompatibility in Verifier examples | Medium | `verifier.agent.md` | Examples rely heavily on bash utilities (`grep`, `wc`, `test -f`). On Windows, these may fail without Git Bash/WSL. Verification may become non-reproducible. | Provide PowerShell-native equivalents or declare prerequisite tooling explicitly (ripgrep, git-bash). |
| Orchestrator over-specifies outputs for mode-driven agents | Medium | `orchestrator.agent.md` + `.planning/codebase/GAPS_AND_MODE_VIOLATIONS.md` | Orchestrator currently lists explicit output artifacts for mode-driven agents, reducing autonomy and increasing fragility. | Shift to “mode + objective + inputs + constraints” delegations; let mode-driven agents own output structure. |
| “Plans are prompts” vs examples that decide the HOW | Low/Med | `planner.agent.md` | Some examples include implementation-specific choices (e.g., JWT) which can undermine “WHAT not HOW”. | Keep examples outcome-focused; push implementation choices to Coder unless required by constraints. |
| No explicit licensing | Low | `AGENTS_GIST.md` | Mentions “Specify your license here” but no license is included. | Add a license file and reflect it in docs. |
| Backup files without policy | Low | `Agents/orchestrator.agent.md.backup`, `.github/agents/Backup-...` | Backups help, but can confuse consumers. | Document backup purpose or move to an archival folder. |

## Potential enhancements (beyond fixes)

1. **Agent spec validation**: add a script/CI step to validate YAML frontmatter and tool lists.
2. **Sync command**: a simple PowerShell script to sync `Agents/` ↔ `.github/agents/` with a “canonical source” switch.
3. **Portable verification snippets**: standardize on `rg` (ripgrep) and provide Windows + bash examples side-by-side.
4. **Explicit “mode handshake”**: require mode-driven agents to declare the mode they chose at the top of each run.

## Related existing repo documents

- `.planning/codebase/GAPS_AND_MODE_VIOLATIONS.md` — detailed gap catalog
- `.planning/mode-enforcement/PLAN-1-orchestrator-researcher.md` — proposed changes
- `.planning/mode-enforcement/PLAN-2-planner-verifier.md` — proposed changes