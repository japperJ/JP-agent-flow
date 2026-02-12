# Code Conventions

This repository is primarily composed of agent definitions and workflow documentation.

## Naming and file conventions

### Agent definition files
- Extension: `*.agent.md`
- Frontmatter: YAML block at the top with keys:
  - `name:` (must match the invocation name exactly; capitalization matters)
  - `description:`
  - `model:` (metadata)
  - `tools:` (capability boundary)

### Agent directories
- `.github/agents/` — conventional agent runtime location for the workspace.
- `Agents/` — used for publishing via Gist (per `GIST_PUBLISHING_GUIDE.md`).

### Backups
- `orchestrator.agent.md.backup` and `Backup-orchestrator.agent.md.backup` exist as manual snapshots.

## Workflow conventions (the `.planning/` contract)

Even though this repo does not contain a running application, the agent system defines a consistent artifact workflow used when applied to other projects:

- **Roadmap artifacts** (Planner roadmap mode)
  - `.planning/ROADMAP.md`
  - `.planning/REQUIREMENTS.md` (REQ-IDs)
  - `.planning/STATE.md`

- **Phase artifacts**
  - Researcher: `.planning/phases/<phase>/RESEARCH.md`
  - Planner: `.planning/phases/<phase>/PLAN.md`
  - Coder: `.planning/phases/<phase>/SUMMARY.md` (+ updates `STATE.md`)
  - Verifier: `.planning/phases/<phase>/VERIFICATION.md`

- **Integration verification**
  - Verifier: `.planning/INTEGRATION.md`

- **Debug sessions**
  - Debugger: `.planning/debug/BUG-[timestamp].md` with immutable symptoms and append-only evidence

## Planning style rules encoded in agents

### Planner
- Plans are prompts.
- Prefer 2–3 tasks per plan.
- Each task must specify: `files`, `action`, `verify`, `done`.
- Must-haves derived goal-backward.

### Coder
- Context7-first when using external libraries.
- One task = one commit; never `git add .`.
- Stop at checkpoints (human-verify/decision/human-action/auth-gate).

### Verifier
- Independent verification; does not trust summaries.
- Artifact verification levels: existence, substance, wired.
- Writes structured gaps in YAML frontmatter.

## Documentation conventions

- Install links are presented as GitHub-friendly badge links using the `aka.ms/awesome-copilot/install/agent?...` wrapper (see `AGENTS_GIST.md` and `.planning/research/VSCODE_INSTALL_FORMAT.md`).