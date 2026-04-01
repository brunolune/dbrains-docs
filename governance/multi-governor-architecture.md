# Multi-Governor Architecture

DBrains uses a **timelock-free, multi-governor architecture** where each governor is a single-responsibility contract that handles a specific domain of decision-making.

## Design Philosophy

Traditional DAO architectures use a single governor with a timelock. DBrains takes a different approach:

- **No Timelock** — Proposals execute directly upon success. No queue/delay step. This simplifies UX while maintaining democratic decision-making.
- **Multiple Governors** — Instead of one governor handling everything, each domain has its own governor with tailored parameters.
- **Direct Execution** — When a vote passes, the action happens immediately.

## Universal Features

All governor contracts share these capabilities:

### Early Execution

If a proposal reaches a configurable threshold (default 60% of total NTT supply voting FOR) before the voting period ends, it can be executed immediately. This prevents unnecessary waiting when consensus is clear.

### SBT Gating

Only project members (SBT holders) can create proposals. This prevents spam and ensures only stakeholders participate in governance.

### Dynamic Thresholds

Proposal creation thresholds scale with token supply (1% in basis points), ensuring governance access scales naturally as the project grows.

## Governor Overview

| Governor | Domain |
|----------|--------|
| BacklogGovernor | Project roadmap |
| TaskGovernor | Task lifecycle |
| TreasuryGovernor | Project spending |
| FreelancerGovernor | Talent admission |
| InvestorGovernor | Investor onboarding |
| PrivateOrderBookGovernor | Internal NTT market |
| ProjectSettingGovernor | Governance config |
| ProjectFactoryGovernor | Platform expansion |

Each governor is detailed in the [Governors](governors.md) page.

## Why Multiple Governors?

1. **Separation of concerns** — Financial decisions have different risk profiles than task management
2. **Tunable parameters** — Each governor can have its own voting parameters suited to its domain
3. **Clear accountability** — Each governor has a well-defined scope of authority
4. **Parallel governance** — Multiple proposals in different domains can proceed simultaneously
