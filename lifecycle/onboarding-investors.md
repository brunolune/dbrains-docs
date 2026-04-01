# Onboarding Investors

Investors join a project through an automated workflow that combines membership approval with an immediate NTT purchase — all in a single governance vote.

## The Workflow

### 1. Application

An investor opens the **Investor Application Modal** from the project dashboard:

- Enters their metadata (introduction, contact info)
- Specifies the **requested NTT amount** and a **reference price** (based on current ASK/BID pricing)
- The modal shows real-time POB pricing and calculates the total USDC cost automatically

### 2. USDC Escrow

When the investor submits their application:

- The total USDC cost is pulled from the investor's wallet and held in escrow
- Funds remain locked until the governance vote concludes
- The investor can track their application status in the UI

### 3. Bundled Governance Proposal

A single proposal is created with **3 bundled actions**:

| Action | Purpose |
|--------|---------|
| Mint membership token | Grants project membership via SBT |
| Approve USDC transfer | Allows the Private Order Book to use the escrowed USDC |
| Place BID order | Places a BID order on the order book on behalf of the investor |

### 4. Vote

Project members vote on the investor onboarding proposal:

- Visible as an investor onboarding proposal in the governance board
- Standard voting parameters apply

### 5. Execution

If the vote passes:

1. The investor receives their SBT (project membership)
2. Their BID order is immediately placed on the Private Order Book
3. If a matching project ASK order exists, the trade fills automatically
4. Any surplus USDC (if bid price > ask price) is refunded to the investor

### Refund on Rejection

If the proposal is defeated or canceled, the investor can reclaim their full escrowed USDC. No funds are lost.

## Key Points

- **Single vote** — Membership and investment are approved together
- **Automatic matching** — If the project has an ASK order at or below the bid price, the trade executes atomically
- **Safe escrow** — Funds are only released if the vote passes; otherwise fully refundable
- **Order book must be open** — Applications are only possible while the project's Private Order Book is active
