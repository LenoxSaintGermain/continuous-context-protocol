---
description: Manually compress the EXECUTION_LEDGER.md using intelligent tier detection or user-specified compression level. Optimizes token efficiency while preserving full historical context.
---

# Compress Ledger Workflow (`/compress-ledger`)

Use this workflow when you want to manually compress the EXECUTION_LEDGER without waiting for the auto-trigger from `librarian-sync`.

**When to Use:**
- Ledger feels bloated (slow to load, hard to scan)
- Preparing for a major version release
- Before onboarding new team members (compress to create clean "Current Truth")
- Manual optimization before context-heavy work

---

## Workflow Steps

### 1. Analyze Current State
First, assess the ledger's current state to understand what compression tier is appropriate.

**Actions**:
- Read `EXECUTION_LEDGER.md` (or all domain ledgers if already sharded)
- Check if `COMPRESSION_METADATA.json` exists
- Calculate metrics:
  - Total lines
  - Entry count
  - Estimated tokens (lines × 0.31)
  - Oldest and newest entry dates
  - Domain distribution (if entries are tagged)

**Present to User**:
```
📊 Ledger Analysis:
- Total lines: 1,247
- Estimated tokens: ~3,900
- Entry count: 42
- Date range: 2026-01-29 → 2026-03-12 (42 days)
- Current architecture: monolithic

Compression Recommendations:
✅ Tier 1: RECOMMENDED (ledger > 1000 lines)
⚠️ Tier 2: Available but not urgent (threshold: 2000 lines)
⬜ Tier 3: Not needed yet (threshold: 5000 lines)
```

---

### 2. Choose Compression Tier
Present the user with compression options based on the analysis.

**Use AskUserQuestion** or present options:

**Options**:
1. **Auto-detect** (Recommended): Let the system choose the appropriate tier
2. **Tier 1**: Batch compression (condense old entries into summaries)
3. **Tier 2**: Domain sharding (split into auth/ui/audio/server ledgers)
4. **Tier 3**: Semantic compression (extract Current Truth principles)
5. **Cancel**: Don't compress right now

**If user chooses Auto-detect**:
```markdown
If lines ≥ 5000 → Tier 3
Else if lines ≥ 2000 → Tier 2
Else if lines ≥ 1000 → Tier 1
Else → "No compression needed yet (ledger under 1000 lines)"
```

---

### 3. Execute Compression
Invoke the `librarian-compress` skill with the chosen tier.

**Invocation**:
```
Skill(skill="librarian-compress", args="tier{N}")
```

Or for auto-detect:
```
Skill(skill="librarian-compress")
```

**What Happens**:
- `librarian-compress` executes the compression logic
- Archives are created in appropriate locations
- Original data preserved (never deleted)
- `COMPRESSION_METADATA.json` updated
- Compression results logged

**Wait for Completion**: This is a synchronous operation. Do not proceed until the skill confirms completion.

---

### 4. Verify Results
After compression completes, verify the results and present them to the user.

**Verification Steps**:
- Confirm ledger size reduced (or sharded appropriately)
- Check that archive files were created
- Verify no data loss (spot-check a few entries in archives)
- Calculate actual token reduction
- Read `COMPRESSION_METADATA.json` to confirm event logged

**Present Results**:
```
✅ Compression Complete: Tier 1

Before:
- Lines: 1,247
- Tokens: ~3,900
- Entries: 42

After:
- Lines: 847
- Tokens: ~2,650
- Entries: 32 (10 compressed into 2 summaries)

Reduction: 32% (1,250 tokens saved)

Archives Created:
- docs/ledgers/archive/BATCH_2026-02-15_2026-03-01.md (180 lines)

Metadata: COMPRESSION_METADATA.json updated with compression event
```

---

### 5. Provide Guidance
Give the user context about what just happened and what to expect going forward.

**For Tier 1**:
```
Your ledger has been compressed using batch summarization. Old entries
are now archived, and period summaries remain in the main ledger.

Next Steps:
- Continue using librarian-sync as normal
- Compression will auto-trigger again at 1000 lines
- Full details preserved in archives for reference
```

**For Tier 2**:
```
Your ledger has been sharded into domain-specific files.

Structure:
- EXECUTION_LEDGER_INDEX.md (navigation)
- docs/ledgers/auth_ledger.md
- docs/ledgers/ui_ledger.md
- docs/ledgers/audio_ledger.md
- ... etc

Next Steps:
- When working on auth: Read auth_ledger.md only
- librarian-sync will auto-detect sharded structure
- Cross-domain work: Read multiple relevant ledgers
```

**For Tier 3**:
```
Your ledger has been semantically compressed into a Current Truth document.

Structure:
- docs/ledgers/chronicle/CURRENT_TRUTH_2026-03-12.md (read this first)
- docs/ledgers/chronicle/FULL_CHRONICLE_2026-03-12.md (full history)

Next Steps:
- Start new work by reading CURRENT_TRUTH.md
- Full chronicle available for deep architectural analysis
- librarian-sync continues updating domain ledgers
```

---

## Edge Cases

### If Ledger is Already Compressed
If the user tries to compress a ledger that was recently compressed:
```
⚠️ Ledger was compressed 3 days ago (Tier 1).
Current state: 847 lines (~2,650 tokens)

No compression needed yet. Recommended threshold: 1000 lines.

Would you still like to force compression? [Yes/No]
```

### If Ledger is Too Small
If ledger is under 1000 lines:
```
ℹ️ Ledger is currently 642 lines (~2,000 tokens).

Compression not recommended until 1000+ lines. Your ledger is
healthy and efficient at this size.

Auto-compression will trigger when needed.
```

### If Compression Fails
If the compression process encounters an error:
```
❌ Compression failed: [error reason]

Your ledger was NOT modified. Original data is safe.

Troubleshooting:
1. Check file permissions on docs/ledgers/
2. Verify COMPRESSION_METADATA.json is valid JSON
3. Try again with explicit tier: /compress-ledger tier1

If issue persists, compression can be performed manually or
contact support with the error details.
```

---

## Manual Override Options

Users can pass specific arguments to control compression:

**Force Tier**:
```
User: "compress the ledger using tier 2"
→ Explicitly invoke tier 2 regardless of auto-detection
```

**Dry Run**:
```
User: "show me what compression would do without actually doing it"
→ Run analysis, show projections, but don't execute compression
```

**Custom Date Range** (Tier 1 only):
```
User: "compress entries older than 60 days"
→ Override default 30-day threshold for Tier 1
```

---

## Success Criteria

After completing this workflow, verify:
- ✅ Ledger size reduced OR sharded appropriately
- ✅ Archive files created and contain original data
- ✅ COMPRESSION_METADATA.json updated
- ✅ Token reduction measured and reported
- ✅ User understands new ledger structure
- ✅ Future `librarian-sync` will work with compressed structure

---

## Notes

**Philosophy**: Compression is optimization, not deletion. All original data is preserved in archives. If something goes wrong, archives can always be restored to rebuild the ledger.

**Frequency**: Most projects need compression every 30-60 days. Tier 1 runs automatically, but Tier 2+ requires user approval since they change the ledger structure.

**Reversibility**: Compression can be "undone" by reading the archives. The `COMPRESSION_METADATA.json` file tracks exactly what was compressed and where to find it.
