# Gemini Workspace Control Tower
Last updated: November 9, 2025, 14:26:53 CST

This directory, `/Users/yatinkarnik/Workspace/GeminiWorkspaces`, serves as the base for all Gemini workspaces. Its structure and rules are designed to ensure consistent and safe operation.

## Gemini Operating Instructions

- **Always Start Here:** Before any task, read this file (`Gemini.md`) to understand the workspace context, rules, and project structure.

- **Project vs. Meta Folders:**
    - Each immediate subfolder is an independent project (e.g., `MoXi/`).
    - Folders starting with an underscore (`_`) are **meta folders** (e.g., `_templates/`), not projects. Do not enter or modify them unless explicitly instructed.

- **Main Context File:** Each project has a primary context file located inside its folder, named after the folder with a `.md` extension (e.g., `MoXi/MoXi.md`).

- **Task-Specific Files:** Future task-specific context files will be located in a `tasks/` subfolder within each project (e.g., `MoXi/tasks/task-3.1.md`). Do not create or reference these files unless explicitly told to do so.

- **Write Guardrails & Double Confirmation:**
    - Do not create, rename, or modify any files at the root level by default.
    - Key context files (`Gemini.md` and all `<Project>/<Project>.md` files) are protected. Only modify them when I explicitly ask for a change **and confirm it twice**. This prevents accidental overwrites.

- **Actions Index:** All reusable commands (CREATE TASK, UPDATE TASK, COMPLETE TASK, STORE CONTEXT/HISTORY) are defined in _templates/actions_index.md.
    - Gemini must consult that file before executing any action.
    - When new templates are added under _templates/, update _templates/actions_index.md to include them.

- **Creating New Projects:**
    1. Create a new top-level folder: `<ProjectName>/`.
    2. Inside, create the main project file: `<ProjectName>/<ProjectName>.md`. This file can be based on a template from the `_templates/` directory.

## Projects

| Project  | Folder Path      | Main Context File         |
|----------|------------------|---------------------------|
| MoXi     | `MoXi/`          | `MoXi/MoXi.md`            |
| Odyssey  | `Odyssey/`       | `Odyssey/Odyssey.md`      |
| Personal | `Personal/`      | `Personal/Personal.md`    |
| Temp     | `Temp/`          | `Temp/Temp.md`            |

## How to Start Work in a Project

1.  **Navigate to the project folder.**
2.  **Read the corresponding `<FolderName>.md` file first.**
3.  **Operate only inside that project folder for the work session.**
4.  **Missing Context:** If a project's main `<Project>.md` file is missing or empty, you may offer to scaffold it based on a template, but **do not create or edit it automatically**. Proceed only after my explicit confirmation.
5.  You may also use optional dry-run and validation behaviors defined in `_templates/actions_index.md` (e.g., a `VALIDATE WORKSPACE` command) to safely inspect changes before committing them.

## Template Maintenance Rule
Whenever new template or guide files are created inside `_templates/`, Gemini should:
1. Announce that `_templates/actions_index.md` may need updating.
2. Offer to automatically insert a new row in the “Available Actions” table.
3. Confirm twice before making any edits.

## File Resolution Protocol
When a task is referenced by ID (e.g., "task 3.1"):

1. Assume the current project is the active folder Gemini is operating in (e.g., `MoXi/`).
2. Search **only** within that project’s `tasks/` subfolder for files matching:
   `tasks/task-<ID>*.md`
   - Example: for ID `3.1`, search `tasks/task-3.1*.md`
3. If multiple matches are found:
   - List all candidate files with their full paths.
   - Ask the user to choose exactly one before proceeding.
4. If the `tasks/` folder does not exist:
   - Offer to create `tasks/` for the project, with single confirmation.
5. If the `tasks/` folder exists but no matching file is found:
   - Ask whether to create a new task file using `_templates/task_base.md`.
   - Only create it after explicit confirmation.

## Changelog
> Track major structural changes to workspace rules and templates.

### 2025-11-09 14:20 CST
- Added File Resolution Protocol.
- Clarified `Updates` vs. `Session History` semantics.
- Introduced filename sanitization for task creation.
- Added optional dry-run and validation modes.

### 2025-11-09 14:11 CST (Initial Release)
- Established core workspace structure.
- Created action templates and dispatch system.

## Error Recovery

If a write operation is incorrect or corrupts a file:

1. Immediately create a backup file:
   `<filename>_backup_<timestamp>.md`
2. Store backups inside a project-specific `_backups/` folder, e.g.:
   `<Project>/_backups/`
3. Copy the current version of the file into the backup before making any destructive change.
4. Inform the user that a backup was created and offer options:
   - Restore from backup, or
   - Proceed and manually fix the current file.
5. Require explicit confirmation before restoring or discarding any backup.
