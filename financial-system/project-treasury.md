# Project Treasury

Each project has a `ProjectTreasury` contract — a lightweight wallet that holds and manages project funds.

## What It Holds

- **ETH** — Native currency
- **Stablecoins** — USDC (designed for future multi-currency support)
- **Any ERC-20 token** — The treasury can receive and hold arbitrary tokens

## How Funds Flow In

| Source | Description |
|--------|-------------|
| NTT conversions | Platform fee (default 1%) on every order book trade |
| Investor onboarding | USDC from investor bid orders |
| Project ASK orders | Revenue from selling project NTTs |
| Direct deposits | Anyone can send ETH to the treasury's `receive()` function |

## How Funds Flow Out

All spending requires a governance vote through the `TreasuryGovernor`:

- `transferETH(recipient, amount)` — Send ETH
- `transferERC20(token, recipient, amount)` — Send any ERC-20 token

No individual — not even the project creator — can unilaterally spend treasury funds.

## Fee Structure

### Platform Fee (Child Projects)

When NTTs are converted in a child project's Private Order Book, a fee (default 1%) is deducted from the USDC side of the trade. For child projects, this fee is routed to the **Main DAO's ProjectTreasury** — the platform's primary revenue stream.

### Project Fee (Main DAO)

For the Main project itself, the conversion fee stays in its own treasury.

### Fee Configuration

The fee rate is a **global parameter** (`pobFeeBasisPoints`) stored on the `ProjectFactory`:
- Read by all `PrivateOrderBook` instances at trade time via `IFeeSource(feeSource).pobFeeBasisPoints()`
- Updated via `ProjectFactory.setPobFeeBasisPoints()`, controlled by the Main DAO through the `ProjectSettingGovernor`

## Dashboard Widget

The Treasury is visible on the project dashboard with:
- Real-time USD balance (ETH + stablecoins)
- NTT supply and ownership distribution
- Private Order Book status indicator
