# The Main DAO

The Main DBrains DAO is the bootstrap project that governs the entire platform.

## What Makes It Special

The Main DAO uses the **exact same infrastructure** as any child project — the same governors, tokens, treasury, and access control. It is deployed via `ProjectFactory.bootstrapMainProject()`, an owner-only function that runs during initial platform setup.

## Platform Governance Powers

The Main DAO controls:

| Power                     | Mechanism                                                            |
| ------------------------- | -------------------------------------------------------------------- |
| Approve new projects      | Vote via `ProjectFactoryGovernor` → `ProjectFactory.createProject()` |
| Set application fee       | `ProjectFactory.setFeeAmount()` via `ProjectSettingGovernor`         |
| Set platform-wide POB fee | `ProjectFactory.setPobFeeBasisPoints()` via `ProjectSettingGovernor` |
| Guardian role             | Emergency pause on child project order books                         |

## Revenue

The Main DAO earns revenue through:

1. **Application fees** — 50 USDC per project application (collected by the factory)
2. **POB transaction fees** — A percentage (default 1%) of every NTT conversion in child projects is routed to the Main DAO's `ProjectTreasury`
