# COMPLETE TASK
Last updated: November 9, 2025, 14:26:53 CST

**Purpose:** Mark a task or its subtasks as completed.

## Core Behavior
1. Locate the task file by ID.
2. Update the `Status:` line → `Completed`.
3. Check off all `[ ]` subtasks as `[x]`.
4. Append an entry under `## Updates`:

```markdown
### {{DATE_TIME_CST}}
- ✅ Task completed successfully.
- Summary of what was achieved.
```

5. Update the top `Last updated:` timestamp.
6. Never delete or replace prior updates — always append.

## Confirmation Rules

Before marking a task complete:

1. Show the resolved file path.
2. Display the current `Status:` line (e.g., `Status: In Progress`).
3. List the subtasks that will be marked `[x]`.
4. Preview the completion update block, including the timestamp that will be used.
5. Ask explicitly: "Mark task <ID> as complete? (yes/no)"

If the task is already marked as `Completed`, require **double confirmation** before making any changes.

## Example Command
```text
Complete task 3.1
```
