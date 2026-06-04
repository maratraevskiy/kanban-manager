# Kanban Manager Skill

A Codex skill for managing project work with a filesystem-based Kanban board.

The skill teaches Codex to create and maintain a `.kanban/` directory with task folders organized by status:

- `.kanban/01_backlog/`
- `.kanban/02_progress/`
- `.kanban/03_review/`
- `.kanban/04_done/`

Each task lives in its own folder and contains a concise `readme.md` describing the perfect final result, the current state, and the task history.

## Install

You can install this skill globally for every project or locally for one project.

### Step 1. Clone This Repository

Choose a place where you keep downloaded tools, then clone the repo:

```bash
mkdir -p ~/Developer
cd ~/Developer
git clone https://github.com/maratraevskiy/kanban-manager.git
cd kanban-manager
```

### Step 2A. Install Globally For Codex

Use this if you want the skill available in Codex across your projects:

```bash
cd ~/Developer/kanban-manager
mkdir -p ~/.codex/skills
cp -R skills/kanban-manager ~/.codex/skills/kanban-manager
```

Restart Codex after installing so the skill is picked up.

### Step 2B. Install Globally For Claude

Use this if you want the skill available in Claude Code across your projects:

```bash
cd ~/Developer/kanban-manager
mkdir -p ~/.claude/skills
cp -R skills/kanban-manager ~/.claude/skills/kanban-manager
```

Claude Code watches existing skill directories for changes. Restart Claude Code if `~/.claude/skills` did not exist when the session started.

### Step 2C. Install Locally For One Project

Use this if you want the skill available only inside one project.

First, go to your project folder:

```bash
cd /path/to/your/project
```

For Codex:

```bash
mkdir -p .agents/skills
cp -R ~/Developer/kanban-manager/skills/kanban-manager .agents/skills/kanban-manager
```

For Claude Code:

```bash
mkdir -p .claude/skills
cp -R ~/Developer/kanban-manager/skills/kanban-manager .claude/skills/kanban-manager
```

### Updating An Existing Install

Go to the cloned repository and pull the latest version:

```bash
cd ~/Developer/kanban-manager
git pull
```

Then copy the skill folder again to the same destination you used before.

### Troubleshooting

If you see this error:

```text
cp: skills/kanban-manager: No such file or directory
```

You are probably not inside the cloned repository. Run:

```bash
cd ~/Developer/kanban-manager
```

Then run the install command again.

### Uninstall

Remove the installed skill folder.

For Codex global install:

```bash
rm -rf ~/.codex/skills/kanban-manager
```

For Claude global install:

```bash
rm -rf ~/.claude/skills/kanban-manager
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
