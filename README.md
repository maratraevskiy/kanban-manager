# Kanban Manager Skill

A Codex skill for managing project work with a filesystem-based Kanban board.

The skill teaches Codex to create and maintain a `.kanban/` directory with task folders organized by status:

- `.kanban/01_backlog/`
- `.kanban/02_progress/`
- `.kanban/03_review/`
- `.kanban/04_done/`

Each task lives in its own folder and contains a markdown file such as `readme.md` or `task.md` with the task description, requirements, definition of done, and work log.

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

When working on a task, the skill asks for the desired definition of done before code changes, keeps the task markdown updated with a work log, and asks before moving task folders between Kanban statuses.

## License

MIT
