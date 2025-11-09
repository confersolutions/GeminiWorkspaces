# Actions Index
Last updated: November 9, 2025, 14:26:53 CST

This file serves as the lookup table for all standard Gemini workspace actions.  
When an action command is issued (e.g., “CREATE TASK” or “STORE HISTORY”), Gemini uses this file to locate the appropriate guide in `_templates/` and follow it exactly.

## Available Actions

| Action | Purpose | Guide File | Typical Prompt |
|---------|----------|-------------|----------------|
| **CREATE TASK** | Initialize a new task from `_templates/task_base.md`. | `_templates/create_task.md` | “Create a new task 3.1 — Implement session history loop.” |
| **UPDATE TASK** | Add a progress update to an existing task. | `_templates/update_task.md` | “Update task 3.1 with progress made today.” |
| **COMPLETE TASK** | Mark a task or subtasks as done. | `_templates/complete_task.md` | “Complete task 3.1.” |
| **STORE CONTEXT / STORE HISTORY** | Append reasoning and summary of the current chat session. | `_templates/store_context.md` | “STORE HISTORY for task 3.1.” |

## Rules for Gemini

1. Always consult this file first to find which guide applies to the given command.  
2. Follow the linked `.md` file’s instructions exactly — including confirmation steps and timestamp rules.  
3. Never guess or infer the right guide by scanning filenames. This file is the single source of truth.  
4. When new command guides are created under `_templates/`, update this file accordingly.  
   - Gemini should offer a reminder after any new `_templates/*.md` file is created.  
   - Update the **Available Actions** table to include new actions and their typical prompts.

## Dry Run & Validation

To keep this workspace safe and auditable, actions should support:

- **Dry Run Mode (optional):**
  - When requested (e.g., “CREATE TASK 3.1 … — dry run”), Gemini:
    1. Resolves the target file(s).
    2. Shows exactly what it *would* write or change.
    3. Does **not** actually write to disk until I confirm.

## Validation Checks (Workspace Health)

When running `VALIDATE WORKSPACE`, Gemini should:

1. **Structural checks**
   - Verify all task files have required sections: `Objective`, `Subtasks`, `Updates`, and `Session History`.
   - Ensure the `Status:` field is one of: `In Progress`, `Completed`, `Blocked`, or `On Hold`.

2. **Consistency checks**
   - Detect duplicate task IDs within the same project.
   - Confirm checkbox syntax is valid: `[ ]` or `[x]`.
   - Validate that timestamps follow the format: `YYYY-MM-DD HH:MM:SS CST`.

3. **Orphan detection**
   - List any task files in `/tasks/` that are not referenced in the project’s main `<Project>.md` file.

4. **Output**
   - Produce a concise summary of issues found.
   - Suggest non-destructive fixes where possible.
   - Ask for explicit confirmation before applying any automatic fixes.

## Reminder
This file acts as the “function map” for all core workspace actions.  
Do not edit or delete existing rows without explicit double confirmation.
