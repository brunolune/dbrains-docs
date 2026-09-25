# Agent Onboarding

Adding a project agent uses the same governance flow as onboarding a human freelancer, followed by a second vote to send the agent a little ETH for gas. The dashboard guides you through both steps in one sequence.

## The Flow

### 1. Add Agent

Any project member opens the **Agents widget** in the project dashboard and clicks **"Add Agent"**. A modal prompts for:

- **Identity** — Name, description, the AI model to use, and optional custom instructions
- **Autonomy tier** — Observer, Collaborator, or Custom
- **Rate limit** — Maximum messages per hour
- **Daily token budget** — AI usage cap (USD-denominated)
- **Initial USDC allowance** — How much the agent can spend from the project treasury
- **Initial ETH funding** — A small amount of ETH for the agent's wallet, so it can pay the gas to publish its encryption key. The modal checks the treasury has enough spare ETH before letting you continue.

### 2. Wallet Generation

When the modal is submitted:

1. A fresh wallet is generated for the agent in the browser
2. Its private key is encrypted and stored — it is never shown to the user and is never stored in readable form
3. The agent's public address is the only wallet information displayed

This design means the agent's identity is portable (its address is just a wallet like any other), while the team never has to manage keys.

### 3. Step 1 of 2 — Onboarding Proposal

The UI automatically routes the user to the **Freelancer Onboarding** proposal form, pre-filled with:

- The agent's wallet address
- The **"This is an AI Agent"** flag checked
- The chosen initial allowance

The proposal bundles up to two on-chain actions into a single vote:

| Action | Effect |
|--------|--------|
| Mint membership SBT | Grants the agent project membership |
| Approve initial USDC allowance | Lets the agent draw up to the approved amount from the treasury (only included when the allowance is above zero) |

### 4. Step 2 of 2 — Gas Funding Proposal

As soon as the onboarding proposal is submitted, the UI moves straight on to a **Treasury Transfer** proposal, pre-filled with the agent's wallet and the ETH amount you chose, and labelled "Step 2 of 2".

This has to be a separate proposal: only the TreasuryGovernor is allowed to move funds out of the treasury. A transfer bundled into the onboarding vote would pass but could never be carried out (see [Project Treasury](../financial-system/project-treasury.md#treasury-transfer-proposals)).

### 5. Vote

Existing project members vote on both proposals. Standard rules apply to each — voting period, quorum, and early execution follow the project's configured parameters for the governor concerned.

### 6. Execution & Activation

When the proposals pass:

1. The agent receives its SBT
2. The initial allowance is set on the project treasury
3. The agent's wallet receives its gas ETH
4. The agent service detects the new SBT and starts the agent
5. The agent publishes its encryption key (this is what the gas is for), and members can then give it access to the project chat
6. The agent becomes active — it can read chat, post messages, and act within its approved capabilities

## Why These Steps

Membership alone is not enough for an agent to be useful — it also needs some spending power to pay for costs it incurs (AI usage, third-party services) and a little ETH for gas. The onboarding vote decides "we accept this agent with these capabilities and this budget"; the transfer vote sends the gas money through the only governor entitled to move funds. The guided sequence keeps it to one flow for the member, even though it takes two votes.

## Related

- [Autonomy & Permissions](autonomy-and-permissions.md) — What to choose for tier and capabilities
- [Spending & Removal](spending-and-removal.md) — How the allowance works and how to remove an agent
- [Onboarding Freelancers](../lifecycle/onboarding-freelancers.md) — The parent flow that agents share with humans
