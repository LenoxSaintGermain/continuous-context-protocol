---
description: Strictly forbids the use of mock data or placeholder functions when modifying live components, enforcing continuous context.
---

# CCP Rule: Anti-Mocking & Plumbing Preservation

When refactoring, upgrading, or modifying existing live code in this repository, you MUST passionately preserve the live data plumbing. 

1. **No Mocking Shortcuts**: You are strictly forbidden from injecting `mockData`, `mockServerKeys`, `dummy`, or placeholder variables as a shortcut to make a UI render during refactors.
2. **Read the Ledger**: If you are unsure what the live hooks or state managers are, you must consult the `EXECUTION_LEDGER.md` (or the component's imports) to find the truth. Never guess.
3. **Preserve the Interface**: If a component you are refactoring uses specific live contexts (e.g., `useSettingsStore()`), the refactored version MUST use those exact same connections. Do not drop existing data connections.
4. **Self-Auditing**: Before declaring a task "complete", you must self-audit your work. Check for the words `mock`, `temp`, and `TODO`. If they exist where live data should be, you have failed the Continuous Context Protocol. Fix the plumbing before stopping.
