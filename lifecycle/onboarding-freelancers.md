# Onboarding Freelancers

New talent joins a project through a democratic onboarding process governed by the `FreelancerGovernor`.

## The Workflow

### 1. Application (Off-Chain)

A candidate visits the project dashboard and clicks **"Apply to Join"**:

- A connected Web3 wallet is required
- The candidate submits their introduction, email, and social links (GitHub, LinkedIn, etc.)
- The application is stored in the PocketBase `freelancer_applications` collection

### 2. Review by DAO Members

Existing project members review applications in the **"Onboarding"** tab of the project dashboard:

- Applications are listed with candidate details
- Members can see the candidate's GitHub, LinkedIn, email, and introduction
- A one-click button drafts an onboarding proposal for any candidate

### 3. Governance Proposal

When a member clicks **"Create Onboarding Proposal"**, the frontend:

1. Creates a proposal with type `freelancer-onboarding`
2. Targets the `FreelancerGovernor`
3. Generates calldata for `ProjectMembershipSBT.safeMint(applicantAddress)`
4. Submits the proposal to governance

### 4. Vote

All project members (SBT holders) vote on the proposal:

- Voting uses NTT-weighted governance
- The standard voting period and quorum apply
- Early execution can fast-track if overwhelming consensus (default 60%) is reached

### 5. Execution & Membership

If the vote passes:

1. The proposal executes directly (no delay)
2. An SBT is minted to the new member's wallet
3. The new member is immediately recognized across the platform
4. They can now propose, vote, and participate in all project activities

## Key Points

- **No fee required** — Unlike project creation, freelancer onboarding has no application fee
- **Democratic** — The team decides who joins, not a single admin
- **Instant activation** — Membership is active the moment the SBT is minted
- **SBT-gated** — Only existing members can create onboarding proposals
