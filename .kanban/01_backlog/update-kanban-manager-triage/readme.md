# Update Kanban Manager Triage

## Goal
The kanban manager skill reliably asks about task creation or updates for every substantive input, and handles changed work from review or done tasks by suggesting progress or backlog as appropriate.

## Current State
Patched `skills/kanban-manager/SKILL.md` and aligned `README.md`; install docs now include skills.sh plus a manual sparse-clone fallback, and backlog remains the triage status.

## History
- 2026-06-09: Created task for improving triage and review/done task handling.
- 2026-06-09: Added explicit task checks, review/done reopening guidance, and README alignment.
- 2026-06-09: Confirmed backlog is the only triage/waiting status.
- 2026-06-09: Replaced multiple install options with one project-agent-folder sparse-clone install flow.
- 2026-06-09: Added skills.sh install command and kept sparse clone as the manual fallback.
