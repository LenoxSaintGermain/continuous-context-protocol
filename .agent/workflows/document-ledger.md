---
description: A workflow template forcing the executing agent to write architectural decisions and constraints into a global Ledger.
---

# Document Ledger Workflow (`/document-ledger`)

Use this workflow immediately before concluding a session, closing a pull request, or finishing a significant refactor. This guarantees the next autonomous agent inherits your exact thought process and structural constraints.

## Workflow Steps

### 1. Diffs & Intent Analysis
- Compile a list of the files you just fundamentally altered.
- List the structural "whys". (Not *what* you coded, but *why* you coded it that way).
  - *Example*: "Did not use standard REST fetch because the upstream API requires WebSockets for latency."

### 2. Identify Plumbing Hazards
- Explicitly list any complex state wiring you introduced or modified.
  - *Example*: "The `UserProfile` component now strictly depends on Firebase `user.uid` and will crash without it. Do NOT refactor this out."

### 3. Ledger Sync
- Open the root `EXECUTION_LEDGER.md` (or your chosen continuous context artifact).
- Add a new timestamped entry containing:
  - **Feature/Task**: The name of what was built.
  - **Architectural Decisions**: The "whys" from Step 1.
  - **Plumbing Truths**: The hazards identified in Step 2.

### 4. Verification
- Verify the ledger has been successfully written to disk.
- Use `notify_user` to state: "Continuous Context Protocol fulfilled. The ledger has been updated for the next session."
