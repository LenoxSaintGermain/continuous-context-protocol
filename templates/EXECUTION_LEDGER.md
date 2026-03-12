# System EXECUTION_LEDGER

> **CRITICAL INSTRUCTION FOR ALL AUTONOMOUS AGENTS:**
> This file is your Semantic Memory. Before executing any prompt, writing any code, or refactoring any component in this repository, you MUST read this ledger to understand the established architectural truths and live data plumbing constraints. 
> 
> *Do not hallucinate architecture. Let the Ledger guide you.*

---

## [Date/Timestamp] - [Feature/Epic Name]
**Author:** [Agent Name or Developer]

### Architectural Decisions
- [Why was it built this way? E.g., "Opted for Redux over Context API for the global canvas to prevent re-render cascades."]
- [Why was a standard approach avoided? E.g., "Avoided standard fetch; this endpoint requires a signed token from the Gateway Server."]

### Live Plumbing Truths (Do Not Mock)
- [Explicit dependencies. E.g., "The `UserSettings` component relies strictly on the `useAuthStore` hook. Do not replace this with `localStorage` or mock data during refactors."]
- [Critical variables. E.g., "The `OPENAI_API_KEY` is injected server-side. The client must never attempt to access it directly."]

---

*New entries should be prepended to the top of this list.*
