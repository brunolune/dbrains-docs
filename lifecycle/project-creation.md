# Project Creation

Launching a new project on DBrains is a democratic process that combines an application fee with community governance.

## The Process

### Step 1: Application

The project creator submits an application through the platform UI:

1. **Connect wallet** — A Web3 wallet is required
2. **Fill metadata** — Title, description, mission, tokenomics plan, tech stack, roadmap, etc.
3. **Approve USDC** — Approve the application fee (default 50 USDC, configurable by the Main DAO)
4. **Submit** — The application is stored in the database and recorded on-chain

### Step 2: Governance Vote

The application becomes visible in the Main DAO's proposals list:

* **Who can propose**: Because the applicant paid the USDC fee, they are immediately granted permission to propose project creation — bypassing the standard minimum token threshold (anti-spam via economic cost rather than token ownership)
* **Who can vote**: Only Main DBrains DAO members (Community SBT holders) can vote on new project approvals

### Step 3: Automated Deployment

If the proposal passes, execution triggers the automated deployment of the new project:

1. All the project's DAO contracts are deployed (governors, token, membership, order book, treasury, and access control)
2. The creator receives an SBT (project membership)
3. Optional: initial members and NTT allocations can be specified

### Output

A fully configured DAO with democratic governance, a treasury, an internal market, and role-based access control — all owned by the creator and members, with the Main DAO retaining a Guardian role.

## Cost

* **Application fee**: 50 USDC (configurable by the Main DAO)
* **Gas**: Deployment costs are covered by the executor of the passed proposal
