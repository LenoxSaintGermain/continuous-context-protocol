# Architectural Current Truth

> **Generated**: YYYY-MM-DD from X,XXX ledger lines
>
> **Purpose**: This document distills thousands of implementation entries into the essential architectural principles, patterns, and constraints that define this project's "Current Truth." Read this first when joining the project or starting new work.

---

## Core Architectural Principles

### [Domain Name - e.g., Authentication Architecture]

**Decision**: [Brief description of architectural choice]

**Rationale**: [Why this approach was chosen over alternatives]

**Implementation**:
- **Primary Interface**: [Key file/function/class]
- **Dependencies**: [What it relies on]
- **Integration Points**: [How other systems interact with it]

**Critical Constraints**:
- [Important limitation or requirement to remember]
- [Another constraint]

**Example**:
```typescript
// How this is used in practice
import { useAuthStore } from '@/lib/stores/authStore'

const { user, isAuthenticated } = useAuthStore()
```

---

### [Another Domain - e.g., UI Component Patterns]

**Decision**: [Architectural choice]

**Rationale**: [Why this pattern]

**Implementation**:
- **Pattern**: [Design pattern name]
- **Example Components**: [Where this is used]
- **Benefits**: [What this achieves]

**Anti-Pattern** (What NOT to do):
```typescript
// ❌ WRONG: Prop proliferation
<Radio options={[...]} onChange={...} disabled={...} />

// ✅ CORRECT: Compound components
<Radio.Group>
  <Radio.Item value="a" />
  <Radio.Item value="b" />
</Radio.Group>
```

---

## Critical Gotchas & Lessons Learned

### [Technology/Service Name]
- **Issue**: [What goes wrong if you don't know this]
- **Solution**: [How to avoid it]
- **Context**: [When this matters]

**Example Gotchas**:
- **Firebase Quota Limits**: Custom claims limited to 50k updates/day. Use Firestore for frequent permission changes.
- **React Native Audio**: Must request iOS permissions before audio.play() or it silently fails.
- **TypeScript**: Never use `any` for external API responses. Use `unknown` and validate with Zod.

---

## Established Patterns & Conventions

### Code Organization
- **Stores**: Global state in `lib/stores/` using Zustand
- **API Layer**: All Firebase calls in `lib/api/` (never direct in components)
- **Types**: Shared types in `lib/types/`, schema validation with Zod
- **Components**: Atomic design - `components/atoms/`, `components/molecules/`, `components/organisms/`

### Naming Conventions
- **Files**: camelCase for utilities, PascalCase for components
- **Functions**: Verb-based (e.g., `fetchUserData`, `validateSchema`)
- **Types**: PascalCase + descriptive (e.g., `UserProfile`, `AuthState`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `MAX_RETRIES`, `API_TIMEOUT`)

### Testing Strategy
- **Unit Tests**: All utilities and pure functions
- **Integration Tests**: API layer and store interactions
- **E2E Tests**: Critical user flows only (auth, core features)
- **Coverage Target**: 80% for `lib/`, 60% for components

---

## Critical Dependencies & Interfaces

### [System Name]

**Interface Contract**:
```typescript
interface SystemInterface {
  // What this system exposes
}
```

**Consumers**: [What relies on this]
**Providers**: [What this relies on]
**Breaking Change Protocol**: [How to safely modify this]

---

## Deprecated Approaches (Do Not Use)

These patterns were tried and abandoned. Do NOT reintroduce them:

### ❌ Mock localStorage in Components
**Why Deprecated**: Breaks browser behavior, causes subtle bugs in production
**Use Instead**: Real browser localStorage with fallback handling
**Deprecated**: Feb 2026

### ❌ Direct Firebase SDK in React Components
**Why Deprecated**: Creates tight coupling, makes testing impossible
**Use Instead**: API layer in `lib/api/` that wraps Firebase calls
**Deprecated**: Jan 2026

### ❌ Prop Drilling for Global State
**Why Deprecated**: Unscalable, verbose, error-prone
**Use Instead**: Zustand stores with context when needed
**Deprecated**: Jan 2026

---

## Technology Stack Decisions

### Why [Technology X]?
**Chosen Over**: [Alternative]
**Reasoning**: [Why we picked this]
**Trade-offs**: [What we gave up]
**Re-evaluation Date**: [When to reconsider]

**Example**:
### Why Zustand for State Management?
**Chosen Over**: Redux, Context API, Jotai
**Reasoning**:
- Minimal boilerplate (3-5 lines per store)
- No providers needed (simpler than Context)
- Built-in TypeScript support
- DevTools integration
**Trade-offs**: Less opinionated (need to establish our own patterns)
**Re-evaluation Date**: If team grows beyond 10 developers

---

## Quick Reference: Common Operations

### How to Add a New Feature Domain
1. Create domain store in `lib/stores/`
2. Add API layer in `lib/api/`
3. Define types in `lib/types/`
4. Build UI in `components/`
5. Add tests in `__tests__/`
6. Update this document with new patterns

### How to Integrate a Third-Party Service
1. Evaluate against security checklist
2. Create wrapper in `lib/integrations/`
3. Abstract vendor details (enable swapping)
4. Add error handling and retries
5. Document rate limits and quotas
6. Update EXECUTION_LEDGER with constraints

### How to Modify Core Architecture
1. Check if breaking change (impacts other systems?)
2. If yes: Create RFC document, get team approval
3. If no: Proceed with backward compatibility
4. Update interfaces and types
5. Migrate gradually (feature flag if needed)
6. Update this Current Truth document

---

## Versioning & Updates

**Current Truth Version**: 1.0 (YYYY-MM-DD)
**Previous Versions**:
- [CURRENT_TRUTH_YYYY-MM-DD.md](archive/CURRENT_TRUTH_YYYY-MM-DD.md)

**Update Frequency**: Every Tier 3 compression (typically every 2-3 months or 5000+ new ledger lines)

**Managed By**: `librarian-compress` skill (Tier 3 semantic compression)

---

## Full Historical Record

For complete chronological history of all implementation decisions:
- **Full Chronicle**: [ledgers/chronicle/FULL_CHRONICLE_YYYY-MM-DD.md](ledgers/chronicle/FULL_CHRONICLE_YYYY-MM-DD.md)
- **Domain Ledgers**: [EXECUTION_LEDGER_INDEX.md](../EXECUTION_LEDGER_INDEX.md)

This Current Truth is distilled from that history but preserves only what's relevant to current and future development.
