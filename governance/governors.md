# The Governors

Each project deploys 7 specialized governors. The Main DAO additionally uses the ProjectFactoryGovernor for platform-level decisions.

---

## BacklogGovernor

**Domain**: Project roadmap and direction

The BacklogGovernor is where the team collectively decides **what to build and when**. Members use it to propose features, improvements, or strategic directions — whether short-term fixes or long-term vision.

A backlog proposal should:

- **State the goal clearly** — What problem does this solve? What value does it bring?
- **Assess feasibility** — Is this realistic given the team's current capacity and skills?
- **Provide a time range** — Estimate how long the implementation will take
- **Break down into tasks** — Describe how the work can be split into concrete tasks, who would be assigned to each, and the NTT rewards associated with them

Proposals can be **refined** — a member can submit an improved version of a previous proposal, linking it to the original to track iteration history. This is useful when the team agrees on the direction but wants to adjust scope, timeline, or task breakdown.

**Example**: A member proposes "Add multi-language support to the platform" with a 3-week timeline, broken into 4 tasks: translation infrastructure (assigned to Alice, 200 NTT), frontend integration (Bob, 150 NTT), language file creation (Carol, 100 NTT), and testing (Dave, 50 NTT). The team votes, suggests refinements, and once approved the tasks can be formally created through the TaskGovernor.

---

## TaskGovernor

**Domain**: Day-to-day task operations

The TaskGovernor manages the lifecycle of individual tasks — the concrete units of work that come out of backlog proposals. Through it, the team creates tasks with clear assignees and NTT rewards, verifies completed work, and handles schedule changes.

- **Create tasks** — Turn approved backlog items into actionable tasks with deadlines and rewards
- **Verify tasks** — Once work is delivered, the team votes to confirm the task is complete, triggering automatic NTT reward minting to the assignee
- **Reschedule or cancel** — If circumstances change, the team can vote to adjust deadlines or cancel tasks that are no longer relevant

**Example**: Following the approved backlog proposal above, a member creates a task "Build translation infrastructure" assigned to Alice with a 1-week deadline and 200 NTT reward. When Alice delivers, the team reviews and votes to verify. Upon verification, 200 NTT are automatically minted to Alice's wallet.

---

## TreasuryGovernor

**Domain**: Project finances and administration

The TreasuryGovernor controls the project's treasury and holds the highest level of authority within the project. It governs how funds (ETH and stablecoins) are spent and can modify access control for the entire project.

- **Fund transfers** — Approve payments from the project treasury to external addresses
- **Access control** — Manage roles and permissions across the project's contracts
- **Administrative decisions** — Handle any structural changes to the project's governance setup

**Example**: The team votes to allocate 5,000 USDC from the treasury to cover hosting costs for the next quarter, sending the funds to the project's operational wallet.

---

## FreelancerGovernor

**Domain**: Team membership

The FreelancerGovernor handles the democratic admission of new talent into the project. When someone applies to join, existing members vote on whether to accept them.

- **Review applications** — Candidates submit their profile (skills, experience, links) through the platform
- **Vote on admission** — The team collectively decides who joins
- **Grant membership** — If approved, an SBT (membership token) is minted to the new member

**Example**: A developer applies to join the project with their GitHub profile and a short introduction. An existing member creates an onboarding proposal, the team reviews the candidate's background, and votes to accept. The new member receives their SBT and can immediately participate in governance.

---

## InvestorGovernor

**Domain**: Investor onboarding

The InvestorGovernor manages the process of admitting investors into the project. It combines membership approval with an NTT purchase in a single vote, holding the investor's USDC in escrow until the outcome is decided.

- **Escrow funds** — The investor's USDC is held securely until the vote concludes
- **Bundled approval** — A single vote grants membership and places the investor's buy order on the order book
- **Refund on rejection** — If the vote fails, the investor reclaims their full deposit

**Example**: An investor applies to join with a 10,000 USDC bid for NTTs. The funds are escrowed, the team votes to accept, and upon approval the investor receives membership and their buy order is placed on the order book. If a matching sell order exists, the trade fills automatically.

---

## PrivateOrderBookGovernor

**Domain**: Internal NTT market management

The PrivateOrderBookGovernor controls the project's internal market where NTTs can be traded. The team uses it to configure trading windows, set prices, and manage the project's own orders.

- **Open the order book** — Set the trading window (start and end dates), project ASK/BID prices, and NTT quantities
- **Close the order book** — End the trading window
- **Cancel project orders** — Remove standing project orders from the book

**Example**: The team votes to open the order book for two weeks, offering 1,000 NTT at an ASK price of 2 USDC per NTT to attract new investors.

---

## ProjectSettingGovernor

**Domain**: Governance configuration

The ProjectSettingGovernor allows the team to democratically adjust the voting parameters of all other governors — voting delay, voting period, quorum, and early execution threshold. Changes can be batched across multiple governors in a single proposal.

- **Tune governance parameters** — Adjust voting rules to match the project's evolving needs
- **Batch updates** — Modify parameters for several governors at once
- **Self-governance** — Can also modify its own parameters through a vote
- On the **Main project only**, also controls platform fees (application fee and POB transaction fee)

**Example**: As the project grows and decisions become more consequential, the team votes to increase the treasury governor's voting period and quorum to ensure broader participation on financial decisions.

---

## ProjectFactoryGovernor

**Domain**: Platform expansion (Main DAO only)

The ProjectFactoryGovernor is exclusive to the Main DAO and governs the creation of new projects on the platform. When someone applies to launch a project, Main DAO members vote on whether to approve it.

- **Review project applications** — Evaluate the project's mission, plan, and team
- **Approve deployment** — A successful vote triggers the automated deployment of the new project's full DAO infrastructure
- Applicants bypass standard proposal thresholds because they paid the USDC application fee

**Example**: A team applies to launch a "Decentralized Design Studio" project on DBrains, paying the 50 USDC application fee. Main DAO members review the proposal, vote to approve, and the project's contracts are automatically deployed.
