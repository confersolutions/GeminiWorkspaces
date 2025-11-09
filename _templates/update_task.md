# UPDATE TASK
Last updated: November 9, 2025, 14:26:53 CST

**Purpose:** Append a dated progress update to an existing task file.

## Core Behavior
1. Identify the task file by its ID (e.g., `task-3.1-...md`).
2. Append a new section under the `## Updates` heading.

### Insert Block Format
```markdown
### {{DATE_TIME_CST}}
- Summary of progress made.
- Key decisions or discoveries.
- Remaining blockers (if any).
```

3. Do **not** rewrite or reformat the rest of the file.
4. Update the top-level `Last updated:` timestamp to the same date/time.

Note: `UPDATE TASK` always writes under the `## Updates` section.
Treat these entries as user-visible progress logs (what moved forward, what changed).

## Confirmation Rules

Before applying an update:

1. Show the resolved file path for the task.
2. Confirm that the update will be added under the `## Updates` section.
3. Preview the new update block that will be appended (including timestamp and bullet points).
4. Ask explicitly: "Apply this update to task <ID>? (yes/no)"

If the task file cannot be found:
- Offer to create it from `_templates/task_base.md`, but only after explicit user confirmation.

## Example Command
```text
Update task 3.1 with progress made on session memory logic.
```
