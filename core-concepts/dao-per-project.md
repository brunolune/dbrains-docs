# DAO per Project

Every project on DBrains operates as its own independent DAO. This means each project has full sovereignty over its governance, finances, and membership.

## What Makes Each Project a DAO

Each project gets:

- **Its own treasury** — A `ProjectTreasury` contract holding ETH and stablecoins
- **Its own governance** — 7 specialized governors handling different decision domains
- **Its own tokens** — Project-specific NTT (contribution) and SBT (membership)
- **Its own internal market** — A `PrivateOrderBook` for NTT conversions
- **Its own access control** — An `AccessManager` defining roles and permissions

## Independence with Oversight

While each project DAO is self-governing, the Main DBrains DAO retains a **Guardian Role** for platform-wide security:

- The Guardian can **pause** a project's order book in emergencies
- The Main DAO collects a small fee on NTT conversions in child projects
- The `ProjectFactory` (owned by the Main DAO) controls project creation

This creates a balance: projects are free to govern themselves, but the platform maintains safety rails.

## How Projects Relate

```
Main DBrains DAO (Project #1)
├── Owns ProjectFactory
├── Collects platform fees
├── Guardian role over child projects
│
├── Child Project #2
│   └── Full DAO (treasury, governors, tokens, order book)
├── Child Project #3
│   └── Full DAO (treasury, governors, tokens, order book)
└── ...
```

The Main DBrains DAO is itself a project — bootstrapped via `ProjectFactory.bootstrapMainProject()` — sharing the exact same infrastructure as child projects. It governs the platform by controlling the factory and setting global parameters like fees.
