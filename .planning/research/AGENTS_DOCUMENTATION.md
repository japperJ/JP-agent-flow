# Agents Documentation Research

## Scope
This document inventories workspace agent definitions under `.github/agents/` (and notes duplicates under `Agents/`), analyzes the example Gist format, and recommends a structure for publishing these agents as a Gist.

- **Workspace scanned:** `c:\REP\JP agent flow`
- **Primary agent folder found:** `.github/agents/`
- **Also present (duplicate set):** `Agents/`

> Note: `.github/agents/` and `Agents/` both contain the same set of files by name. The `*.agent.md` files are the actual agent definitions; `README.md` is supporting documentation.

---

## 1) Agents found in `.github/agents/`

### Inventory (agent definition files)
- `.github/agents/coder.agent.md`
- `.github/agents/debugger.agent.md`
- `.github/agents/designer.agent.md`
- `.github/agents/orchestrator.agent.md`
- `.github/agents/planner.agent.md`
- `.github/agents/researcher.agent.md`
- `.github/agents/verifier.agent.md`

### Supporting docs
- `.github/agents/README.md` (notes about orchestrator subagent naming and general usage)

---

## 2) Per-agent summary (name, purpose, capabilities, specialty/mode)

Below, **capabilities** are inferred from (a) the agent’s written responsibilities and (b) its declared `tools:` list in YAML frontmatter.

### Orchestrator
- **File:** `.github/agents/orchestrator.agent.md`
- **Agent name:** `Orchestrator`
- **Purpose/description (frontmatter):** “JP Coordinates the full development lifecycle by delegating to subagents. Never implements directly.”
- **Capabilities (tools):** `read/readFile`, `agent`, `memory`
  - Practically: can read context, invoke subagents, and maintain memory; **no direct edit/execute/search** tools.
- **Specialty / mode:** Lifecycle coordinator; explicitly **delegates** across phases: Research → Plan → Execute → Verify → Debug → Iterate.
- **Notable conventions:**
  - Strong constraints around calling `runSubagent` and using **relative paths** in delegation.
  - Parallelization guidance based on file overlap.

### Planner
- **File:** `.github/agents/planner.agent.md`
- **Agent name:** `Planner`
- **Purpose/description:** Creates roadmaps, implementation plans, and validates plans; plans are executable “prompts” for a single agent session.
- **Capabilities (tools):** `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`, `todo`
  - Can investigate codebase, consult docs/web, and author planning artifacts.
- **Specialty / mode(s):** Explicit modes: `roadmap`, `plan`, `validate`, `gaps`, `revise`.
- **Notable conventions:**
  - “WHAT not HOW” planning style.
  - Must-haves tracing and goal-backward planning.

### Researcher
- **File:** `.github/agents/researcher.agent.md`
- **Agent name:** `Researcher`
- **Purpose/description:** Investigates technologies, maps codebases, and researches implementation approaches; “Context7-first, source-verified.”
- **Capabilities (tools):** `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`
- **Specialty / mode(s):** Explicit modes: `project`, `phase`, `codebase`, `synthesize`.
- **Notable conventions:**
  - Source hierarchy (Context7 → official docs → web → training data).
  - Requires confidence levels and explicit sourcing.

### Coder
- **File:** `.github/agents/coder.agent.md`
- **Agent name:** `Coder`
- **Purpose/description:** Writes code following mandatory coding principles; executes plans atomically with per-task commits.
- **Capabilities (tools):** `vscode`, `execute`, `read`, `context7/*`, `github/*`, `edit`, `search`, `web`, `memory`, `todo`
  - Can implement and verify changes, and interact with GitHub tooling.
- **Specialty / mode:** Implementation/execution agent; follows strong “Execution Model” for consuming `.planning/.../PLAN.md`.
- **Notable conventions:**
  - Mandatory coding principles (structure/architecture/naming/errors/regenerability).
  - Commit protocol (one task, one commit; never `git add .`).
  - Explicit checkpoint format.

### Designer
- **File:** `.github/agents/designer.agent.md`
- **Agent name:** `Designer`
- **Purpose/description:** Handles UI/UX; prioritizes usability, accessibility, aesthetics.
- **Capabilities (tools):** `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`, `todo`
- **Specialty / mode:** UI/UX implementation with accessibility emphasis (WCAG 2.1 AA mentioned).
- **Notable conventions:**
  - Pushes back on technical constraints that harm UX.

### Debugger
- **File:** `.github/agents/debugger.agent.md`
- **Agent name:** `Debugger`
- **Purpose/description:** Scientific debugging with hypothesis testing, persistent debug files, and structured investigation.
- **Capabilities (tools):** `vscode`, `execute`, `read`, `edit`, `search`, `web`, `memory`, `context7/*`
- **Specialty / mode(s):** Explicit modes: `find_and_fix` (default) and `find_root_cause_only`.
- **Notable conventions:**
  - Mandatory `.planning/debug/` debug file protocol, immutable symptoms, append-only evidence logs.
  - Bias mitigation, 3-test limit per hypothesis.

### Verifier
- **File:** `.github/agents/verifier.agent.md`
- **Agent name:** `Verifier`
- **Purpose/description:** Goal-backward verification of phase outcomes and cross-phase integration.
- **Capabilities (tools):** `vscode`, `execute`, `read`, `edit`, `search`, `memory`
- **Specialty / mode(s):** Explicit modes: `phase`, `integration`, `re-verify`.
- **Notable conventions:**
  - “Task completion ≠ goal achievement” with structured verification checklists.
  - Uses YAML frontmatter for gaps in `VERIFICATION.md`.

---

## 3) Example Gist analysis (format + structure)

**Source provided:** https://gist.github.com/burkeholland/0e68481f96e94bbb98134fa6efd00436

### What the example Gist contains
The Gist is a *multi-file* Gist centered around a top-level Markdown doc (`ainstall.md`) plus separate `*.agent.md` files.

#### A) `ainstall.md` (landing page)
Key structural elements observed:
1. **Title + short description** (e.g., “Ultralight Orchestration”).
2. **Instructions** section.
3. **Install table** listing each agent with:
   - Agent name as a link
   - “Install in VS Code” badge link
   - “Install in VS Code Insiders” badge link
   - Type column (e.g., “Agent”)
   - Description column
4. **Agent Breakdown** section with per-agent subsections:
   - `### Orchestrator (Model)` etc.
   - Brief bullet list describing responsibilities.

This page is written to be both human-readable and directly actionable (install links up front).

#### B) Individual agent definition files
Each agent is stored as its own `*.agent.md` file.

Common pattern:
- **YAML frontmatter** at the top:
  - `name:`
  - `description:`
  - `model:`
  - `tools:`
- Body content contains role instructions, rules, and (where relevant) a workflow.

### Notes relevant to your workspace
- The example Gist includes 4 core agents (Orchestrator/Planner/Coder/Designer). Your workspace extends this with **Researcher**, **Debugger**, and **Verifier**.
- The Orchestrator in the example also includes a comment about **Memory being experimental** in VS Code Insiders.

---

## 4) Recommendations for structuring *your* new Gist page

### Recommended Gist file layout
Use a **multi-file Gist** (same approach as the example):
- `README.md` (or `ainstall.md`) as the landing page
- One file per agent definition:
  - `orchestrator.agent.md`
  - `planner.agent.md`
  - `researcher.agent.md`
  - `coder.agent.md`
  - `designer.agent.md`
  - `debugger.agent.md`
  - `verifier.agent.md`

### Recommended landing page sections (order matters)
1. **Title + one-paragraph overview**
   - State: what the agent set is for (multi-agent workflow), and what environments it targets (VS Code / Insiders).
2. **Quick install section**
   - A table like the example (agent name + install links + short description).
   - Include both VS Code and VS Code Insiders install badges.
3. **Agent breakdown**
   - One `###` heading per agent.
   - 3–6 bullets each: what it does, when to use it, and key constraints.
4. **How they work together**
   - A short “Lifecycle” or “Flow” diagram (ASCII is fine).
   - Mention: file-overlap parallelization rule.
5. **Artifacts and folder conventions**
   - Document `.planning/` outputs expected by Planner/Researcher/Coder/Verifier/Debugger (e.g., `.planning/phases/...`, `.planning/debug/...`).
6. **Gotchas / troubleshooting**
   - Memory experimental toggle (if applicable).
   - Tooling prerequisites (Context7 MCP, GitHub MCP), if your agent set expects them.

### Formatting conventions to adopt
- Keep each agent’s `*.agent.md` file with consistent YAML frontmatter keys: `name`, `description`, `model`, `tools`.
- Use consistent headings inside each agent file:
  - `## Modes` (if applicable)
  - `## Workflow` / `## Execution Model`
  - `## Rules`
- Avoid duplicating long bodies on the landing page; keep the landing page *summary*, link to agent files for full details.

### Recommendation specific to *this repo*
Because the repository has both `.github/agents/` and `Agents/`, pick one canonical location (for the repo) and mention it once in docs. For a Gist, the location becomes irrelevant; what matters is the agent file content.

---

## Sources
- Workspace agent definitions: `.github/agents/*.agent.md` and `.github/agents/README.md`
- Example Gist landing + raw files:
  - https://gist.github.com/burkeholland/0e68481f96e94bbb98134fa6efd00436
  - https://gist.githubusercontent.com/burkeholland/0e68481f96e94bbb98134fa6efd00436/raw/fce5baafdc7e5f44ecb236be3cb9502a4e208752/ainstall.md
  - https://gist.githubusercontent.com/burkeholland/0e68481f96e94bbb98134fa6efd00436/raw/fce5baafdc7e5f44ecb236be3cb9502a4e208752/orchestrator.agent.md
  - https://gist.githubusercontent.com/burkeholland/0e68481f96e94bbb98134fa6efd00436/raw/fce5baafdc7e5f44ecb236be3cb9502a4e208752/planner.agent.md
  - https://gist.githubusercontent.com/burkeholland/0e68481f96e94bbb98134fa6efd00436/raw/fce5baafdc7e5f44ecb236be3cb9502a4e208752/coder.agent.md
  - https://gist.githubusercontent.com/burkeholland/0e68481f96e94bbb98134fa6efd00436/raw/fce5baafdc7e5f44ecb236be3cb9502a4e208752/designer.agent.md

Additional context referenced in the Gist comments:
- Context7 MCP extension (example prerequisite): https://marketplace.visualstudio.com/items?itemName=Upstash.context7-mcp

Notes:
- The example Gist uses `aka.ms/awesome-copilot/install/agent?url=...` wrapper links which ultimately hand off to `vscode:` / `vscode-insiders:` deep links. These wrappers may not render meaningful HTML content when fetched via a text extractor, but their structure is visible directly in the `ainstall.md` source.
