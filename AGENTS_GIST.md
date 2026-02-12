# JP Multi-Agent Development System

A comprehensive, production-ready agent workflow for VS Code and VS Code Insiders that orchestrates seven specialized agents through the complete software development lifecycle. From initial research through planning, implementation, verification, and debugging — all with structured artifact tracking and goal-backward validation.

Built for solo developers who want AI agent collaboration that works like a senior engineering team.

---

## ⚠️ IMPORTANT: Publishing & Install Link Setup

**This file must be published to GitHub Gist before the install badges will work.**

The VS Code agent installer wrapper (`https://aka.ms/awesome-copilot/install/agent`) rejects URLs from `raw.githubusercontent.com` domains. The solution is to host the agent files via **GitHub Gist raw URLs** instead.

### Publishing Workflow:

1. **Publish to Gist:** Upload all 7 agent files (`orchestrator.agent.md`, `researcher.agent.md`, etc.) to a GitHub Gist
2. **Get the Gist ID:** After publishing, your Gist URL will be `https://gist.github.com/japperJ/cdeaa98b5d7dd612d525d73bdc456e28`
3. **Update the install badges below:** Replace `cdeaa98b5d7dd612d525d73bdc456e28` placeholders with your actual Gist ID

### URL Format Reference:

Once published, the correct install badge URLs follow this pattern:

**For VS Code (stable):**
```
https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2FAGENT_FILE.agent.md
```

**For VS Code Insiders:**
```
https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2FAGENT_FILE.agent.md
```

Where:
- `cdeaa98b5d7dd612d525d73bdc456e28` = Your actual Gist ID (from step 2 above)
- `AGENT_FILE.agent.md` = `orchestrator.agent.md`, `researcher.agent.md`, `planner.agent.md`, etc.

---

## Installation

**📝 Note:** These install badges will work once this Gist is published and you replace `cdeaa98b5d7dd612d525d73bdc456e28` with your actual Gist ID in the URLs below.

Install any or all agents directly into VS Code or VS Code Insiders. Each agent operates independently but works seamlessly when orchestrated together.

| Agent | Description | Install |
|-------|-------------|---------|
| **[Orchestrator](#orchestrator-claude-sonnet-45)** | Coordinates the full lifecycle by delegating to subagents. Never implements directly. | [![Install in VS Code](https://img.shields.io/badge/VS%20Code-Install-blue?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Forchestrator.agent.md) [![Install in VS Code Insiders](https://img.shields.io/badge/Insiders-Install-green?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Forchestrator.agent.md) |
| **[Researcher](#researcher-gpt-52)** | Investigates technologies, maps codebases, Context7-first source verification. | [![Install in VS Code](https://img.shields.io/badge/VS%20Code-Install-blue?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fresearcher.agent.md) [![Install in VS Code Insiders](https://img.shields.io/badge/Insiders-Install-green?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fresearcher.agent.md) |
| **[Planner](#planner-gpt-52)** | Creates roadmaps and executable plans. Plans are prompts — WHAT not HOW. | [![Install in VS Code](https://img.shields.io/badge/VS%20Code-Install-blue?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fplanner.agent.md) [![Install in VS Code Insiders](https://img.shields.io/badge/Insiders-Install-green?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fplanner.agent.md) |
| **[Coder](#coder-claude-opus-46)** | Writes code following mandatory principles. Executes plans atomically with per-task commits. | [![Install in VS Code](https://img.shields.io/badge/VS%20Code-Install-blue?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fcoder.agent.md) [![Install in VS Code Insiders](https://img.shields.io/badge/Insiders-Install-green?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fcoder.agent.md) |
| **[Designer](#designer-gemini-3-pro-preview)** | Handles all UI/UX. Prioritizes usability, accessibility, aesthetics. Never compromises on UX. | [![Install in VS Code](https://img.shields.io/badge/VS%20Code-Install-blue?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fdesigner.agent.md) [![Install in VS Code Insiders](https://img.shields.io/badge/Insiders-Install-green?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fdesigner.agent.md) |
| **[Verifier](#verifier-claude-sonnet-45)** | Goal-backward verification. Task completion ≠ goal achievement. | [![Install in VS Code](https://img.shields.io/badge/VS%20Code-Install-blue?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fverifier.agent.md) [![Install in VS Code Insiders](https://img.shields.io/badge/Insiders-Install-green?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fverifier.agent.md) |
| **[Debugger](#debugger-claude-opus-46)** | Scientific debugging with hypothesis testing. Persistent debug files and bias mitigation. | [![Install in VS Code](https://img.shields.io/badge/VS%20Code-Install-blue?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fdebugger.agent.md) [![Install in VS Code Insiders](https://img.shields.io/badge/Insiders-Install-green?logo=visualstudiocode)](https://aka.ms/awesome-copilot/install/agent?url=vscode-insiders%3Achat-agent%2Finstall%3Furl%3Dhttps%3A%2F%2Fgist.githubusercontent.com%2FjapperJ%2Fcdeaa98b5d7dd612d525d73bdc456e28%2Fraw%2Fdebugger.agent.md) |

### How to Complete Setup After Publishing:

1. Note your Gist ID from the URL (e.g., `https://gist.github.com/japperJ/abc123def456` → Gist ID is `abc123def456`)
2. Do a find-replace in this file: `cdeaa98b5d7dd612d525d73bdc456e28` → your actual Gist ID
3. The install badges will now work correctly!

> **Repository:** https://github.com/japperJ/JP-agent-flow

---

## Agent Breakdown

### Orchestrator (Claude Sonnet 4.5)

**The project coordinator.** Breaks down complex requests into lifecycle phases and delegates to specialized subagents. Never implements anything itself.

- **Model:** Claude Sonnet 4.5 (copilot)
- **Tools:** `read/readFile`, `agent`, `memory`
- **Purpose:** Lifecycle coordination across Research → Plan → Execute → Verify → Debug → Iterate

**Key Capabilities:**
- Request routing (determines which agents to invoke for any task)
- Full 10-step execution model for greenfield projects
- Phase-based workflow with gap-closure loops
- Intelligent parallelization based on file-overlap rules
- Manages `.planning/` artifact structure across all phases

**When to use:**
- Starting a new project from scratch
- Adding complex features that span multiple concerns
- Any task requiring coordination between multiple agents

**Never does:**
- Implement code directly (has no edit tools)
- Make architectural decisions without delegation
- Tell agents HOW to do their work (only WHAT)

**Core Workflow:**
```
User Request
    ↓
Orchestrator analyzes scope
    ↓
Delegates to: Researcher → Planner → Coder/Designer → Verifier
    ↓
Monitors progress, handles gaps, reports completion
```

---

### Researcher (GPT-5.2)

**The investigator.** Researches technologies, maps codebases, verifies implementation approaches. Context7-first with explicit source verification.

- **Model:** GPT-5.2 (copilot)
- **Tools:** `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`
- **Purpose:** Technology investigation, codebase analysis, and implementation research

**Operating Modes:**
1. **Project mode** — New projects: researches domain, tech stack, architecture patterns, pitfalls
2. **Phase mode** — Research implementation details for a specific phase
3. **Codebase mode** — Maps existing codebases (stack, architecture, conventions, concerns)
4. **Synthesize mode** — Consolidates multiple research outputs into unified summary

**Source Hierarchy (strict priority order):**
1. **Context7** (`#context7`) — HIGH confidence — Always try first for library/framework docs
2. **Official docs** (web) — HIGH confidence — When Context7 lacks detail
3. **Web search** (web) — MEDIUM confidence — Ecosystem discovery, comparisons
4. **Training data** — LOW confidence — Only when above fail, flagged as unverified

**Key Features:**
- Every finding includes confidence level and source citation
- Negative claims ("X doesn't support Y") require extra verification
- Outputs to `.planning/research/` or `.planning/phases/N/RESEARCH.md`
- Never implements — research only

**Typical Output Files:**
- `SUMMARY.md` — Executive summary with recommendations
- `STACK.md` — Technology choices with rationale
- `FEATURES.md` — Feature analysis with standard approaches
- `ARCHITECTURE.md` — Recommended patterns
- `PITFALLS.md` — Known issues and mitigation strategies

---

### Planner (GPT-5.2)

**The architect.** Creates roadmaps, phase plans, and validates completeness. Plans are executable prompts — describes WHAT, not HOW.

- **Model:** GPT-5.2 (copilot)
- **Tools:** `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`, `todo`
- **Purpose:** Strategic planning and task breakdown with goal-backward validation

**Operating Modes:**
1. **Roadmap mode** — Creates phase breakdown, requirement mapping, success criteria
2. **Plan mode** — Task-level planning for specific phases (2-3 tasks per plan)
3. **Validate mode** — Verifies plans will achieve goals across 6 dimensions
4. **Gaps mode** — Creates fix plans from verification failures
5. **Revise mode** — Updates plans based on validation issues

**Core Philosophy:**
- **Plans are prompts** — Each executable by one agent in one session
- **WHAT not HOW** — Describes outcomes and constraints, not implementation
- **Goal-backward** — Derives what must exist from what must be true
- **Anti-enterprise** — If it needs a meeting to understand, it's too complex
- **Research first** — Uses `#context7` before making technical assumptions

**Quality Control:**
- Targets 2-3 tasks per plan (5 max before splitting)
- Keeps plans under 50% of executing agent's context budget
- 6-dimensional validation: requirements coverage, task completeness, dependencies, key links, scope, must-haves

**Task Anatomy:**
Every task has `files`, `action`, `verify`, `done` — fully specified and testable

**Outputs:**
- `ROADMAP.md` — Phase breakdown with success criteria
- `REQUIREMENTS.md` — Traceable requirements with REQ-IDs
- `STATE.md` — Project state tracking
- `PLAN.md` files — Executable task plans (one per task group)

---

### Coder (Claude Opus 4.6)

**The implementer.** Writes production-quality code following mandatory principles. Executes plans atomically with per-task commits.

- **Model:** Claude Opus 4.6 (copilot)
- **Tools:** `vscode`, `execute`, `read`, `context7/*`, `github/*`, `edit`, `search`, `web`, `memory`, `todo`
- **Purpose:** Code implementation with strict quality standards and commit discipline

**Mandatory Coding Principles:**
1. **Structure** — Consistent layout, feature-based grouping, shared structure first
2. **Architecture** — Flat and explicit, no premature abstraction
3. **Functions** — Linear control flow, single purpose, prefer pure
4. **Naming & Comments** — Descriptive names, comments explain WHY not WHAT
5. **Logging & Errors** — Structured logging, explicit error handling
6. **Regenerability** — Files rewritable from interface contracts
7. **Platform Use** — Use conventions directly, don't wrap unnecessarily
8. **Modifications** — Match existing patterns exactly
9. **Quality** — Deterministic, testable, fail loud and early

**Execution Model:**
1. Loads `STATE.md` and `PLAN.md`
2. Executes tasks sequentially
3. Verifies each task with specified command
4. Commits after each successful task (conventional commits)
5. Stops at checkpoints for human input
6. Creates `SUMMARY.md` when complete

**Deviation Handling (priority order):**
- **Rule 4** (highest): STOP for architecture changes → decision checkpoint
- **Rule 1**: Auto-fix bugs (syntax, logic, types, security) → document in summary
- **Rule 2**: Auto-add critical pieces (validation, error handling, auth) → document
- **Rule 3**: Auto-fix blockers (dependencies, imports) → document

**Commit Protocol:**
- One task, one commit (never batch)
- Never `git add .` — stage files individually
- Conventional commit types: `feat`, `fix`, `test`, `refactor`, `perf`, `docs`, `style`, `chore`

**TDD Support:**
When detected, uses RED → GREEN → REFACTOR structure with separate commits per phase

---

### Designer (Gemini 3 Pro Preview)

**The UX advocate.** Handles all UI/UX design with uncompromising focus on usability, accessibility, and aesthetics.

- **Model:** Gemini 3 Pro (Preview) (copilot)
- **Tools:** `vscode`, `execute`, `read`, `context7/*`, `edit`, `search`, `web`, `memory`, `todo`
- **Purpose:** UI/UX implementation prioritizing user experience over technical convenience

**Priority Order (strictly enforced):**
1. **Usability** — Can users accomplish their goal without thinking?
2. **Accessibility** — Can everyone use it, regardless of ability?
3. **Aesthetics** — Does it look and feel polished?

**Core Principles:**
- **Less is more** — Remove until removing anything else breaks it
- **Consistency** — Reuse existing components before creating new ones
- **Feedback** — Every user action gets visible response
- **Hierarchy** — Most important = most visible
- **Whitespace** — Give elements room to breathe
- **Motion** — Animate with purpose, never decoration

**Key Characteristics:**
- Pushes back on technical constraints that harm UX
- Implements complete working code (not mockups)
- Tests responsiveness across breakpoints
- Ensures WCAG 2.1 AA compliance minimum
- Reads `.planning/phases/N/RESEARCH.md` for design constraints
- Follows existing design language (never introduces new one)

**Context Awareness:**
- Checks `CONVENTIONS.md` for existing design patterns
- Consults `#context7` for component library docs
- Researches existing design systems before creating new components

---

### Verifier (Claude Sonnet 4.5)

**The quality gatekeeper.** Goal-backward verification that work achieved its goal, not just that tasks were completed.

- **Model:** Claude Sonnet 4.5 (copilot)
- **Tools:** `vscode`, `execute`, `read`, `edit`, `search`, `memory`
- **Purpose:** Independent verification with systematic gap detection

**Core Principle:**
**Task completion ≠ Goal achievement.** Files can exist without being functional. Functions can be exported without being imported. Routes can be defined without being reachable.

**Operating Modes:**
1. **Phase mode** — Verifies phase implementation against success criteria
2. **Integration mode** — Verifies cross-phase wiring and end-to-end flows
3. **Re-verify mode** — Re-checks after gap closure

**10-Step Phase Verification:**
1. Check for previous verification (re-verification handling)
2. Load context (roadmap, requirements, state)
3. Establish must-haves (observable truths, artifacts, wiring)
4. Verify observable truths (independently test each)
5. Verify artifacts (3 levels: existence → substance → wired)
6. Verify key links (component→API, API→DB, form→handler, state→render)
7. Check requirements coverage
8. Scan for anti-patterns (TODOs, placeholders, empty implementations)
9. Identify human verification needs
10. Structure gap output in YAML

**3-Level Artifact Verification:**
- **Level 1: Existence** — File exists?
- **Level 2: Substance** — Real code, not stub? (line count thresholds)
- **Level 3: Wired** — Actually imported and used elsewhere?

**Integration Verification:**
1. Build export/import map across phases
2. Verify export usage (connected, imported-not-used, orphaned)
3. Verify API coverage (defined routes vs called routes)
4. Verify auth protection (which routes protected?)
5. Verify end-to-end flows (auth, data, forms)
6. Compile integration report

**Verification Statuses:**
- **PASSED** — All checks satisfied
- **GAPS_FOUND** — Failures documented with YAML frontmatter
- **HUMAN_NEEDED** — Programmatic checks passed, manual verification required

**Gap Structure:**
- Type: artifact / key_link / truth / requirement
- Severity: blocker / warning / info
- Evidence: bash commands showing the gap
- Issue: precise description

**Critical Rule:** Does NOT trust SUMMARY.md — verifies everything independently with bash commands

---

### Debugger (Claude Opus 4.6)

**The scientific investigator.** Finds and fixes bugs using hypothesis testing with persistent debug files and cognitive bias mitigation.

- **Model:** Claude Opus 4.6 (copilot)
- **Tools:** `vscode`, `execute`, `read`, `edit`, `search`, `web`, `memory`, `context7/*`
- **Purpose:** Systematic debugging with scientific methodology

**Philosophy:**
- **User = reporter, you = investigator** — Symptoms ≠ root causes
- **Your own code is harder to debug** — Watch for confirmation bias
- **Systematic over heroic** — Methodical elimination beats inspired guessing

**Operating Modes:**
1. **find_and_fix** (default) — Find root cause AND implement fix
2. **find_root_cause_only** — Find and document, don't fix

**Cognitive Bias Guards:**
| Bias | Trap | Antidote |
|------|------|----------|
| Confirmation | Looking only for supporting evidence | Actively try to DISPROVE hypothesis |
| Anchoring | Fixating on first clue | Generate ≥2 hypotheses before testing |
| Availability | Blaming most recent change | Check git log but don't assume recent=guilty |
| Sunk Cost | Sticking with wrong theory | 3-test limit per hypothesis, then pivot |

**Debug File Protocol:**
Every session gets persistent `.planning/debug/BUG-[timestamp].md` with:
- **Symptoms** (IMMUTABLE) — Original report, never edited
- **Current Focus** (OVERWRITE) — Current hypothesis being tested
- **Eliminated Hypotheses** (APPEND-ONLY) — Failed theories stay for reference
- **Evidence Log** (APPEND-ONLY) — All observations preserved
- **Resolution** (OVERWRITE) — Root cause and fix when found

**Investigation Techniques:**
- **Binary Search** — Narrow problem space by halving
- **Rubber Duck** — Explain code path, find mismatch
- **Minimal Reproduction** — Strip until only bug remains
- **Working Backwards** — Trace wrong output to source
- **Differential** — Compare working vs broken
- **Observability First** — Strategic logging before hypothesizing
- **Comment Out Everything** — When all else fails
- **Git Bisect** — When it used to work

**Hypothesis Testing Protocol:**
1. Form ≥2 hypotheses
2. Rank by testability (not likelihood)
3. For each: Predict → Design test → Execute → Evaluate
4. 3-test limit — if unresolved, refine or pivot

**Verification Requirements:**
Fix is verified when ALL true:
1. Original symptom gone
2. Fix addresses root cause (not symptom)
3. No new failures introduced
4. Works consistently (not just once)
5. Related functionality intact

**When to Restart:**
- 3+ hypotheses tested with no progress
- Fixes create new bugs
- Can't explain behavior theoretically
- Intermittent and can't reproduce reliably
- Working >30 minutes on same bug

---

## How They Work Together

### The Full Lifecycle (Greenfield Project)

```
User: "Build a recipe sharing app"
    ↓
┌─────────────────────────────────────────────────────┐
│ ORCHESTRATOR: Routes request, manages lifecycle     │
└─────────────────────────────────────────────────────┘
    │
    ├─► RESEARCH Phase (Steps 1-2)
    │   │
    │   ├─► Researcher (project mode)
    │   │       → .planning/research/STACK.md, FEATURES.md, ARCHITECTURE.md, PITFALLS.md
    │   │
    │   └─► Researcher (synthesize mode)
    │           → .planning/research/SUMMARY.md
    │
    ├─► ROADMAP Phase (Step 3)
    │   │
    │   └─► Planner (roadmap mode)
    │           → .planning/ROADMAP.md, REQUIREMENTS.md, STATE.md
    │           → Shows user roadmap, waits for approval
    │
    ├─► PER-PHASE Loop (Steps 4-8, repeated for each phase)
    │   │
    │   ├─► Researcher (phase mode)
    │   │       → .planning/phases/N/RESEARCH.md
    │   │
    │   ├─► Planner (plan mode)
    │   │       → .planning/phases/N/PLAN.md
    │   │
    │   ├─► Planner (validate mode)
    │   │       → Pass/fail with issues
    │   │       → If issues: Planner (revise mode) → re-validate
    │   │
    │   ├─► Coder + Designer (parallel if non-overlapping files)
    │   │       → Code implementation with per-task commits
    │   │       → .planning/phases/N/SUMMARY.md
    │   │
    │   ├─► Verifier (phase mode)
    │   │       → .planning/phases/N/VERIFICATION.md
    │   │       → If gaps: Gap-closure loop (max 3 iterations)
    │   │
    │   └─► If gaps persist after 3 loops: Report to user
    │
    ├─► INTEGRATION Phase (Step 9)
    │   │
    │   └─► Verifier (integration mode)
    │           → .planning/INTEGRATION.md
    │           → Checks cross-phase wiring, end-to-end flows
    │
    └─► COMPLETION (Step 10)
        │
        └─► Orchestrator compiles final report
                → What was built, decisions, verification status, how to run
```

### Specialized Workflows

**Bug Fixing:**
```
User: "Login is broken"
    ↓
Orchestrator → Debugger (find_and_fix)
    → Creates .planning/debug/BUG-[timestamp].md
    → Hypothesis testing with bias guards
    → Implements fix with verification
    → Updates debug file with root cause
```

**Quick Code Change:**
```
User: "Add dark mode toggle"
    ↓
Orchestrator → Coder (if logic)
           or → Designer (if UI-focused)
    → Direct implementation
    → Conventional commit
```

**Existing Codebase Analysis:**
```
User: "Analyze this project"
    ↓
Orchestrator → Researcher (codebase mode)
    → .planning/codebase/STACK.md
    → .planning/codebase/ARCHITECTURE.md
    → .planning/codebase/CONVENTIONS.md
    → .planning/codebase/CONCERNS.md
```

### Parallelization Rules

**Run in parallel when:**
- Tasks touch different files with no overlap
- Tasks are in different domains (styling vs logic)
- Tasks have no data dependencies

**Run sequentially when:**
- Task B needs output from Task A
- Tasks might modify the same file
- Design must be approved before implementation

**File Conflict Prevention:**
- Orchestrator explicitly scopes each agent to specific files
- Uses component boundaries for UI work
- Splits into sub-phases if overlap unavoidable

---

## Artifacts & Folder Structure

All agents write to `.planning/` for structured, traceable artifact management:

```
.planning/
├── REQUIREMENTS.md         # Requirements with REQ-IDs (Planner creates)
├── ROADMAP.md             # Phase breakdown (Planner creates)
├── STATE.md               # Project state tracking (Planner initializes, Coder updates)
├── INTEGRATION.md         # Cross-phase verification (Verifier creates)
│
├── research/              # Research outputs (Researcher creates)
│   ├── SUMMARY.md         #   Consolidated research (synthesize mode)
│   ├── STACK.md           #   Technology choices
│   ├── FEATURES.md        #   Feature analysis
│   ├── ARCHITECTURE.md    #   Architecture patterns
│   └── PITFALLS.md        #   Known pitfalls
│
├── codebase/              # Codebase analysis (Researcher codebase mode)
│   ├── STACK.md           #   Current stack inventory
│   ├── ARCHITECTURE.md    #   Current architecture
│   ├── STRUCTURE.md       #   Directory structure
│   ├── CONVENTIONS.md     #   Code conventions
│   ├── TESTING.md         #   Testing setup
│   ├── INTEGRATIONS.md    #   External integrations
│   └── CONCERNS.md        #   Tech debt and risks
│
├── phases/
│   ├── 1/
│   │   ├── RESEARCH.md    # Phase research (Researcher phase mode)
│   │   ├── PLAN.md        # Task plans (Planner plan mode)
│   │   ├── SUMMARY.md     # Execution summary (Coder)
│   │   └── VERIFICATION.md # Phase verification (Verifier phase mode)
│   ├── 2/
│   │   └── ...
│   └── N/
│
└── debug/                 # Debug session files (Debugger creates)
    ├── BUG-[timestamp].md
    └── ...
```

### Key Artifact Patterns

**Frontmatter YAML:**
Most planning artifacts use YAML frontmatter for structured metadata:
- Plans: `phase`, `plan`, `type`, `wave`, `dependencies`, `must_haves`
- Verifications: `phase`, `status`, `score`, `gaps`
- Debug files: `bug_id`, `status`, `created`, `updated`, `symptoms`, `root_cause`, `fix`

**Traceability:**
- Requirements have REQ-IDs
- Plans reference requirements
- Verifications check requirement coverage
- Summaries list commits
- Debug files are append-only evidence logs

**Context References:**
Plans use `@` notation to reference other artifacts:
```markdown
## Context
@.planning/phases/1/RESEARCH.md
@.planning/codebase/CONVENTIONS.md
```

---

## Prerequisites & Setup

### Required Tools

1. **Context7 MCP** (highly recommended)
   - Install: [Context7 MCP Extension](https://marketplace.visualstudio.com/items?itemName=Upstash.context7-mcp)
   - Provides up-to-date library/framework documentation
   - Used by Researcher, Planner, Coder, Designer, Debugger

2. **Git** (required for Coder)
   - Per-task commits with conventional commit format
   - Repository must be initialized before Coder runs

3. **VS Code or VS Code Insiders**
   - GitHub Copilot subscription active
   - Agent support enabled (generally available in Copilot)

### Optional Tools

- **GitHub MCP** — For GitHub integration (Coder uses if available)
- **Memory** — Experimental in VS Code Insiders (Orchestrator uses if available)

### Getting Started

1. **Install the agents** you need using the install badges above
2. **Initialize `.planning/` directory** in your project (agents will create subdirectories as needed)
3. **Initialize git** if not already: `git init`
4. **Start with Orchestrator** for complex work or invoke specialized agents directly for focused tasks

### Invocation Examples

**Start a new project:**
```
@orchestrator Build a recipe sharing app with user authentication
```

**Add a feature to existing project:**
```
@orchestrator Add real-time notifications using WebSockets
```

**Analyze existing codebase:**
```
@researcher Analyze this codebase — map the tech stack and architecture
```

**Create implementation plan:**
```
@planner Create a plan for the user authentication phase
```

**Implement a specific feature:**
```
@coder Execute the plan in .planning/phases/1/PLAN.md
```

**Fix a bug:**
```
@debugger Login returns 500 error when password is incorrect
```

**Verify phase completion:**
```
@verifier Verify Phase 1 implementation against success criteria
```

**Design UI:**
```
@designer Create a dark mode toggle component with smooth transitions
```

---

## Gotchas & Tips

### Memory in VS Code Insiders

The `memory` tool is experimental in VS Code Insiders. Orchestrator uses it if available but gracefully degrades if not present.

### Path Conventions

All agents use **relative paths** within `.planning/`. Never hardcode absolute paths in plans or artifacts — they break across different agent contexts.

### Commit Discipline

Coder **never** uses `git add .` — always stages files individually. This ensures atomic, reviewable commits per task.

### Verification is Independent

Verifier does NOT trust SUMMARY.md claims. It independently verifies everything with bash commands. This catches "tasks completed but goals not achieved" scenarios.

### Context Budget Management

Planner keeps plans under 50% of Coder's context budget (target: 2-3 tasks per plan, 5 max). This maintains execution quality.

### Hypothesis Testing Discipline

Debugger enforces a 3-test limit per hypothesis. If 3 tests don't resolve it, the hypothesis is too vague — refine or pivot.

### Designer Authority

Designer prioritizes UX over technical convenience. If a technical constraint harms user experience, Designer will push back. This is intentional.

### Parallelization Safety

Orchestrator explicitly scopes agents to specific files when delegating parallel work to prevent merge conflicts.

### Must-Haves Traceability

Plans derive `must_haves` goal-backward from phase success criteria. Verifier checks these independently. This ensures planning → execution → verification alignment.

---

## Advanced Usage

### Custom Request Routing

Orchestrator automatically determines routing, but you can specify:

```
@orchestrator Research options for real-time features, then create a plan (don't implement yet)
```

This triggers Steps 1-2 (research) and stops before execution.

### Gap-Closure Loop

When Verifier finds gaps after phase execution:

1. Verifier writes gaps to `VERIFICATION.md` frontmatter (structured YAML)
2. Orchestrator invokes Planner (gaps mode) to create fix plans
3. Orchestrator invokes Coder to execute fixes
4. Orchestrator invokes Verifier (re-verify mode)
5. Max 3 iterations — if gaps persist, escalates to user

### TDD Workflow

If Planner detects TDD setup or user mentions "test-first," plans use RED→GREEN→REFACTOR structure:
- RED: Write failing test → commit: `test: add failing test for [feature]`
- GREEN: Implement minimum code → commit: `feat: implement [feature]`
- REFACTOR: Clean up → commit: `refactor: clean up [feature]` (if changes made)

### Resuming Projects

STATE.md tracks project position. Orchestrator reads it to determine resume point:
- Research exists but no roadmap → resume at Step 3
- Roadmap exists but phase not started → resume at Step 4
- Phase plans exist but not validated → resume at Step 6
- Phase execution incomplete → resume at Step 7
- Phase complete but not verified → resume at Step 8

### Checkpoint Handling

Agents return structured checkpoints for:
- **human-verify** — Visual/manual checks (90% of checkpoints)
- **decision** — User must choose between options (9%)
- **human-action** — User must perform action (1%)
- **auth-gate** — Authentication required

Human provides input, agent resumes from checkpoint task.

---

## Philosophy

This agent system is built on these principles:

1. **Solo developer workflow** — No enterprise ceremony, no unnecessary meetings
2. **Goal-backward everything** — Start from desired end state, derive what must exist
3. **Verification is not optional** — Task completion ≠ goal achievement
4. **Context7 first** — Training data is stale, always verify against current docs
5. **WHAT not HOW** — Agents decide implementation, plans describe outcomes
6. **Fail loud and early** — Better to stop and ask than proceed with wrong assumptions
7. **Traceable artifacts** — Every decision, every gap, every commit documented
8. **Scientific debugging** — Hypothesis testing with bias guards, not heroic guessing
9. **Regenerable code** — Any file rewritable from its interface contract
10. **Atomic commits** — One task, one commit, fully reviewable

---

## Contributing

Found an issue or want to improve these agents? Contributions welcome!

---

## License

[Specify your license here]

---

**Built with ❤️ for developers who want AI agents that work like a senior engineering team.**
