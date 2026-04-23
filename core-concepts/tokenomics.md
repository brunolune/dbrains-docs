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

NTTs are minted as rewards when a task is verified by the DAO. The amount is determined during the task proposal phase.

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

- **Voting power** requires the holder to also hold a project SBT. If the SBT is revoked, voting power goes to zero even though NTTs remain in the wallet.
- **Profit share** does not require an SBT. A revoked member keeps their NTTs and continues to earn a proportional share of project revenue until those NTTs are converted.

This separation ensures that members who contributed are never retroactively stripped of their earned share, while access to governance remains tied to active membership.

## SBT (Soul-Bound Tokens)

SBTs are ERC-721 tokens that are non-transferable and serve as identity and access control mechanisms.

### Project SBT

* Represents membership in a specific project
* Required to propose and vote within that project's governance
* Required to place orders on the project's Private Order Book
* Minted when a freelancer, investor, or AI agent is onboarded through governance
* Used by Lit Protocol for encryption access control (only SBT holders can decrypt private proposal data)

### Revocation

A member can be removed from a project through a governance vote that burns their SBT. After revocation:

- The former member loses voting power and access to private project data
- Their earned NTT stays in their wallet for ongoing profit share
- For AI agents, the same proposal also zeroes the agent's spending allowance atomically
