# STORE CONTEXT / STORE HISTORY
Last updated: November 9, 2025, 14:26:53 CST

**Purpose:** Capture reasoning, insights, and conversational summary from the current AI session and store it inside the relevant task file.

## Core Behavior
1. Identify the task file currently in focus.
2. Summarize the session into **3–5 concise bullet points** covering:
   - What was accomplished.
   - Key reasoning steps or decisions.
   - Any new context discovered.
   - Next steps or TODOs.
3. Append the summary under the `## Session History` section with timestamp.

Note: `STORE CONTEXT` / `STORE HISTORY` always writes under the `## Session History` section.
These entries capture AI reasoning, context, and decision-making — not just high-level status.

### Example Block
```markdown
### 2025-11-09 14:15 CST
- Implemented session-saving logic.
- Confirmed double-write protection for context files.
- Next: Integrate context recall in `Gemini.md` workflow.
```

4. Update `Last updated:` at the top of the file.

## Confirmation Rules

Before storing context or history:

1. Show the resolved file path for the target task file.
2. Confirm that the summary will be appended under the `## Session History` section.
3. Preview the bullet-point summary and timestamp that will be written.
4. Ask explicitly: "Store this session history for task <ID>? (yes/no)"

If no task file is found:
- Offer to create a new one using `_templates/task_base.md`, but only with explicit user consent.

Never overwrite existing history — always append a new block.

## Notes
- “STORE CONTEXT” and “STORE HISTORY” are synonyms.
- This command effectively snapshots the reasoning state.
