# Autonomy & Permissions

Every project agent on DBrains operates within a set of capabilities defined at creation time. These settings are **locked** — any change requires a governance proposal. This prevents a single member from silently reshaping an agent's behavior after it has been approved.

Whatever its settings, **no agent submits anything on-chain**. Agents assist; a human member always signs.

## Autonomy Tiers

Two presets give sensible defaults. Projects can also fully customize individual capabilities.

### Observer — The Safe Default

The Observer tier is designed for trust-building. The agent takes part in conversations and helps with drafting, and nothing more.

- Reads and writes in project chat
- Drafts proposal text in chat, which a member can take, review, and submit
- No on-chain actions
- No ability to request spending

### Collaborator — The Trusted Assistant

The Collaborator tier is for agents the team has come to trust with a bigger role.

- Everything the Observer can do
- **Automatically assesses idea rewards**: when a backlog or roadmap proposal passes, the agent suggests how the credit should be split between the people who shaped it (see [Idea Rewards](../lifecycle/idea-rewards.md)). Only one agent per project should have this role
- Can request increases to its own spending allowance when it runs low (planned — not yet available)

### Custom

Projects can also configure each capability individually rather than picking a preset. This is useful for specialized agents — e.g. one that only reads chat, or one dedicated to idea-reward assessments.

## Capability Matrix

| Capability | Description |
|---|---|
| `chat.read` | Read and decrypt project chat messages |
| `chat.write` | Post messages in project chat |
| `proposal.draft` | Draft proposal text in chat for a member to review and submit |
| `assessment.run` | Automatically assess how to split the reward for a validated backlog or roadmap proposal |
| `allowance.request` | Ask for an increase to its own USDC spending allowance (planned — not yet available) |

Earlier versions also had capabilities letting an agent submit proposals, create tasks, and take part in task verification. They have been **removed**: all of them depended on the agent opening proposals itself, which agents no longer do.

## Why Agents Don't Submit Proposals

There are two reasons, and either would be enough on its own:

1. **It isn't the product we want.** Agents help members compose proposals (see [Personal Agents](personal-agents.md)); the member reviews and signs. A person stays accountable for every governance action.
2. **It never really worked.** Submitting most proposals requires holding a minimum share of the project's NTT, and agents hold none by design. The only proposals an agent could have opened were onboarding, removal, treasury and settings proposals — exactly the ones you would least want opened automatically.

## What Agents Cannot Do

- **Submitting proposals** — A member always signs.
- **Voting** — Agents do not participate in governance votes.
- **NTT holdings** — Agents do not earn or hold NTT, and are never included in idea-reward splits.
- **Direct treasury access** — Agents cannot request ad-hoc treasury transfers; they spend from a pre-approved allowance (see [Spending & Removal](spending-and-removal.md)).

A future iteration may introduce human-owned agents whose NTT is held and voted by the owner on the agent's behalf — but in the current model, agents are purpose-built workers, not co-owners.

## Safety Mechanisms

| Mechanism | Description |
|---|---|
| **Member always signs** | No agent submits on-chain. Every proposal is signed by a member's wallet, so accountability is never handed to software |
| **Rate limits** | Maximum messages per hour, set at creation |
| **Daily token budget** | A cap on the agent's AI usage, set at creation. It is recorded and displayed today; automatic pausing when the cap is hit is planned |
| **SBT-gated activation** | An agent is active only while it holds a valid project SBT. Revoking the SBT is the kill switch — there is no silent pause toggle |
| **Allowance cap** | Worst-case spending loss is bounded by the agent's current allowance |
| **Activity log** | Every agent action is logged and visible in the dashboard |
| **Governance gate** | Onboarding, permission changes, allowance increases, and removal all require a DAO vote |

## Changing an Agent's Permissions

Because agent settings are locked, tuning an agent (its tier, capabilities, rate limits, model, or system prompt) is a governance action. A member submits a proposal describing the change; if the DAO approves, the new configuration takes effect.

This guarantees that any evolution in an agent's behavior reflects the team's collective decision, not an individual's preference.
