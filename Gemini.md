# Gemini Workspace Hub: The Constitution

**Last Updated:** 2025-11-16

---

### 1. Overview

This file is the **root `GEMINI.md`**, serving as the master guide for the entire `GeminiWorkspaces` environment. It defines the global rules, lists all active projects, and sets the operational context for our collaboration.

**Company:** Confer Solutions AI
**Purpose:** A multi-client AI/ML software company.

### 2. Workspace Structure

This hub is organized into a series of distinct project and meta-workspaces.

*   **Project Workspaces:** Self-contained folders for client work or internal products.
*   **Meta Workspaces (`_` prefix):** Folders containing shared resources, like templates.

### 3. Master Project Index

| Project             | Folder Path           | Purpose                                      |
|---------------------|-----------------------|----------------------------------------------|
| **ConferSolutionsAI** | `ConferSolutionsAI/`  | Internal Frameworks & Company Assets         |
| **MoXi**            | `MoXi/`               | Client Engagement: AI for Mortgage Services  |
| **Odyssey**         | `Odyssey/`            | (To be defined)                              |
| **Personal**        | `Personal/`           | User's personal tasks and experiments        |
| **Temp**            | `Temp/`               | Ephemeral scratchpad (safe to delete)        |
| **_templates**      | `_templates/`         | Global file templates and action definitions |

### 4. Global Rules & Protocols

#### **a. My Primary Directive**
My first action in any session is to read the `GEMINI.md` file in the relevant workspace directory to load the correct context.

#### **b. Creating a New Project Workspace**
1.  Create a new top-level folder: `<ProjectName>/`.
2.  Create a `GEMINI.md` file inside it, preferably based on a template from `_templates/`.
3.  Update the **Master Project Index** in *this file* to include the new project.

#### **c. Security & Data Handling**
*   Never commit API keys, passwords, or sensitive client data to version control.
*   Use environment variables or a secure secret management system.
*   Sanitize all data before using it in training sets or logs.

#### **d. Coding Style**
*   Default to **PEP 8** for Python and **Prettier** for JavaScript/TypeScript unless a project's `GEMINI.md` specifies otherwise.
*   Strive for clear, readable, and maintainable code.

### 5. Original Context File
The original `Gemini.md` (before it was standardized to `GEMINI.md` and updated) is preserved for historical context and can be found in the git history.