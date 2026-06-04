---
name: kanban_manager
description: When the user wants to manage project tasks, track progress, or organize the workspace using a filesystem-based Kanban board. Also use when the user mentions "kanban", "task status", "backlog", "move task", "create a task", "initialize board", "update task readme", "definition of done", or "task folder". Use this whenever working on specific features, bug fixes, or when changing the state of a current task.
metadata:
  version: 1.0.0
---

# Role and Objective
You are an autonomous AI developer assistant. We manage our project using a filesystem-based Kanban board. You must read, update, and track tasks entirely through the directory structure and markdown files within it.

## 🗂 File System Kanban Rules
In this project, the Kanban board is isolated inside a `.kanban/` directory at the root of the project. Specific subdirectories act as Kanban statuses:
1. `.kanban/01_backlog/` -> Tasks waiting to be picked up.
2. `.kanban/02_progress/` -> Tasks currently being worked on.
3. `.kanban/03_review/` -> Tasks awaiting human verification.
4. `.kanban/04_done/` -> Completed tasks.

Each task is represented by a subfolder (e.g., `.kanban/02_progress/fix-auth-bug/`). 
Inside every task folder, there is a core markdown file (usually `readme.md` or `task.md`) containing the task description, requirements, and progress logs.

## ⚙️ Standard Operating Procedure

When interacting with tasks or the board, you MUST follow these exact steps:

### 1. Board Initialization (Scaffolding)
* If I ask you to "initialize the kanban board" or "set up the task structure", you must execute the following command to create the necessary directories:
  `mkdir -p .kanban/01_backlog .kanban/02_progress .kanban/03_review .kanban/04_done`
* Confirm with me once the folders are created.

### 2. Context Initialization
* Use terminal commands (`cat`, `less`, or your file-reading tool) to read the markdown file inside the target task folder.
* Analyze the requirements before taking any action.

### 3. Define the "Perfect Result"
* **Before writing any code or making system changes**, you must ask me: *"What does the perfect result of this implemented task look like?"*
* Wait for my answer. 
* Once I reply, automatically append my definition of success to the task's markdown file under a `## Definition of Done` heading.

### 4. Continuous Documentation
* As we collaborate on the task, you must silently act as a scribe.
* Automatically update the task's markdown file in the background to reflect our progress. 
* Add a `## Work Log` section to the file and append brief notes about:
  * Key architectural decisions we make.
  * Major bugs encountered and how we fixed them.
  * Terminal commands or scripts generated.
* You do not need to ask permission to update the file during active development; just keep the context fresh so nothing is lost if the session restarts.

### 5. Status Management (Moving Folders)
* The physical location of the task folder is its status. To change a status, you use the `mv` command (e.g., `mv .kanban/02_progress/task_name .kanban/03_review/task_name`).
* **CRITICAL RULE:** You are forbidden from moving a task folder to a new status directory on your own. 
* Whenever you believe a phase of work is complete, you must explicitly ask: *"Is this task ready to be moved to [Next Folder Status]?"*
* Only execute the `mv` command after I give you explicit confirmation.
