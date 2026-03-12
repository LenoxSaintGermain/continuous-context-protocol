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

3. **Compression Check (Auto-Efficiency):**
   - After writing to the ledger, measure its current state:
     - Count total lines in `EXECUTION_LEDGER.md` (or all domain ledgers if using sharded architecture)
     - Calculate estimated tokens (lines × 0.31)
   - Check compression thresholds:
     - **Tier 1**: ≥ 1000 lines
     - **Tier 2**: ≥ 2000 lines
     - **Tier 3**: ≥ 5000 lines

4. **Conditional Compression (Auto-Trigger):**
   - **If Tier 1 threshold met** (≥ 1000 lines):
     - Automatically invoke the `librarian-compress` skill
     - This will perform inline batch compression transparently
     - Wait for compression to complete before proceeding

   - **If Tier 2 threshold met** (≥ 2000 lines):
     - Add warning to confirmation: "⚠️ **Ledger Size Alert**: {lines} lines detected. Recommend running `librarian-compress` with tier2 to shard into domain-specific ledgers for better token efficiency."
     - Do NOT auto-execute (sharding requires user approval)

   - **If Tier 3 threshold met** (≥ 5000 lines):
     - Add warning: "⚠️ **Critical Ledger Size**: {lines} lines detected. Strongly recommend `librarian-compress tier3` for semantic compression to extract Current Truth principles."
     - Do NOT auto-execute (major structural change)

5. **Confirmation:**
   - Once the documentation is synced into the Ledger, explicitly state in your response that the "LIBRARIAN Sync Protocol" was executed successfully.
   - Include compression status:
     - "Compression status: None" (if < 1000 lines)
     - "Compression status: Tier-1-Auto (ledger compressed from {before} to {after} lines)" (if Tier 1 executed)
     - "Compression status: Tier-2-Recommended" (if ≥ 2000 lines)
     - "Compression status: Tier-3-Recommended" (if ≥ 5000 lines)
   - If compression was triggered, include token reduction achieved
