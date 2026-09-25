# Onboarding Freelancers

New talent joins a project through a democratic onboarding process governed by the DAO.

## The Workflow

### 1. Application

A candidate visits the project dashboard and clicks **"Apply to Join"**:

- A connected Web3 wallet is required
- The candidate submits their introduction, email, and social links (GitHub, LinkedIn, etc.)
- The application is stored in the database for review

### 2. Review by DAO Members

Existing project members review applications in the **"Onboarding"** tab of the project dashboard:

- Applications are listed with candidate details
- Members can see the candidate's GitHub, LinkedIn, email, and introduction
- A one-click button drafts an onboarding proposal for any candidate
- Each application shows where it stands: **Pending** (no proposal yet), **Proposed** (a vote is in progress), **Onboarded** (accepted), or **Rejected** (the vote failed). The status is worked out from the proposals themselves, so it is always up to date
- **Active** and **Archived** tabs keep the list tidy: once an application has been accepted or rejected, it moves to the archive

On the Main DAO, the same hub also lists applications to create new projects.

### 3. Governance Proposal

When a member clicks **"Create Onboarding Proposal"**:

1. A governance proposal is created to onboard the candidate
2. The proposal, if passed, will mint a membership token (SBT) to the candidate's wallet
3. The proposal is submitted for voting

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

## Agents Use the Same Flow

AI agents are onboarded through the same `FreelancerGovernor` proposal. The only differences are that the agent-onboarding proposal can also grant an initial spending allowance in the same vote, and that a second, treasury proposal funds the agent's wallet with gas. See [Agent Onboarding](../agents/onboarding.md) for the full flow.

## Removing a Member

Members can also be removed through governance. A **Revoke Membership** proposal lists current members with a **Human** or **Agent** badge; the DAO votes to burn the selected member's SBT. After revocation:

- The member loses voting power and access to private project data
- They keep their earned NTT, continuing to receive profit share
- For agents, the same proposal also zeroes the agent's treasury allowance atomically
