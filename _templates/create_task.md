# CREATE TASK
Last updated: November 9, 2025, 14:20:02 CST

**Purpose:** Initialize a new task in the active project workspace.

## Core Behavior
1. Always confirm the project and target directory (`/tasks/`) before creating a file.
2. Use `_templates/task_base.md` as the source.
3. Replace placeholders:
   - `{{TASK_ID}}` → e.g. `3.1`
   - `{{TASK_TITLE}}` → short, kebab-case title (e.g. `session-history-loop`)
   - `{{DATE_TIME_CST}}` → current timestamp.

### Filename Sanitization Rules
When generating the task filename:

- Convert the title to lowercase.
- Replace spaces and special characters with hyphens (`-`).
- Remove or normalize characters that are not safe for filenames.
- Keep the total filename (excluding the directory) under ~50 characters when possible.
- Use the pattern:
  `task-<ID>-<sanitized-title>.md`
- Before creating the file, show the generated filename and ask for confirmation.

4. Create a new markdown file at:
   `/tasks/task-<id>-<title>.md`

## Confirmation Rules
- If the file already exists, Gemini **must ask twice** before overwriting.
- On confirmation, append `_v2` or `_updated` to preserve previous history if needed.

## Example

```text
Command: Create a new task 3.1 — Implement session history loop
File: tasks/task-3.1-implement-session-history-loop.md
```

### Output Structure (example)
```markdown
# Task 3.1 — Implement Session History Loop
Status: In Progress
Last updated: 2025-11-09 14:10 CST
...
```

### Notes
- Ensure correct timestamp format (CST).
- Never create tasks outside the /tasks/ folder.
- Always echo a confirmation summary before file creation.