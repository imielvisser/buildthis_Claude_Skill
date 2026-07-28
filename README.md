# /buildthis - Autonomous Project Orchestrator for Claude

A single skill file that turns Claude into a full project manager. One command decomposes a plan, spins up parallel sub-agents in isolated git worktrees, runs QA, tracks costs, and delivers a tabbed HTML report.

## What It Does

`/buildthis` runs an eight-stage pipeline:

1. **Intake** - Classifies your input (file, folder, URL, or inline text) and normalizes it into a canonical plan
2. **Assessment** - Reads the plan and repo, flags risks, detects environment, identifies spec gaps
3. **Onboarding** - Asks targeted steering questions: budget tier, parallelism, design direction, target environment
4. **Decomposition** - Breaks the plan into phases and tasks with acceptance criteria, test parameters, and blockers
5. **Build loop** - Dispatches sub-agents in parallel, each in its own isolated git worktree
6. **Phase gate** - Runs QA on every task, merges passing work, cleans up worktrees, verifies zero artifacts remain
7. **Master review** - Scores confidence across five dimensions with itemized deductions, runs a final fix pass
8. **Report** - Generates a self-contained tabbed HTML file and opens it in your browser

## Key Features

- **Worktree isolation** - Each concurrent task gets its own git worktree, preventing agent collisions
- **Strict state machine** - 10 states with defined transitions, survives session drops and context resets
- **Three-tier escalation** - Builder agents, Advisor agents, and the Orchestrator, each with a defined role
- **Budget tiers** - Economy, Business, and First Class model configurations for different cost/quality tradeoffs
- **Sensitivity profiles** - Standard (dev), Elevated (stage), Maximum (production) with increasing safeguards
- **Cost tracking** - Per-phase token usage and estimated USD in `Build/cost.json`
- **Design bar** - Awwwards-premium default for all UI work; generic output is treated as a QA failure
- **Resumable builds** - `Build/tasks.json` persists state so interrupted builds can resume cleanly

## Install

**As a slash command (recommended):**

```bash
# Per project
cp SKILL.md .claude/commands/buildthis.md

# Global (all projects)
cp SKILL.md ~/.claude/commands/buildthis.md
```

**As an auto-triggering skill:**

```bash
mkdir -p .claude/skills/buildthis
cp SKILL.md .claude/skills/buildthis/SKILL.md
```

## Usage

```
/buildthis project_plan.md
/buildthis Docs/scope/
/buildthis add OAuth login with Google and GitHub
/buildthis https://docs.example.com/prd
```

Or just say "buildthis: add dark mode" in conversation.

## Requirements

- Claude Code or Claude Desktop with skills support
- No external dependencies

## License

MIT

## Author

Built by [Imiel Visser](https://imiel.dev) ([@imiel_visser](https://x.com/imiel_visser))

Read the full breakdown: [I Built a Skill That Turns Claude Into a Project Manager](https://imiel.dev/blog/buildthis-autonomous-project-orchestrator-2026-guide)
