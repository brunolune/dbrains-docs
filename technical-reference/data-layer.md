# Data Layer (PocketBase)

DBrains uses **PocketBase** as its off-chain data layer — a lightweight Go backend providing a REST API with SQLite storage.

## Strategy: PocketBase-First

The frontend fetches all project data primarily from PocketBase for instant, rich metadata. Blockchain is queried only for authoritative status flags (`validated`, `executed`) and contract addresses via efficient multicall.

## Collections

DBrains uses 10 PocketBase collections, all with public read/write rules (authorization is handled on-chain via SBT/NTT ownership):

| Collection | Purpose |
|------------|---------|
| `projects` | Project metadata (title, description, category, creator) |
| `members` | Project membership records (projectId, address, role, joinedAt) |
| `project_proposals` | Proposal metadata (projectId, title, type, status, proposer) |
| `project_tasks` | Task metadata linked to projects |
| `freelancer_applications` | Freelancer onboarding applications |
| `investor_applications` | Encrypted investor details (nttAmount, pricePerNttUsdc, usdcCost) |
| `comments` | Chat messages with `targetType` and `targetId` for thread isolation |
| `profiles` | User profile metadata |
| `tasks` | Additional task metadata |
| `proposals` | Additional proposal metadata |

## The Adapter Pattern

The PocketBase adapter (`web/src/lib/weavedb.ts`) provides a drop-in replacement for the former WeaveDB client:

### API Surface

```
get(collection, docId)        — Fetch single record by logical ID
get(collection, ...filters)   — Fetch with WeaveDB-style filters
cget(collection)              — Fetch all records in a collection
set(data, collection, docId)  — Create or replace a record
update(data, collection, docId) — Update fields on existing record
upsert(data, collection, docId) — Create or update
del(collection, docId)        — Delete a record
```

### docId Pattern

PocketBase enforces 15-character auto-generated record IDs. The adapter stores the logical document ID (e.g., `"dbrains-main"`, UUIDs, `"proposal-{bigint}"`) in a `docId` text field. All CRUD operations query by `docId` filter and inject `id: docId` into returned records so consumer code reads `.id` as the logical identifier.

### Filter Translation

WeaveDB-style filter arguments are automatically translated to PocketBase filter/sort syntax:
- `["field", "==", "val"]` → PocketBase filter
- `["field", "asc"]` → PocketBase sort

## Key Hooks

### useProjects()

Fetches all PocketBase projects, cross-references with on-chain data:
- Iterates `ProjectFactory.applications(appId)` for appIds 1-20 via multicall
- Returns `activeProjects` (deployed) and `pendingApplications` (not yet executed)
- Team size fetched via SBT `name()` per project

### useProjectBoard(project)

Dashboard-ready data fetching:
- **Members**: Probes `SBT.ownerOf(tokenId)` for tokenIds 1-20 via multicall
- **Balances**: NTT balance per member
- **Treasury**: ETH, USDC, and NTT holdings
- **Order Book**: Active orders and events

### useChat(targetType, targetId)

Real-time chat for any target (project, proposal, or task):
- Polls every 5 seconds via `setInterval`
- Optimistic updates on send (rolls back on error)
- Module-level in-memory cache

## Deployment

### Production

- Dockerized PocketBase v0.22 on Railway
- Persistent volume for SQLite
- Domain: `api.dbrains.xyz`
- Auto-creates admin account from environment variables on startup

### Local Development

```bash
pocketbase serve
# Available at http://localhost:8090
```

No separate database server needed. Migrations in `pb/pb_migrations/` auto-run on startup.
