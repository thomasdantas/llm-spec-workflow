# llm-spec-workflow

A spec-driven workflow kit for building software with LLM agents. It turns vague feature requests into structured PRDs, technical specs, and numbered tasks — then guides agents through implementation, code review, QA, and bugfixing in a repeatable pipeline.

## Overview

This repository is **not an application**. It is a collection of markdown templates, agent commands, and conventions that any project can adopt to get disciplined, spec-first development out of LLM coding agents (Claude Code, Cursor, Codex, etc.).

The core idea is simple: **Spec before code.** Every feature goes through a structured pipeline that produces traceable artifacts at each stage, so nothing is lost between "what the user wants" and "what the agent builds."

### Pipeline at a glance

```
Feature Request
      │
      ▼
┌─────────────┐     ┌──────────────────┐     ┌──────────────┐
│  Create PRD  │────▶│ Create Tech Spec │────▶│ Create Tasks │
└─────────────┘     └──────────────────┘     └──────────────┘
                                                     │
                          ┌──────────────────────────┘
                          ▼
                   ┌──────────────┐
                   │ Execute Task │──┐
                   └──────────────┘  │
                          │          │ (loop per task)
                          ▼          │
                   ┌──────────────┐  │
                   │   Review     │──┘
                   └──────────────┘
                          │
                          ▼
                   ┌──────────────┐     ┌──────────────┐
                   │      QA      │────▶│   Bugfix     │
                   └──────────────┘     └──────────────┘
```

## Workflow

### Phase 1 — Create PRD (`create-prd`)

An agent captures product intent by asking clarifying questions, then drafts a **Product Requirements Document** using the standardized template. The PRD covers goals, user stories, features, UX considerations, and explicit out-of-scope items.

**Output:** `tasks/prd-<feature-name>/prd.md`

### Phase 2 — Create Tech Spec (`create-techspec`)

Starting from the PRD and a deep analysis of the existing codebase, the agent produces a **Technical Specification** focused on _how_ to build (architecture, interfaces, data models, APIs, testing strategy, build order) — not _what_ to build.

**Output:** `tasks/prd-<feature-name>/techspec.md`

### Phase 3 — Create Tasks (`create-tasks`)

The agent breaks the PRD + Tech Spec into numbered, independently completable tasks. A high-level task list is shown for **human approval** before any files are generated. Each task gets its own markdown file with subtasks, success criteria, and test requirements.

**Output:** `tasks/prd-<feature-name>/tasks.md` and `tasks/prd-<feature-name>/<num>_task.md`

### Phase 4 — Execute Task (`execute-task`)

The agent picks the next uncompleted task, reads all context (PRD, Tech Spec, task file), plans the approach, runs the task reviewer agent, and then **implements the code**. This phase loops until all tasks are done.

**Output:** Working code committed to the project.

### Phase 5 — Code Review (`execute-review`)

A review pass that analyzes git diffs, verifies rules compliance, checks Tech Spec adherence, runs the test suite, and produces a structured **Code Review Report** with an approval status.

**Output:** Code Review Report (APPROVED / APPROVED WITH RESERVATIONS / REJECTED).

### Phase 6 — QA (`execute-qa`)

Quality assurance driven by PRD requirement IDs. The agent uses Playwright MCP tools for E2E testing, accessibility checks, and visual validation. Any bugs found are documented in `bugs.md`.

**Output:** QA Report and `tasks/prd-<feature-name>/bugs.md`.

### Phase 7 — Bugfix (`execute-bugfix`)

The agent reads `bugs.md`, plans fixes per bug, implements them with regression tests, validates UI bugs via Playwright, runs the full test suite, and updates the bug tracker.

**Output:** Bugfix Report and updated `bugs.md`.

## Project Structure

```
llm-spec-workflow/
├── README.md                  # This file
├── AGENTS.md                  # Agent directives (all providers)
├── CLAUDE.md                  # Agent directives (Claude-specific)
│
├── docs/
│   └── prompt.md              # Placeholder for agent reference prompt
│
├── templates/                 # Blank templates used by commands
│   ├── prd-template.md        # PRD structure
│   ├── techspec-template.md   # Tech Spec structure
│   ├── tasks-template.md      # Task list structure
│   └── task-template.md       # Individual task structure
│
├── tasks/                     # Living spec artifacts (per-feature folders)
│   ├── prd.md                 # Sample PRD starter
│   ├── techspec.md            # Sample Tech Spec starter
│   ├── tasks.md               # Sample task list starter
│   └── x_task.md              # Sample individual task starter
│
└── .claude/
    ├── commands/              # Workflow command definitions
    │   ├── create-prd.md      # Phase 1: PRD creation
    │   ├── create-techspec.md # Phase 2: Tech Spec creation
    │   ├── create-tasks.md    # Phase 3: Task breakdown
    │   ├── execute-task.md    # Phase 4: Task implementation
    │   ├── execute-review.md  # Phase 5: Code review
    │   ├── execute-qa.md      # Phase 6: QA validation
    │   └── execute-bugfix.md  # Phase 7: Bug fixing
    │
    ├── agents/                # Agent definitions
    │   └── task-reviewer.md   # Task reviewer agent (placeholder)
    │
    └── skills/                # Reusable agent skills
        └── skills-best-practices/
            ├── SKILL.md       # Meta-skill for authoring other skills
            ├── assets/        # Skill template files
            ├── references/    # Validation checklists
            └── scripts/       # Metadata validation scripts
```

## Directory Reference

### `templates/`

Blank, fill-in-the-blank markdown templates that commands use as the canonical structure for each artifact. They define _what sections_ a PRD, Tech Spec, or task file must contain — agents copy them and fill in the content.

| Template               | Purpose                                                                  |
| ---------------------- | ------------------------------------------------------------------------ |
| `prd-template.md`      | Overview, goals, user stories, features, UX, out of scope                |
| `techspec-template.md` | Architecture, interfaces, data models, APIs, testing, build order, risks |
| `tasks-template.md`    | Numbered checkbox list of tasks                                          |
| `task-template.md`     | Per-task doc with requirements, subtasks, success criteria, tests        |

### `tasks/`

Where generated spec artifacts live. When a command runs, it creates a **per-feature folder** following the convention `tasks/prd-<feature-name>/` containing:

- `prd.md` — The filled PRD
- `techspec.md` — The filled Tech Spec
- `tasks.md` — The task checklist
- `<num>_task.md` — Individual task files (e.g. `1_task.md`, `2_task.md`)
- `bugs.md` — Bug tracker (created during QA)

The files at the root of `tasks/` are starter samples for reference.

### `.claude/commands/`

Procedural command definitions that tell the agent exactly what role to assume, what files to read, what steps to follow, and what output to produce. Each command maps to one phase of the workflow pipeline. They are designed for Claude Code slash commands but the patterns are portable to other agent frameworks.

### `.claude/agents/`

Definitions for specialized sub-agents that can be invoked by commands. Currently contains a placeholder for a **task reviewer** agent that validates task plans before implementation begins.

### `.claude/skills/`

Reusable skill modules following the [agentskills.io](https://agentskills.io) convention. Skills provide domain-specific knowledge and procedures that agents can activate when a task touches their area. The included `skills-best-practices` is a meta-skill that teaches agents how to author new skills.

### `docs/`

Supplementary documentation and reference material for agents. Currently a placeholder for a custom agent prompt.

### `AGENTS.md`

Agent behavior guide compatible with all LLM providers (Cursor, Codex, Copilot, etc.). Defines priorities, recommended stack, project structure conventions, git safety rules, and anti-patterns to avoid.

### `CLAUDE.md`

Claude-specific agent directives. Covers pre-work steps (read the project before acting), code quality expectations, and edit safety rules (re-read before editing, limit batch edits).

## How to Use

1. **Copy this repo** into your project (or use it as a template).
2. **Customize** `AGENTS.md` and `CLAUDE.md` with your project's stack, conventions, and rules.
3. **Add your own rules** to `.claude/rules/` for project-specific standards.
4. **Add skills** to `.claude/skills/` for domain-specific agent knowledge.
5. **Run the pipeline** — start with `create-prd` for a new feature and follow the phases in order.

Each command is self-contained: it tells the agent what role to play, what files to read, and what to produce. Human approval is required at key checkpoints (task list approval, code review status).
