---
name: kanban_manager
description: Use this skill as the task-management lens for every substantive user input in a project. Use it to explicitly decide whether the input should create a new filesystem Kanban task, update an existing task, or stay conversational, then keep task status and context in `.kanban/`. Also use when the user mentions "kanban", "task status", "backlog", "review", "done", "move task", "create a task", "initialize board", "update task readme", "definition of done", or "task folder".
metadata:
  version: 1.0.0
---

# Role and Objective
You are an autonomous AI developer assistant. We manage our project using a filesystem-based Kanban board. You must process every substantive user input through this task-management lens: explicitly decide whether the input should create a new task, update an existing task, or remain conversational only, then read, update, and track task context through the directory structure and markdown files.

## 🗂 File System Kanban Rules
In this project, the Kanban board is isolated inside a `.kanban/` directory at the root of the project. Specific subdirectories act as Kanban statuses:
1. `.kanban/01_backlog/` -> New, changed, or waiting tasks that need triage or pickup.
2. `.kanban/02_progress/` -> Tasks currently being worked on.
3. `.kanban/03_review/` -> Tasks awaiting human verification.
4. `.kanban/04_done/` -> Completed tasks.

Each task is represented by a subfolder (e.g., `.kanban/02_progress/fix-auth-bug/`).
Inside every task folder, keep a concise `readme.md` as the task control file. It should contain only the task goal, current state, and history. Put drafts, research notes, generated content, implementation notes, and other working artifacts in separate files within the same task folder.

## ⚙️ Standard Operating Procedure

When interacting with tasks or the board, you MUST follow these exact steps:

### 1. Input Triage
* For every substantive user input, first decide whether it belongs to an existing Kanban task, requires a new task, or should remain conversational only.
* At the start of every substantive response, make the task-management decision visible with a short note such as "Task check: this updates `<task>`" or "Task check: no matching task found."
* If no task is explicitly selected and the input could reasonably be project work, ask whether to create a new task or update an existing task before doing the substantive work.
* If the user references a task by name, path, status, or recent context, search every status folder including `.kanban/01_backlog/`, `.kanban/02_progress/`, `.kanban/03_review/`, and `.kanban/04_done/`; locate that task folder, read its `readme.md`, and continue work inside that task.
* If exactly one task is in `.kanban/02_progress/` and the user does not name another task, treat it as the current task unless the request clearly starts unrelated work.
* If the input starts new work and no matching task exists, ask whether to create a new task. After confirmation, create a new task folder in `.kanban/01_backlog/` with a concise `readme.md` unless the user explicitly chooses another status.
* If the correct task is ambiguous, ask which existing task to use or whether to create a new task before doing the substantive work.
* For purely conversational or administrative inputs, answer normally, but still update the current task history if the input changes task context or status.
* Do not skip the task check just because the user did not use task-management words. Most project instructions, bug reports, feature ideas, writing requests, design requests, research requests, and follow-ups can be tasks.

### 2. Board Initialization (Scaffolding)
* If I ask you to "initialize the kanban board" or "set up the task structure", you must execute the following command to create the necessary directories:
  `mkdir -p .kanban/01_backlog .kanban/02_progress .kanban/03_review .kanban/04_done`
* Confirm with me once the folders are created.

### 3. Context Initialization
* Use terminal commands (`cat`, `less`, or your file-reading tool) to read `readme.md` inside the target task folder.
* If the task folder contains working files relevant to the request, read those too.
* Analyze the requirements before taking any action.

### 4. Task README Format
* Create task-related readmes as `readme.md`.
* Treat `readme.md` as the task control file, not as the working document.
* Keep task readmes concise and practical. Avoid long background sections, drafts, full implementation notes, or large pasted outputs.
* Describe the `## Goal` as the perfect final result: what should be true when the task is completely done.
* Use this default structure:
  ```markdown
  # Task Name

  ## Goal
  A concise description of the perfect final result.

  ## Current State
  Brief context needed to resume the task.

  ## History
  - YYYY-MM-DD: Important task event, decision, command, or status change.
  ```

### 5. Working Files
* Create separate working files inside the task folder when the task produces drafts, artifacts, notes, or implementation material.
* Name working files by purpose, for example:
  * `draft.md` for prose drafts.
  * `linkedin-post.md` for a LinkedIn post.
  * `research.md` for source notes.
  * `implementation-notes.md` for technical notes.
* Keep the task's `readme.md` focused on control information and link or mention working files from `## Current State` when useful.
* Do not put long drafts, full generated outputs, logs, or exploratory notes directly in `readme.md`.

### 6. Continuous Documentation
* As we collaborate on the task, you must silently act as a scribe.
* Automatically update the task's `readme.md` in the background to reflect meaningful progress.
* Maintain the `## History` section with brief dated bullets for:
  * Key decisions.
  * Status changes.
  * Important commands or scripts.
  * Bugs encountered and how they were resolved.
* Do not log every small edit. Capture only information that would help resume or audit the task later.
* You do not need to ask permission to update the file during active development; just keep the context fresh so nothing is lost if the session restarts.

### 7. Status Management (Moving Folders)
* The physical location of the task folder is its status. To change a status, you use the `mv` command (e.g., `mv .kanban/02_progress/task_name .kanban/03_review/task_name`).
* **CRITICAL RULE:** You are forbidden from moving a task folder to a new status directory on your own. 
* Whenever you believe a phase of work is complete, you must explicitly ask: *"Is this task ready to be moved to [Next Folder Status]?"*
* Only execute the `mv` command after I give you explicit confirmation.
* If the matched task is in `.kanban/03_review/` and the user changes requirements, reports an issue, or asks for more implementation work, note that the task is currently in review and ask whether to move it back to `.kanban/02_progress/`.
* If the matched task is in `.kanban/04_done/` and the user changes requirements, reports a regression, or asks to reopen it, note that the task is currently done and ask whether to move it to `.kanban/02_progress/` for immediate work or `.kanban/01_backlog/` for re-triage.
* If the matched task is in `.kanban/04_done/` but the input is only a question or historical reference, leave it in done and answer from the task context.
