# Execution Ledger Index

> **Note**: This project uses **domain-sharded ledgers** for token efficiency. Instead of one massive ledger, context is organized by domain so agents only load relevant information.

---

## Domain Ledgers

| Domain | File | Lines | Last Updated |
|--------|------|-------|--------------|
| 🔐 Authentication | [auth_ledger.md](ledgers/auth_ledger.md) | 0 | YYYY-MM-DD |
| 🎨 UI/Frontend | [ui_ledger.md](ledgers/ui_ledger.md) | 0 | YYYY-MM-DD |
| 🔊 Audio Engine | [audio_ledger.md](ledgers/audio_ledger.md) | 0 | YYYY-MM-DD |
| 🖥️ Server/API | [server_ledger.md](ledgers/server_ledger.md) | 0 | YYYY-MM-DD |
| 🔌 Integrations | [integration_ledger.md](ledgers/integration_ledger.md) | 0 | YYYY-MM-DD |
| 🚀 Deployment | [deployment_ledger.md](ledgers/deployment_ledger.md) | 0 | YYYY-MM-DD |

---

## Quick Navigation

**Working on authentication?** → Read [auth_ledger.md](ledgers/auth_ledger.md)
**UI/component changes?** → Read [ui_ledger.md](ledgers/ui_ledger.md)
**Audio features?** → Read [audio_ledger.md](ledgers/audio_ledger.md)
**Backend/API work?** → Read [server_ledger.md](ledgers/server_ledger.md)
**Third-party integrations?** → Read [integration_ledger.md](ledgers/integration_ledger.md)
**CI/CD or deployment?** → Read [deployment_ledger.md](ledgers/deployment_ledger.md)

**Need full context?** → Read all domain ledgers (total: 0 lines)

---

## Compression History

**Last Sharding**: YYYY-MM-DD
**Pre-Shard Archive**: [LEDGER_PRE_SHARD_YYYY-MM-DD.md](ledgers/archive/LEDGER_PRE_SHARD_YYYY-MM-DD.md)
**Original Line Count**: 0 lines
**Token Reduction**: 0% (sharded for scalability)

---

## About Domain Sharding

Domain sharding is **Tier 2 compression** in the Continuous Context Protocol (CCP). It splits a monolithic ledger into domain-specific files so agents working on UI features don't need to load 2000+ lines of audio engine history.

**Benefits**:
- ✅ **Token Efficient**: Only load relevant domain (66-85% token reduction)
- ✅ **Faster Context Loading**: Smaller files = quicker reads
- ✅ **Better Organization**: Related entries grouped together
- ✅ **Scalable**: Each domain can grow independently

**When to Use**:
- Ledger exceeds 2000 lines
- Multiple distinct areas of the codebase being developed
- Team working on different domains simultaneously

**Managed By**: `librarian-compress` skill (Tier 2)

---

## Archive Locations

**Batch Compressions** (Tier 1): `ledgers/archive/BATCH_*.md`
**Pre-Shard Ledgers** (Tier 2): `ledgers/archive/LEDGER_PRE_SHARD_*.md`
**Semantic Snapshots** (Tier 3): `ledgers/chronicle/CURRENT_TRUTH_*.md`

See [COMPRESSION_METADATA.json](COMPRESSION_METADATA.json) for complete compression history.
