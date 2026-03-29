# Governance Parameters

Each governor has configurable voting parameters that can be changed democratically through the `ProjectSettingGovernor`.

## Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| **Voting Delay** | Time between proposal creation and voting start | 1 minute |
| **Voting Period** | Duration of the voting window | 5-10 minutes (per governor) |
| **Quorum** | Minimum % of total NTT supply that must participate | 4% |
| **Early Execution Threshold** | % of total NTT supply voting FOR that short-circuits voting | 60% |

## How to Change Parameters

1. A DAO member navigates to **Proposals > Governance / Config**
2. The form displays all 6 project governors with their **current on-chain values**
3. The member modifies the desired parameters
4. A proposal is submitted to the `ProjectSettingGovernor`
5. Members vote on the changes
6. If passed, new parameters take effect **immediately** upon execution

### Batch Updates

The `ProjectSettingGovernor` supports multi-target proposals. A single vote can update parameters across multiple governors simultaneously. For example, you could increase the voting period for both the `TreasuryGovernor` and the `BacklogGovernor` in one proposal.

## Platform Fee Configuration (Main DAO Only)

On the Main DBrains project, the governance config form also includes **Platform Fees**:

| Fee | Target | Default |
|-----|--------|---------|
| Project creation fee | `ProjectFactory.setFeeAmount()` | 50 USDC |
| POB transaction fee | `ProjectFactory.setPobFeeBasisPoints()` | 1% (100 basis points) |

These fees are global parameters that affect all projects on the platform and can only be changed by the Main DAO through governance.

## Design Considerations

- **Short voting periods** are used during development (5-10 minutes). Production deployments will use longer periods for critical decisions.
- **Early execution** prevents unnecessary waiting when consensus is clear, while still protecting against rushed decisions below the threshold.
- **Quorum** ensures sufficient participation — proposals that pass with very low turnout can be problematic.
