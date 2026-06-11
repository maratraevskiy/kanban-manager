# Kanban Manager Skill

A Codex skill for managing project work with a filesystem-based Kanban board.

It helps the agent create and maintain a `.kanban/` directory with task folders organized by status:

```text
.kanban/01_backlog/
.kanban/02_progress/
.kanban/03_review/
.kanban/04_done/
```

## Install

### Option 1: CLI Install

Use `npx skills` to install the skill directly:

```bash
# Install all skills
npx skills add maratraevskiy/kanban-manager
```

This installs the skill into your `.agents/skills/` directory.

### Option 2: Clone and Copy

Clone the repo and copy the skill folder manually:

```bash
git clone https://github.com/maratraevskiy/kanban-manager.git
mkdir -p .agents/skills
cp -r kanban-manager/skills/kanban-manager .agents/skills/
```

## Usage

Try prompts like:

```text
Initialize the kanban board.
Create a task for adding OAuth login.
What is the status of my kanban tasks?
Move this task to review.
```

## License

MIT
