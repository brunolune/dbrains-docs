# Governance Parameters

Each governor has configurable voting parameters that can be changed democratically through governance.

## Parameters

| Parameter | Description |
|-----------|-------------|
| **Voting Delay** | Time between proposal creation and voting start |
| **Voting Period** | Duration of the voting window |
| **Quorum** | Minimum % of total voting power that must participate (default 4%) |
| **Early Execution Threshold** | % of total voting power voting FOR that short-circuits voting (default 60%) |
| **Voting Power Curve (α)** | Exponent applied to NTT balance to derive voting power (default 0.7) — see [Tokenomics](../core-concepts/tokenomics.md#sublinear-voting-power) |

## How to Change Parameters

1. A DAO member navigates to **Proposals > Governance / Config**
2. The form displays all 6 project governors with their **current on-chain values**
3. The member modifies the desired parameters
4. A proposal is submitted for voting
5. Members vote on the changes
6. If passed, new parameters take effect **immediately** upon execution

### Batch Updates

A single governance vote can update parameters across multiple governors simultaneously. For example, you could increase the voting period for both the treasury and backlog governors in one proposal.

## Platform Fee Configuration (Main DAO Only)

On the Main DBrains project, the governance config form also includes **Platform Fees**:

| Fee | Default |
|-----|---------|
| Project creation fee | 50 USDC |
| POB transaction fee | 1% (100 basis points) |

These fees are global parameters that affect all projects on the platform and can only be changed by the Main DAO through governance.

## Design Considerations

- **Early execution** prevents unnecessary waiting when consensus is clear, while still protecting against rushed decisions below the threshold.
- **Quorum** ensures sufficient participation — proposals that pass with very low turnout can be problematic.
- **Voting power curve (α)** lets the DAO trade off between rewarding contribution and resisting concentration. Lower α further flattens the influence of large holders; α closer to 1 sharpens the merit signal. Lowering α also makes the SBT onboarding gate more load-bearing, since splitting a balance across identities becomes more valuable under any sublinear curve.
