# Private Order Book

The `PrivateOrderBook` (POB) is a two-sided, dual-currency order book for NTT conversions, tightly integrated with the `ProjectTreasury`. It provides the mechanism for converting NTTs to USDC or ETH and vice versa.

## Core Mechanics

### Order Types

- **ASK orders** (sell NTTs) — Members offer their NTTs at a specified price, denominated in either USDC or ETH
- **BID orders** (buy NTTs) — Members deposit USDC or ETH to purchase NTTs at a specified price

### Currency Siloing

Orders only match other orders in the **same currency** — a USDC ASK does not fill against an ETH BID. The two currencies form parallel books inside the same contract. This keeps pricing clear and avoids hidden conversion risk at trade time.

### Non-Transferable Trading

Since NTTs cannot be transferred between wallets, every trade uses a **burn + remint** mechanism:

1. Seller's NTTs are **burned**
2. New NTTs are **minted** to the buyer
3. The buyer's payment is transferred to the seller (minus platform fee)

### Partial Fills

Orders can be partially filled. If a BID for 100 NTTs finds an ASK for only 50, the first 50 are traded and the remaining BID stays open.

## Trade Flows

### Buying NTTs

```
Buyer pays (USDC or ETH) → Treasury keeps fee → Seller's NTTs burned → New NTTs minted to buyer
```

### Selling NTTs

```
Seller's NTTs burned → Escrowed funds minus fee → Seller receives USDC or ETH
```

### Automated Investor Matching

When the `InvestorGovernor` places a bid on behalf of an approved investor, the contract automatically checks for a matching project ASK order **in the same currency**:

- If `projectAsk.price <= investorBid.price`, the fill executes atomically
- Surplus (bid > ask) is automatically refunded to the investor

## DAO-Controlled Scheduling

The `PrivateOrderBookGovernor` votes to configure the order book:

```
configureOrderBook(
  startTime, endTime,
  askPrice, askAmount, askCurrency,
  bidPrice, bidAmount, bidCurrency
)
```

This sets:

- **Active window** — When trading is allowed (start/end timestamps)
- **Project ASK** — Price, quantity, and currency of the NTTs the project is selling (mints new supply)
- **Project BID** — Price, quantity, and currency of the NTTs the project wants to buy back (burns supply)
- Auto-cancels any previously active project orders

The project ASK and BID can each be denominated in a different currency — e.g. the project can sell NTTs for USDC while buying NTTs back with ETH.

### Order Book Status

The dashboard displays the POB status dynamically:

- **Open** — Currently within the active window
- **Scheduled** — Future start time set
- **Closed** — No active window or past end time

## Price Safety

Project orders (ASK and BID placed by the DAO) are protected by a **price deviation bound**: a proposal to open the order book with a price far off the last fill price is automatically rejected. This is especially important given that AI agents can draft and propose order book configurations — the bound prevents a subtly mispriced proposal from quietly draining the treasury.

The bound is configurable through governance, and can be widened temporarily for strategic off-market orders when the team deliberately chooses to do so.

## Supply Control

The DAO controls NTT supply through project orders:

| Order Type | Effect |
|------------|--------|
| Project ASK | Selling NTTs → mints new supply (dilution) → revenue to Treasury |
| Project BID | Buying NTTs → burns supply (buyback) → funded by Treasury |

## Access Control

- **SBT Gating** — Only project members can place and fill orders
- **Investor Entry** — For non-members, the `InvestorGovernor` can place an investor bid as part of onboarding

## Safety (Pausable)

The Guardian can **pause** the market in emergencies:

- Freezes new orders, fills, and matching
- `cancelOrder` remains active — members can always withdraw their escrowed funds in the original currency
- Only the Guardian can unpause
