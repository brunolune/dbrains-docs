# Access Control & Roles

Each project uses an OpenZeppelin `AccessManager` contract to manage permissions. Roles are set up automatically during project deployment and control which contracts can call which functions.

## Role Matrix

| Role | ID | Holder | Permission |
|------|----|--------|------------|
| **Admin** | 0 | TreasuryGovernor | Full AccessManager control |
| **Minter** | 1 | TaskManager, PrivateOrderBook | `NTToken.mint()` |
| **Order Creator** | 2 | PrivateOrderBookGovernor | `PrivateOrderBook.openOrderBook / closeOrderBook / cancelOrder` |
| **Pauser** | 3 | Guardian (deployer) | `PrivateOrderBook.pause / unpause` |
| **Task Admin** | 4 | TaskGovernor | `TaskManager.createTask / verifyTask / rescheduleTask / cancelTask` |
| **Treasury Admin** | 5 | TreasuryGovernor | `ProjectTreasury.transferETH / transferERC20` |
| **Burner** | 6 | PrivateOrderBook | `NTToken.burnFrom` |
| **Investor POB** | 8 | InvestorGovernor | `PrivateOrderBook.placeInvestorBidOrder` |
| **Guardian** | 999 | Deployer / Main DAO | Admin over Minter role |

## How It Works

### Automatic Setup

When a project is deployed through the `ProjectDeployer` library:

1. An `AccessManager` is created for the project
2. All roles are defined and assigned to the appropriate contracts
3. Function-level permissions are set (e.g., only the `TaskGovernor` can call `createTask`)
4. The **Admin role** is transferred to the `TreasuryGovernor`
5. The deployer renounces its temporary admin role

### Role Separation

The role system ensures strict separation of concerns:

- The **TaskManager** can mint NTT rewards but cannot spend treasury funds
- The **PrivateOrderBook** can mint and burn NTTs (for trades) but cannot create tasks
- The **TreasuryGovernor** can spend funds and modify access control, but only through governance votes
- The **Guardian** can only pause/unpause the order book — a safety mechanism, not a governance override

### SBT as Access Control

Beyond the `AccessManager`, project membership SBTs serve as a broader access control layer:

- **Proposing**: Only SBT holders can create governance proposals
- **Voting**: Only SBT holders can vote
- **Trading**: Only SBT holders can place orders on the Private Order Book
- **Decryption**: Only SBT holders can decrypt private proposal data (via Lit Protocol)

## Guardian Decentralization (Future)

The current Guardian assignment to the deployer wallet is a temporary bootstrapping measure. Planned improvements:

- **Option A**: Transfer Guardian role to the Main DAO Treasury (`projects[1].projectTreasury`) for full decentralization
- **Option B**: Create a Security Council Multisig — appointed and revocable by the Main DAO — for rapid emergency response
