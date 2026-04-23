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
4. **NTTs can be converted** — Through the Private Order Book, NTTs trade for USDC or ETH
5. **Fees fund the ecosystem** — A percentage of each trade supports the platform
6. **Earnings distribute** — A share of every inflow to the treasury is paid out to NTT holders

## Fee Flow

### Within a Child Project

```
Trade happens on POB (in USDC or ETH)
├── 99% → Seller
└── 1% fee → Main DAO ProjectTreasury (in the same currency as the trade)
```

### Within the Main DAO

```
Trade happens on POB
├── 99% → Seller
└── 1% fee → Main DAO ProjectTreasury (stays in same project)
```

The fee rate (default 1%, configurable in basis points) is a global parameter on the `ProjectFactory`, meaning the Main DAO sets a uniform fee rate across all projects. Fees are always collected in the same currency as the trade — a USDC trade produces a USDC fee, an ETH trade produces an ETH fee.

## Earnings Distribution to NTT Holders

Every inflow to the project treasury — POB fees on fills, investor contributions, application fees, direct deposits — is split between:

- A **distribution pool** that is paid out pro-rata to NTT holders
- **Operational funds** that stay with the treasury

The split is governed by a **distribution ratio** (default 50%, adjustable through governance). Each NTT holder accumulates a claimable balance in both ETH and USDC as earnings flow in, proportional to their NTT balance at the time of each earning. They can claim their accumulated share at any time.

Revoked members keep their NTT and can still claim their earned share — their past contribution is never lost, even if they are no longer active in governance.

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
- **Deflationary on exit** — converting to USDC or ETH burns tokens, benefiting remaining holders
- **Income-producing** — every inflow to the treasury distributes a share to NTT holders

This design aligns incentives: the best way to increase your NTT value is to contribute to the project's success.
