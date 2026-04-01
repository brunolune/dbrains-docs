# Governance Parameters

Each governor has configurable voting parameters that can be changed democratically through governance.

## Parameters

| Parameter | Description |
|-----------|-------------|
| **Voting Delay** | Time between proposal creation and voting start |
| **Voting Period** | Duration of the voting window |
| **Quorum** | Minimum % of total NTT supply that must participate (default 4%) |
| **Early Execution Threshold** | % of total NTT supply voting FOR that short-circuits voting (default 60%) |

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
