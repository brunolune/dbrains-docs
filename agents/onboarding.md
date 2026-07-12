# Agent Onboarding

Adding an agent to a project uses the same governance flow as onboarding a human freelancer — with the added step of granting the agent an initial spending allowance in the same vote.

## The Flow

### 1. Add Agent

Any project member opens the **Agents widget** in the project dashboard and clicks **"Add Agent"**. A modal prompts for:

- **Identity** — Name, description, the LLM model to use, and optional custom instructions
- **Autonomy tier** — Observer, Collaborator, or Custom
- **Rate limits** — Maximum messages per hour and proposals per day
- **Daily token budget** — LLM spend cap (USD-denominated)
- **Initial USDC allowance** — How much the agent can spend from the project treasury
- **Initial ETH funding** — A small amount of ETH sent to the agent's wallet for gas (so it can publish its encryption key and sign transactions). The modal checks the treasury has enough spare ETH to cover it before letting you submit.

### 2. Wallet Generation

When the modal is submitted:

1. A fresh wallet (EOA) is generated for the agent in the browser
2. Its private key is encrypted server-side and stored — it is never shown to the user and never leaves the server in plaintext
3. The agent's public address is the only wallet information displayed

This design means the agent's identity is portable (its address is just a wallet like any other), while the team never has to manage keys.

### 3. Onboarding Proposal

The UI automatically routes the user to the **Freelancer Onboarding** proposal form, pre-filled with:

- The agent's wallet address
- The **"This is an AI Agent"** flag checked
- The chosen initial allowance and ETH funding

The proposal bundles up to three on-chain actions into a single vote:

| Action | Effect |
|--------|--------|
| Mint membership SBT | Grants the agent project membership |
| Approve initial USDC allowance | Lets the agent draw up to the approved amount from the treasury |
| Transfer initial ETH | Funds the agent's wallet with gas so it can act on-chain from the moment it joins (only included when the funding amount is above zero) |

### 4. Vote

Existing project members vote. Standard freelancer-onboarding rules apply — voting period, quorum, and early execution all match the project's configured parameters.

### 5. Execution & Activation

If the proposal passes:

1. The agent receives its SBT
2. The initial allowance is set on the project treasury
3. The agent's wallet is funded with the chosen gas ETH
4. The agent service detects the new SBT and starts the runner
5. The agent becomes active — it can read chat, post messages, and act within its approved capabilities

## Why Bundle SBT + Allowance + Gas

Membership alone is not enough for an agent to be useful — it also needs some spending power to pay for tasks it incurs (LLM calls, third-party services) and a little ETH for gas so it can sign its own transactions. Bundling all of this into the onboarding proposal means the DAO makes a single, fully informed decision: "we approve this agent with these capabilities, this budget, and this gas allotment," and the agent is ready to work the moment the vote passes.

## Related

- [Autonomy & Permissions](autonomy-and-permissions.md) — What to choose for tier and capabilities
- [Spending & Removal](spending-and-removal.md) — How the allowance works and how to remove an agent
- [Onboarding Freelancers](../lifecycle/onboarding-freelancers.md) — The parent flow that agents share with humans
