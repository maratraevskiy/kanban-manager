# Kanban Manager Skill

A Codex skill for managing project work with a filesystem-based Kanban board.

It helps the agent create and maintain one `.kanban/` directory at the level-1 workspace root, with task folders organized by status:

```text
.kanban/01_backlog/
.kanban/02_progress/
.kanban/03_review/
.kanban/04_done/
```

The board should not be nested inside a repository, app, package, or other subfolder.

## Install

### Option 1: CLI Install

Use `npx skills` to install the skill directly:

```bash
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
Yes, create the task, but wait for my explicit approval before implementing it.
Yes, help me brainstorm the implementation details.
For this task, keep separate implementation docs.
Plan the implementation for adding OAuth login.
What is the status of my kanban tasks?
Move this task to review.
```

After creating a task, the skill can offer a one-question-at-a-time brainstorming flow and compile the answers into `implementation-spec.md`.

After creating a task, the skill waits for explicit user consent before implementing that task, even if plans or specs already exist.

When asked, the skill keeps implementation details in separate task files such as `initial-implementation-plan.md`, `updates-plan.md`, and `final-implementation.md` while leaving `readme.md` as the concise task control file.

In Plan Mode, planning prompts include the Kanban task action: create a new task with `initial-implementation-plan.md` when no task exists, or update the matching task with `updates-plan.md`.

## License

MIT
