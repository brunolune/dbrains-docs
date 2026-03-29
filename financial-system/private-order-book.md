# Private Order Book

The `PrivateOrderBook` (POB) is a two-sided order book for NTT conversions, tightly integrated with the `ProjectTreasury`. It provides the mechanism for converting NTTs to stablecoins and vice versa.

## Core Mechanics

### Order Types

- **ASK orders** (sell NTTs) — Members offer their NTTs at a specified USDC/NTT price
- **BID orders** (buy NTTs) — Members deposit USDC to purchase NTTs at a specified price

### Non-Transferable Trading

Since NTTs cannot be transferred between wallets, every trade uses a **burn + remint** mechanism:

1. Seller's NTTs are **burned**
2. New NTTs are **minted** to the buyer
3. USDC is transferred from buyer to seller (minus platform fee)

### Partial Fills

Orders can be partially filled. If a BID order for 100 NTTs finds an ASK for only 50, the first 50 are traded and the remaining BID stays open.

## Trade Flows

### Buying NTTs

```
Buyer pays USDC → Treasury keeps fee → Seller's NTTs burned → New NTTs minted to buyer
```

### Selling NTTs

```
Seller's NTTs burned → Escrowed USDC minus fee → Seller receives USDC from Treasury
```

### Automated Investor Matching

When `placeInvestorBidOrder` is called by the `InvestorGovernor`, the contract automatically checks for a matching project ASK order:
- If `projectAsk.price <= investorBid.price`, the fill executes atomically
- Surplus USDC (bid > ask) is automatically refunded to the investor

## DAO-Controlled Scheduling

The `PrivateOrderBookGovernor` votes to configure the order book:

```
configureOrderBook(startTime, endTime, askPrice, askNTTAmount, bidPrice, bidNTTAmount)
```

This sets:
- **Active window** — When trading is allowed (start/end timestamps)
- **Project ASK** — Price and quantity of NTTs the project is selling (mints new supply)
- **Project BID** — Price and quantity of NTTs the project wants to buy back (burns supply)
- Auto-cancels any previously active project orders

### Order Book Status

The dashboard displays the POB status dynamically:
- **Open** — Currently within the active window
- **Scheduled** — Future start time set
- **Closed** — No active window or past end time

## Supply Control

The DAO controls NTT supply through project orders:

| Order Type | Effect |
|------------|--------|
| Project ASK | Selling NTTs → mints new supply (dilution) → revenue to Treasury |
| Project BID | Buying NTTs → burns supply (buyback) → funded by Treasury |

## Access Control

- **SBT Gating** — Only project members can place and fill orders
- **Investor Entry** — For non-members, the `InvestorGovernor` can call `placeInvestorBidOrder` as part of onboarding

## Safety (Pausable)

The Guardian can **pause** the market in emergencies:
- Freezes new orders, fills, and matching
- `cancelOrder` remains active — members can always withdraw their escrowed USDC
- Only the Guardian can unpause
