# JP Agents Workspace Setup

## What Was Fixed

The Orchestrator agent was using incorrect lowercase agent names (`researcher`, `planner`, `coder`, etc.) when calling the `runSubagent` tool.

**The fix:** Updated all `runSubagent` calls throughout the Orchestrator to use the correct capitalized agent names that match the actual agent definitions:
- `Researcher` (not `researcher`)
- `Planner` (not `planner`)
- `Coder` (not `coder`)
- `Designer` (not `designer`)
- `Verifier` (not `verifier`)
- `Debugger` (not `debugger`)

## How It Works Now

When you use the Orchestrator agent, it will:

1. **Receive your request** (e.g., "Build a recipe sharing app")
2. **Call runSubagent** with the appropriate agent name and prompt
3. **Wait for the subagent** to complete its work (research, planning, coding, etc.)
4. **Coordinate the workflow** through all phases

## Agent Roles

| Agent | Role | Tools |
|---|---|---|
| **Orchestrator** | Coordinates workflow, delegates to others | read, agent, memory |
| **Researcher** | Investigates tech stacks, patterns, docs | Full toolkit + Context7 + web |
| **Planner** | Creates roadmaps and task plans | Full toolkit + Context7 + web |
| **Coder** | Implements code, commits changes | Full toolkit + Context7 + GitHub |
| **Designer** | UI/UX design and styling | Full toolkit |
| **Verifier** | Validates work against goals | Full toolkit |
| **Debugger** | Scientific debugging | Full toolkit |

## Example Usage

Instead of manually calling each agent, you now invoke the Orchestrator:

```
User: "Build a recipe sharing app"

Orchestrator will:
├─ runSubagent(Researcher, "Project mode. Research recipe sharing...")
├─ runSubagent(Planner, "Roadmap mode. Create phased roadmap...")
├─ runSubagent(Coder, "Execute Phase 1 plan...")
├─ runSubagent(Verifier, "Verify Phase 1...")
└─ ... continue through all phases
```

## Key Changes Made

1. **Agent Naming**: All agent names must be capitalized (`Researcher`, `Planner`, `Coder`, etc.)
2. **Agent Invocation**: Use `runSubagent(AgentName, "prompt")` with capitalized names
3. **All delegation examples**: Updated throughout the Orchestrator instructions
4. **Parallel execution**: Now uses `runSubagent(Coder, ...)` + `runSubagent(Designer, ...)` properly

## How to Use

1. **Invoke Orchestrator**: Use `@Orchestrator` in Copilot Chat
2. **Describe your goal**: "Build a [type of app]" or "Add [feature]"
3. **Let it orchestrate**: The Orchestrator will automatically call the right subagents
4. **Review outputs**: Check `.planning/` directory for all generated artifacts

## Artifacts Structure

```
.planning/
├── REQUIREMENTS.md         # All requirements with IDs
├── ROADMAP.md              # Phase breakdown
├── STATE.md                # Current progress
├── research/
│   ├── SUMMARY.md          # Consolidated research
│   ├── STACK.md            # Tech stack decisions
│   ├── FEATURES.md         # Feature analysis
│   ├── ARCHITECTURE.md     # Architecture patterns
│   └── PITFALLS.md         # Known pitfalls
└── phases/
    ├── 1/
    │   ├── RESEARCH.md     # Phase-specific research
    │   ├── PLAN.md         # Task-level plan
    │   ├── SUMMARY.md      # What was built
    │   └── VERIFICATION.md # Verification results
    └── 2/
        └── ...
```

## The Full Workflow

```
User Request
    ↓
Orchestrator (coordinates)
    ↓
├─ Step 1: Researcher (project mode) → tech stack, architecture
├─ Step 2: Researcher (synthesize) → SUMMARY.md
├─ Step 3: Planner (roadmap) → ROADMAP.md, REQUIREMENTS.md
│
│  For each phase:
├─ Step 4: Researcher (phase mode) → implementation details
├─ Step 5: Planner (plan mode) → task plans
├─ Step 6: Planner (validate) → verify plans
├─ Step 7: Coder + Designer (execute) → implement + commit
├─ Step 8: Verifier (verify) → check success criteria
│
├─ Step 9: Verifier (integration) → cross-phase checks
└─ Step 10: Report to user
```

## Troubleshooting

****Agent name mismatch**: Ensure you use capitalized agent names: `Researcher`, `Planner`, `Coder`, `Designer`, `Verifier`, `Debugger`
- Check that agent files are in `.github/agents/` directory
- Verify frontmatter `name:` matches the agent name exactly (capitalized)
- Ensure Orchestrator is calling `runSubagent` with proper capitalization
- Ensure Orchestrator is calling `runSubagent` (not `@mentions`)

**Problem: Agents can't edit files**
- Verify each agent has `edit` in their `tools:` list
- Check that the agent has `vscode` tool access
- Ensure Orchestrator is delegating, not implementing

**Problem: Context overflow**
- Plans might be too large (target 2-3 tasks per plan)
- Split phases into smaller sub-phases
- Use more granular delegation

## Direct Agent Use

You can also call agents directly for specific tasks:

- `@researcher` - Research a technology or pattern
- `@planner` - Create a plan for a feature
- `@coder` - Implement a specific change
- `@designer` - Design UI components
- `@verifier` - Verify work was completed
- `@debugger` - Debug an issue

But for **complex multi-phase projects**, always use `@Orchestrator` to coordinate.
