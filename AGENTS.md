# SDD Harness - Agent Bootstrap

## Project Overview

This is the **SDD Harness** - an Agent Development Framework running on Qoder IDE. It combines two powerful methodologies:

- **Superpowers** (git submodule: `superpowers/`) - Agentic skills framework & software development methodology
- **OpenSpec** (`.qoder/` + `openspec/`) - Spec-driven development (SDD) for AI coding assistants

## Core Philosophy

1. **Spec before code** - Agree on what to build before writing any code (OpenSpec)
2. **Skill-first execution** - Always check for matching skills before taking action (Superpowers)
3. **TDD mandatory** - RED-GREEN-REFACTOR: write failing test, watch it fail, write minimal code, watch it pass
4. **YAGNI ruthlessly** - You Aren't Gonna Need It - remove unnecessary features
5. **Evidence over claims** - Verify before declaring success

## Skill Loading Rules

Before ANY response or action (including clarifying questions), you MUST:
1. Check `superpowers/skills/` for matching Superpowers skills
2. Check `skills/` for Harness-specific extension skills
3. Check `.qoder/skills/` for OpenSpec workflow skills
4. Invoke matching skills BEFORE proceeding

### Superpowers Skills (in `superpowers/skills/`)

| Skill | When to Use |
|-------|-------------|
| `brainstorming` | Before ANY creative work - features, components, functionality changes |
| `writing-plans` | When you have an approved spec/design, before touching code |
| `subagent-driven-development` | When implementing from a plan - dispatches subagents per task |
| `executing-plans` | Alternative to subagent-driven - batch execution with checkpoints |
| `test-driven-development` | During implementation - enforces RED-GREEN-REFACTOR |
| `requesting-code-review` | Between tasks - reviews against plan |
| `receiving-code-review` | When receiving code review feedback |
| `using-git-worktrees` | After design approval - creates isolated workspace |
| `finishing-a-development-branch` | When tasks complete - merge/PR workflow |
| `systematic-debugging` | When debugging - 4-phase root cause process |
| `verification-before-completion` | Before declaring work done |
| `dispatching-parallel-agents` | For concurrent subagent workflows |
| `writing-skills` | When creating new skills |
| `using-superpowers` | Bootstrap - establishes how to find and use skills |

**CRITICAL**: If a skill might apply (even 1% chance), you MUST invoke it. This is not negotiable.

## OpenSpec Workflow

OpenSpec provides slash commands (located in `.qoder/commands/opsx/`) for spec-driven development:

```
/opsx:explore  ──►  /opsx:propose  ──►  /opsx:apply  ──►  /opsx:archive
   (optional          (draft plan,       (implement        (merge specs,
    thinking)          review it)         tasks)            file away)
```

### Command Details

| Command | Purpose |
|---------|---------|
| `/opsx:explore` | Think through ideas before committing - reads codebase, weighs options |
| `/opsx:propose <name>` | Create change with proposal.md, specs/, design.md, tasks.md |
| `/opsx:apply` | Implement tasks from the current change |
| `/opsx:sync` | Sync specs after implementation |
| `/opsx:archive` | Archive change, merge delta specs into main specs |
| `/opsx:update` | Refresh OpenSpec agent instructions |

## The Complete Development Cycle

1. **Explore** (`/opsx:explore`) - Understand what to build (optional but recommended)
2. **Brainstorm** (`superpowers:brainstorming`) - Refine ideas into design, save design doc
3. **Propose** (`/opsx:propose`) - Create OpenSpec change with all artifacts
4. **Plan** (`superpowers:writing-plans`) - Break into bite-sized TDD tasks
5. **Implement** (`/opsx:apply` + `superpowers:subagent-driven-development`) - Execute with TDD
6. **Review** (`superpowers:requesting-code-review`) - Review against plan
7. **Archive** (`/opsx:archive`) - Merge specs, clean up

### Workflow Integration Rules

- **Always brainstorm first** - Use `superpowers/brainstorming` before `/opsx:propose`
- **Design docs** are saved to `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`
- **Plans** are saved to `docs/superpowers/plans/YYYY-MM-DD-<feature>.md`
- **OpenSpec changes** live in `openspec/changes/<change-name>/`
- After brainstorming, use `/opsx:propose` to create the formal OpenSpec change
- `/opsx:apply` drives implementation; wrap it with Superpowers execution skills

## Directory Structure

```
.
├── .qoder/                  # Qoder IDE integration (OpenSpec commands & skills)
│   ├── commands/opsx/       # Slash commands: explore, propose, apply, archive, sync, update
│   └── skills/              # OpenSpec skills for Qoder
├── openspec/                # OpenSpec SDD root
│   ├── specs/               # Source of truth (system behavior)
│   ├── changes/             # Proposed changes (one folder per change)
│   └── config.yaml          # OpenSpec configuration
├── superpowers/             # Git submodule: obra/superpowers
│   └── skills/              # 14 Superpowers methodology skills
├── skills/                  # Harness-specific extension skills
├── src/                     # Harness source code
├── tests/                   # Test suite
├── docs/                    # Project documentation
│   └── superpowers/         # Superpowers-generated artifacts
│       ├── specs/           # Design documents
│       └── plans/           # Implementation plans
├── AGENTS.md                # This file - agent bootstrap
├── package.json             # Node.js project configuration
└── .gitignore               # Git ignore rules
```

## Key Constraints

- Node.js >= 20.19.0
- OpenSpec CLI: `npm install -g @fission-ai/openspec@latest`
- Superpowers: managed as git submodule, update with `git submodule update --remote superpowers`
- Telemetry disabled by default (see .gitignore)
