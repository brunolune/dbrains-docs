# The Governors

Each project deploys 7 specialized governors. The Main DAO additionally uses the `ProjectFactoryGovernor` for platform-level decisions.

---

## BacklogGovernor

**Domain**: Project roadmap and direction

- Manages high-level backlog proposals that define project priorities
- Supports **refined proposals** — versioning via `proposeRefinement`, linking to parent proposals with `parentId` to track iteration history

---

## TaskGovernor

**Domain**: Day-to-day task operations

- Controls the `TaskManager` contract
- Actions: create, verify, reschedule, and cancel tasks
- Task verification triggers automatic NTT reward minting

---

## TreasuryGovernor

**Domain**: Project finances

- Controls `ProjectTreasury` (ETH and ERC-20 transfers)
- Holds the **Admin role** on the project's `AccessManager`
- The most powerful governor — can modify access control for the entire project

---

## FreelancerGovernor

**Domain**: Team membership

- Onboards new freelancers by minting `ProjectMembershipSBT`
- Action: `SBT.safeMint(applicantAddress)`

---

## InvestorGovernor

**Domain**: Investor onboarding

- Handles investor applications with USDC escrow
- Bundles 3 actions in a single proposal: SBT mint + USDC approval + order book bid placement
- Includes refund mechanism for rejected proposals

---

## PrivateOrderBookGovernor

**Domain**: Internal NTT market management

- Controls the `PrivateOrderBook` contract
- Actions:
  - **Configure order book** — Set active window (start/end timestamps), project ASK/BID prices, and NTT quantities
  - **Close order book** — End the trading window
  - **Cancel project orders** — Remove standing project orders

---

## ProjectSettingGovernor

**Domain**: Governance configuration

- Democratically modifies voting parameters of all other governors
- Calls `updateSettings(votingDelay, votingPeriod, quorumNumerator, earlyExecThreshold)` on target governors
- Can batch parameter changes across multiple governors in a single proposal
- **Self-governance**: Can modify its own parameters via `updateOwnSettings()` (protected by `onlyGovernance`)
- On the **Main project only**, also controls platform fees (application fee and POB transaction fee)

---

## ProjectFactoryGovernor

**Domain**: Platform expansion (Main DAO only)

- Democratizes the creation of new projects on the platform
- Executes `ProjectFactory.createProject(appId)` to deploy full DAO infrastructure
- Only members of the Main DBrains DAO can vote
- Applicants bypass standard proposal thresholds because they paid the USDC application fee
