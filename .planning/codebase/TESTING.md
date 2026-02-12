# Testing Setup

This repository is not an executable application; it is a set of Copilot agent definitions and supporting documentation. There is **no unit/integration test framework configured** in the repo itself.

## What “testing” means for this repo

Testing here is largely:
- **Schema/format correctness** of `*.agent.md` files (YAML frontmatter validity; required keys present).
- **Installability** of agent links (deep links and wrapper URLs resolve correctly).
- **Behavioral smoke tests**: invoking agents in VS Code and verifying they follow their contracts.

## Embedded verification workflows (as part of agent design)

Although not repo tests, the agent system provides its own QA loops:
- Planner `validate` mode validates plans pre-execution.
- Verifier `phase`/`integration` modes validate that artifacts are real and wired.
- Debugger uses hypothesis-driven verification and regression checks.

## Gaps / improvement ideas

If you want automated checks in CI for this repository:
1. Add a Markdown linter (e.g., markdownlint) to reduce formatting drift.
2. Add a small script to parse each `*.agent.md` file and validate frontmatter:
   - required keys: `name`, `description`, `model`, `tools`
   - `tools` is a list
   - `name` matches expected file naming and capitalization
3. Add a link checker for `AGENTS_GIST.md` once a Gist ID is set (optional; requires network).

See also `.planning/codebase/CONCERNS.md` for portability risks (bash-centric verification examples).