# Tokenomics

DBrains uses two types of tokens to manage membership, governance, and value distribution.

## NTT (Non-Transferable Tokens)

NTT is the core economic token of each project. It is an ERC-20 token with transfer restrictions.

### Key Properties

* **Project-specific** — Each project has its own NTT contract
* **Bound to a member** — NTTs are tied to the wallet that earned them
* **Non-transferable** — Cannot be sent between wallets or traded on public markets
* **Represents voting power** — Used to vote on governance proposals (while the holder keeps their SBT)
* **Represents profit share** — Proportional claim on project revenue

### How NTTs Are Earned

NTTs are minted as rewards when a task is verified by the DAO. The amount is determined during the task proposal phase. The people behind a validated backlog or roadmap proposal can also earn NTT through [Idea Rewards](../lifecycle/idea-rewards.md), so good ideas are rewarded alongside the work that carries them out. A project's founders can also earn additional NTT through [Creator Rewards](../lifecycle/project-creation.md#creator-rewards) — a time-limited bonus tied to the project's activity.

### How NTTs Are Converted

Since NTTs cannot be freely transferred, conversions happen through the project's **Private Order Book**:

1. A member places an ASK order (offering NTTs at a price)
2. A buyer places a BID order (offering USDC or ETH for NTTs)
3. When orders match, the seller's NTTs are **burned** and new NTTs are **minted** to the buyer
4. The seller receives the payment minus a platform fee

This burn-and-remint mechanism ensures NTTs remain non-transferable while still being convertible to real value.

### Burning and Value

When NTTs are burned (converted to currency), the remaining holders' tokens become more valuable — they now represent a larger share of the project's total supply. This creates natural deflationary pressure.

### Voting Power vs Profit Share

NTTs carry two benefits, but they activate differently:

- **Voting power** requires the holder to also hold a project SBT. If the SBT is revoked, voting power goes to zero even though NTTs remain in the wallet. Voting power is **sublinear** in NTT balance — see below.
- **Profit share** does not require an SBT. It is strictly **linear pro-rata** to the holder's NTT balance. A revoked member keeps their NTTs and continues to earn a proportional share of project revenue until those NTTs are converted.

This separation ensures that members who contributed are never retroactively stripped of their earned share, while access to governance remains tied to active membership.

### Sublinear Voting Power

Voting power does not scale one-to-one with NTT balance. It follows a **sublinear curve** tuned by a governance parameter **α** (alpha) between 0 and 1:

- At **α = 1**, voting power equals NTT balance (purely linear).
- At **α < 1**, each additional NTT yields slightly less voting power than the previous one. The merit signal is preserved — bigger contributors still have more say — but marginal influence flattens as holdings grow.
- The **default is α = 0.7**, which neutralises solo-takeover risk (e.g. an investor accumulating a majority of supply through the order book) while keeping meaningful differentiation between contributor tiers.

α is tunable by the DAO through the same configuration process as other governance parameters (see [Governance Parameters](../governance/parameters.md)). Each proposal locks in the α that was in force at its creation, so an in-flight vote is never re-weighted mid-stream.

Profit share is **not** affected by α — it remains linear in NTT balance. Only voting weight is curved.

## SBT (Soul-Bound Tokens)

SBTs are ERC-721 tokens that are non-transferable and serve as identity and access control mechanisms.

### Project SBT

* Represents membership in a specific project
* Required to propose and vote within that project's governance
* Required to place orders on the project's Private Order Book
* Minted when a freelancer, investor, or AI agent is onboarded through governance
* Gates access to encrypted content — only current SBT holders can decrypt private proposals and chat (see [Access Control](../governance/access-control.md#sbt-as-access-control))

### Revocation

A member can be removed from a project through a governance vote that burns their SBT. After revocation:

- The former member loses voting power and access to private project data
- Their earned NTT stays in their wallet for ongoing profit share
- They keep **sell-side access to the Private Order Book** so they can exit their NTT position if they choose — surfaced via a dedicated **Sell NTT** panel on the My Holdings page. Buy-side access is blocked, so a revoked member cannot purchase their way back into the project.
- For AI agents, the same proposal also zeroes the agent's spending allowance atomically
