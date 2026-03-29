# NTT Conversion Economics

Understanding how value flows through the NTT ecosystem.

## The Value Cycle

```
Work → NTT Minting → Ownership & Voting → Conversion → Value Extraction
  ↑                                                          |
  └──────────── Treasury funds more work ←──────────────────┘
```

1. **Contributors do work** — Tasks are proposed and executed
2. **NTTs are minted** — Verified work earns NTT rewards
3. **NTTs represent ownership** — Voting power + profit share in the project
4. **NTTs can be converted** — Through the Private Order Book, NTTs trade for USDC
5. **Fees fund the ecosystem** — A percentage of each trade supports the platform

## Fee Flow

### Within a Child Project

```
Trade happens on POB
├── 99% USDC → Seller
└── 1% fee → Main DAO ProjectTreasury
```

### Within the Main DAO

```
Trade happens on POB
├── 99% USDC → Seller
└── 1% fee → Main DAO ProjectTreasury (stays in same project)
```

The fee rate (default 1%, configurable in basis points) is a global parameter on the `ProjectFactory`, meaning the Main DAO sets a uniform fee rate across all projects.

## Supply Dynamics

### Inflationary Pressure (Minting)

NTTs are minted in two scenarios:
- **Task verification** — The `TaskManager` mints NTTs to the assignee
- **Project ASK orders** — When the project sells NTTs on the POB, new tokens are minted

More minting means more total supply, which dilutes existing holders' percentage ownership.

### Deflationary Pressure (Burning)

NTTs are burned when:
- **Selling NTTs** — A member places an ASK order and their NTTs are burned upon fill
- **Project BID orders** — When the project buys back NTTs, they are burned (reducing supply)

Burning concentrates ownership among remaining holders, increasing each token's proportional value.

### Equilibrium

The DAO controls this balance through governance:
- **Need funding?** → Open a project ASK order (dilutive, but brings USDC into treasury)
- **Want to reward holders?** → Open a project BID order (buyback, deflationary)
- **Growing the team?** → More task verifications mint NTTs (dilutive, but grows capacity)

## Price Discovery

NTT prices emerge from the Private Order Book's supply and demand:
- **Project ASK price** — Set by the DAO; represents the "official" selling price for new NTTs
- **Member ASK price** — Set by individual sellers; market-driven
- **BID prices** — Set by buyers willing to pay for NTTs

The spread between ASK and BID prices reflects the market's valuation of the project's NTTs.

## Key Insight

NTTs are not speculative tokens. They are:
- **Earned** through verified contributions
- **Non-transferable** — no secondary market speculation
- **Internally valued** — price discovery happens within the project community
- **Deflationary on exit** — converting to USDC burns tokens, benefiting remaining holders

This design aligns incentives: the best way to increase your NTT value is to contribute to the project's success.
