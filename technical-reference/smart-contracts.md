# Smart Contracts

## Framework

DBrains smart contracts are built on the **OpenZeppelin Governor** framework with significant customizations:
- Timelock-free execution
- Early execution threshold
- SBT-gated proposal creation
- Dynamic proposal thresholds

## Token Standards

| Token | Standard | Modifications |
|-------|----------|---------------|
| NTToken (NTT) | ERC-20 | Transfer restrictions (non-transferable), burn/mint controlled by AccessManager |
| ProjectMembershipSBT | ERC-721 | Non-transferable, one per member per project |

## Architecture

### UUPS Upgradeable Proxies

All project contracts use the **Universal Upgradeable Proxy Standard (UUPS)**. This means:
- Each contract is deployed as a minimal proxy pointing to a shared implementation
- Upgrades are possible through governance (controlled by the TreasuryGovernor)
- Implementation contracts are deployed once; proxies are cheap to create

### Deployed Library Pattern

The `ProjectDeployer` is a library with `public` functions. In Solidity, public library functions are deployed as separate contracts and invoked via `DELEGATECALL`. This pattern:
- Keeps `ProjectFactory` bytecode small (~8.5KB, well under the EIP-170 24KB limit)
- Moves the heavy deployment logic (~17.9KB) into a separately deployed library
- Foundry handles library deployment and linking automatically

### Contract Inventory

A full redeployment creates approximately **30 contracts**:
- 11 implementation contracts (governors, tokens, treasury, order book, task manager)
- `ProjectDeployer` library
- `ProjectFactory` (implementation + proxy)
- `ProjectFactoryGovernor` (implementation + proxy)
- Main DAO project (12 proxies + AccessManager)
- Mock USDC (testnet only)

## Network

- **Development/Testing**: Sepolia testnet
- **Production target**: Layer 2 (Base, Polygon, or similar)

## Key Contracts

### ProjectFactory

The singleton factory contract (~8.5KB):
- `applyForProject(metadataURI)` — Submit a project application (pays USDC fee)
- `createProject(appId)` — Deploy full DAO infrastructure (called by ProjectFactoryGovernor)
- `bootstrapMainProject()` — Owner-only, deploys the Main DAO
- `setFeeAmount(amount)` — Update application fee
- `setPobFeeBasisPoints(bps)` — Update global POB fee

### TaskManager

The execution engine for task-based work:
- `createTask(proposalId, description, assignee, reward, start, end)` — Create a new task
- `verifyTask(taskId)` — Mark complete and mint NTT rewards
- `rescheduleTask(taskId, newStart, newEnd)` — Adjust timeline
- `cancelTask(taskId)` — Cancel a task

### PrivateOrderBook

Two-sided NTT market:
- `placeAskOrder(price, amount)` — Sell NTTs
- `placeBidOrder(price, amount)` — Buy NTTs
- `fillOrder(orderId, amount)` — Fill an existing order
- `cancelOrder(orderId)` — Cancel and refund
- `configureOrderBook(...)` — DAO sets trading window and project orders
- `placeInvestorBidOrder(...)` — Restricted; called by InvestorGovernor

### ProjectTreasury

Lightweight fund custody:
- `receive()` — Accept ETH
- `transferETH(to, amount)` — Send ETH (governed)
- `transferERC20(token, to, amount)` — Send tokens (governed)

## Address Management

All deployed contract addresses are managed in `web/src/lib/contracts.ts`. The `redeploy.sh` script automatically updates this file after deployment.

> **Important**: All addresses passed to contract calls must be full 42-character hex strings with valid EIP-55 checksums. Use `viem`'s `getAddress()` for normalization.
