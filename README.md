# Gemini Workspaces: A Self-Contained, Auditable System for AI Collaboration

This repository contains a structured workspace designed for safe, efficient, and transparent collaboration with Gemini and other AI assistants. It establishes a clear, rule-based system for managing projects, tasks, and context, making it ideal for both solo developers and teams.

## Key Features

*   **Control Tower (`Gemini.md`):** A central file that defines all operating rules, project structures, and protocols for the AI to follow.
*   **Project-Based Structure:** Each top-level folder is treated as an independent project, with its own context and tasks.
*   **Template-Driven Actions:** The `_templates` directory contains guides and templates for standardized actions like `CREATE TASK`, `UPDATE TASK`, and `STORE CONTEXT`, ensuring consistency.
*   **Explicit Confirmation Protocols:** All actions that modify files require explicit confirmation, with previews of the changes, to prevent errors.
*   **Auditable History:** The system is designed to be fully auditable, with clear changelogs, session histories, and update records for each task.
*   **Error Recovery and Validation:** Includes protocols for error recovery (backups) and workspace validation to maintain integrity.

## How It Works

1.  **Start at the Root:** The AI always starts by reading `Gemini.md` to understand the rules of the workspace.
2.  **Navigate to a Project:** The user specifies a project to work on (e.g., `MoXi`).
3.  **Execute Actions:** The user issues commands (e.g., "CREATE TASK 1.1"), which the AI executes by following the corresponding guide in the `_templates` directory.
4.  **Store Context:** The AI stores its reasoning and session history in the relevant task file, providing a clear audit trail.

## Directory Structure

```
/
├── Gemini.md               # The main control tower file
├── MoXi/                   # Example Project 1
│   ├── MoXi.md             # Main context for Project MoXi
│   └── tasks/              # Folder for task-specific files
├── Odyssey/                # Example Project 2
├── Personal/               # Example Project 3
├── Temp/                   # Temporary workspace
└── _templates/             # Contains all action guides and file templates
    ├── actions_index.md    # Maps commands to guide files
    ├── create_task.md      # Guide for creating tasks
    ├── update_task.md      # Guide for updating tasks
    ├── complete_task.md    # Guide for completing tasks
    ├── store_context.md    # Guide for storing session history
    └── task_base.md        # Base template for a new task
```

This system is designed to be self-documenting and easy for new collaborators (human or AI) to understand and use safely.
