---
name: librarian-sync
description: Enforces that the agent updates the Continuous Context Protocol (CCP) Ledger after every Epic, Feature, or significant integration phase.
---

# LIBRARIAN Sync Protocol

**Purpose:**
To eliminate "Context Rot" and prevent the agentic system from losing track of architectural decisions, un-written rules, and live data plumbing configurations. The agent is forced to act as the System Historian.

**When to Use:**
You **MUST** use this skill immediately after completing any multi-step task, merging a feature, or closing a bug. You must not end a session without invoking this protocol.

## Protocol Steps

1. **Information Extraction:**
   - Review your recent tool calls, terminal outputs, and the code changes you just made.
   - Specifically identify *why* you made a structural change (e.g., "Why did we use `Zod` over `Yup`?", "Why did we route around the standard API?").

2. **Artifact Enforcement (Mandatory):**
   - You **MUST** write or update a concise summary of the newly built feature into the project's root `EXECUTION_LEDGER.md` (or equivalent `.md` manifest).
   - Document any live interfaces or hooks that your code now relies on (e.g., "SettingsView now explicitly requires `useAuthStore`").
   - This ensures the next agent does not hallucinate placeholder components.

3. **Confirmation:**
   - Once the documentation is synced into the Ledger, explicitly state in your `TaskSummary` that the "LIBRARIAN Sync Protocol" was executed successfully.
