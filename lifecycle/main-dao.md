# The Main DAO

The Main DBrains DAO is the bootstrap project (Application ID 1) that governs the entire platform.

## What Makes It Special

The Main DAO uses the **exact same infrastructure** as any child project — the same governors, tokens, treasury, and access control. It is deployed via `ProjectFactory.bootstrapMainProject()`, an owner-only function that runs during initial platform setup.

This design choice ensures:
- The platform "eats its own dog food" — governance mechanics are battle-tested at the platform level
- No special-case code for platform governance vs project governance
- The Main DAO members experience the same UX as any project team

## Platform Governance Powers

The Main DAO controls:

| Power | Mechanism |
|-------|-----------|
| Approve new projects | Vote via `ProjectFactoryGovernor` → `ProjectFactory.createProject()` |
| Set application fee | `ProjectFactory.setFeeAmount()` via `ProjectSettingGovernor` |
| Set platform-wide POB fee | `ProjectFactory.setPobFeeBasisPoints()` via `ProjectSettingGovernor` |
| Guardian role | Emergency pause on child project order books |

## Revenue

The Main DAO earns revenue through:

1. **Application fees** — 50 USDC per project application (collected by the factory)
2. **POB transaction fees** — A percentage (default 1%) of every NTT conversion in child projects is routed to the Main DAO's `ProjectTreasury`

## Identification

The Main DAO is identified by:
- **On-chain**: Application ID `1` in the `ProjectFactory`
- **PocketBase**: Document ID `"dbrains-main"` in the `projects` collection
- **Metadata URI**: `weavedb://projects/dbrains-main`

The frontend automatically detects the Main project and enables platform-level governance features (like fee configuration) accordingly.
