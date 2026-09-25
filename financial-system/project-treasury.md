# Project Treasury

Each project has a `ProjectTreasury` contract — a lightweight wallet that holds and manages project funds.

## What It Holds

- **ETH** — Native currency, held as a first-class asset
- **USDC** — Stablecoin, held as a first-class asset
- **Any ERC-20 token** — The treasury can receive and hold arbitrary tokens

Both ETH and USDC circulate through the platform as equal partners — trades can happen in either currency, and the treasury accumulates both from its various revenue sources.

## How Funds Flow In

| Source | Description |
|--------|-------------|
| NTT conversions | Platform fee (default 1%) on every order book trade, collected in the trade's currency |
| Investor onboarding | USDC or ETH from investor bid orders |
| Project ASK orders | Revenue from selling project NTTs, in whichever currency the ASK is denominated |
| Application fees | For the Main DAO, fees from new project applications (USDC or ETH) |
| Direct deposits | Anyone can send ETH or tokens directly to the treasury |

## How Funds Flow Out

All spending requires a governance vote through the `TreasuryGovernor`:

- `transferETH(recipient, amount)` — Send ETH
- `transferERC20(token, recipient, amount)` — Send any ERC-20 token

No individual — not even the project creator — can unilaterally spend treasury funds.

### Treasury Transfer Proposals

Members move funds with a **Treasury Transfer** proposal: pick the asset (ETH or USDC), the recipient, and the amount. The form shows how much is available to spend and blocks a transfer the treasury can't cover — money set aside for NTT holders' earnings (see below) can never be spent this way. Treasury transfers are used for contributor payouts, operational costs, and gas funding for AI agents.

The TreasuryGovernor is the **only** governor allowed to move funds. A transfer can't be tucked into another kind of proposal (an onboarding vote, for example): it would pass the vote but could never be carried out.

### Allowances (For AI Agents)

The treasury also supports **spending allowances** — pre-approved limits that let a specific wallet pull funds up to a cap without a separate governance vote each time. This is used to fund AI agents (see [Spending & Removal](../agents/spending-and-removal.md)). Allowances are set through governance and can be raised, lowered, or revoked in a single vote. Unlike transfers, allowances can also be set by the FreelancerGovernor, so an agent's onboarding and removal votes can include its allowance.

## Earnings Distribution

A configurable portion of **all incoming funds** (ETH and USDC) is automatically earmarked for distribution to NTT holders, pro-rata to their NTT balance at the time of each earning.

### How It Works

- A **distribution ratio** (default 50%) governs the split between distributed earnings and operational funds
- The distributed pool accumulates over time as earnings flow into the treasury
- Each NTT holder's share grows in proportion to their NTT balance
- Holders can **claim** their accumulated ETH and USDC at any time

### Who Can Claim

Any holder of NTT can claim — no SBT required. This means:

- Active members claim their share as part of their ongoing participation
- **Revoked members** can still claim earnings on NTT they held at the time of revocation. Their contribution is preserved even after they leave.

### Earnings Dashboard

The dashboard treasury widget shows each member's:

- Claimable ETH and USDC
- Total unclaimed pool for the project
- Current distribution ratio

Buttons let the member **sweep** (account for any new incoming funds) and **claim** (withdraw their share). For members who have been revoked from projects, a dedicated **My Holdings** page aggregates their claimable earnings across every project where they still hold NTT. Each revoked row on that page also exposes a **Sell NTT** panel — a sell-only view of the project's order book — so an ex-member can convert their remaining NTT to USDC or ETH without needing access to the (SBT-gated) project dashboard. See [Private Order Book → Access Control](private-order-book.md#access-control) for the buy-side / sell-side split that makes this possible.

### Governance Control

The distribution ratio is a project-level parameter adjustable through the `ProjectSettingGovernor`. A project that wants to reinvest more aggressively can lower the ratio; one that prioritizes immediate returns to contributors can raise it.

## Fee Structure

### Platform Fee (Child Projects)

When NTTs are converted in a child project's Private Order Book, a fee (default 1%) is deducted from the currency side of the trade. For child projects, this fee is routed to the **Main DAO's ProjectTreasury** in the same currency as the trade — the platform's primary revenue stream.

### Project Fee (Main DAO)

For the Main project itself, the conversion fee stays in its own treasury.

### Fee Configuration

The fee rate is a **global parameter** stored on the `ProjectFactory` and read by every order book at trade time. It is updated by the Main DAO through the `ProjectSettingGovernor`.

## Dashboard Widget

The Treasury is visible on the project dashboard with:

- Real-time USD balance (ETH + stablecoins)
- NTT supply and ownership distribution
- Earnings Share panel (claimable ETH/USDC, unclaimed pool, distribution ratio)
- Private Order Book status indicator
