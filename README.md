# Kanban Manager Skill

A Codex skill for managing project work with a filesystem-based Kanban board.

The skill teaches Codex to create and maintain a `.kanban/` directory with task folders organized by status:

- `.kanban/01_backlog/`
- `.kanban/02_progress/`
- `.kanban/03_review/`
- `.kanban/04_done/`

Each task lives in its own folder and contains a concise `readme.md` describing the perfect final result, the current state, and the task history.

## Install

Install for your Codex user profile:

```bash
mkdir -p ~/.codex/skills
cp -R skills/kanban-manager ~/.codex/skills/kanban-manager
```

Or install only for a specific project:

```bash
mkdir -p .agents/skills
cp -R skills/kanban-manager .agents/skills/kanban-manager
```

Restart Codex after installing so the skill is picked up.

## Install From GitHub

Codex can also install this skill directly from GitHub:

```bash
install-skill-from-github.py --repo maratraevskiy/kanban-manager --path skills/kanban-manager
```

If your Codex environment exposes the built-in skill installer, ask Codex:

```text
Install the skill from github.com/maratraevskiy/kanban-manager/tree/main/skills/kanban-manager
```

## Usage

Example prompts:

```text
Initialize the kanban board.
Create a task for adding OAuth login.
What is the status of my kanban tasks?
Move this task to review.
```

When working on a task, the skill keeps the task `readme.md` updated with concise history entries and asks before moving task folders between Kanban statuses.

## Task README Format

Task readmes are intentionally short and resumable:

```markdown
# Task Name

## Goal
A concise description of the perfect final result.

## Current State
Brief context needed to resume the task.

## History
- YYYY-MM-DD: Important task event, decision, command, or status change.
```

The skill maintains the `## History` section as work progresses, recording meaningful decisions, status changes, important commands, and resolved issues without logging every small edit.

## Working Files

Keep `readme.md` as the task control file only: goal, current state, and history.

Put drafts, research notes, generated content, implementation notes, and other artifacts in separate files inside the same task folder, for example:

- `linkedin-post.md`
- `draft.md`
- `research.md`
- `implementation-notes.md`

## License

MIT
