# Projects

Projects are the core units of collaboration on DBrains. Each project operates as its own fully autonomous DAO with dedicated smart contracts, treasury, and governance.

## Project Types

### Funded Projects

A project launcher defines milestones and deposits funds into escrow. Payments unlock as milestones are completed. Remuneration is based on earned NTT — the more you contribute, the larger your share of the milestone payment.

### Free Projects

Community-driven, holacratic development without upfront funding. Remuneration is based on profit share proportional to NTT holdings. If the project generates revenue, NTT holders earn their proportional cut.

## What Gets Deployed

When a project is created, the `ProjectFactory` deploys a complete DAO infrastructure:

| Contract | Purpose |
|----------|---------|
| 7 Governors | Democratic governance for different domains |
| NTToken (NTT) | Non-transferable contribution token |
| ProjectMembershipSBT | Soul-bound membership token |
| PrivateOrderBook | Internal NTT market |
| ProjectTreasury | Fund custody and management |
| AccessManager | Role-based permission control |

## Project Metadata

Each project stores structured metadata in PocketBase:

- **Title** and **Tagline**
- **Description / Mission**
- **Problem Solved**
- **Tokenomics** plan
- **Tech Stack**
- **Roadmap**
- **Website** and **Social Links**
- **Contact Email** (private, admin-only)

## The Factory Model

All projects are launched through the `ProjectFactory` — a singleton contract owned by the Main DBrains DAO. The factory:

- Collects the application fee (default 50 USDC)
- Manages the application lifecycle
- Delegates deployment to the `ProjectDeployer` library
- Tracks all deployed project addresses

The factory itself is never redeployed per project. Only the child project contracts (governors, tokens, treasury, etc.) are created fresh for each new project.
