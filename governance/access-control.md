# Access Control & Roles

Each project uses a role-based access control system to manage permissions. Roles are set up automatically during project deployment and control which parts of the system can perform which actions.

## Roles

| Role | Holder | What it can do |
|------|--------|----------------|
| **Admin** | TreasuryGovernor | Full control over the access control system |
| **Minter** | Task & Order Book systems | Mint NTTs (as task rewards or trade settlements) |
| **Order Creator** | Order Book Governor | Open, close, and cancel orders on the Private Order Book |
| **Pauser** | Guardian | Emergency pause/unpause of the Private Order Book |
| **Task Admin** | Task Governor | Create, verify, reschedule, and cancel tasks |
| **Treasury Admin** | TreasuryGovernor | Transfer ETH and tokens from the project treasury |
| **Burner** | Order Book system | Burn NTTs during trade settlements |
| **Investor POB** | Investor Governor | Place buy orders on behalf of approved investors |
| **Guardian** | Deployer / Main DAO | Emergency safety role with limited scope |

## How It Works

### Automatic Setup

When a project is deployed:

1. The access control system is created and all roles are assigned to the appropriate governors and contracts
2. Permissions are locked down so each component can only perform actions within its domain
3. The **Admin role** is handed to the TreasuryGovernor (the most powerful governor)
4. The deployer renounces its temporary admin role — no single wallet retains control

### Role Separation

The role system ensures strict separation of concerns:

- The **task system** can mint NTT rewards but cannot spend treasury funds
- The **order book** can mint and burn NTTs for trades but cannot create tasks
- The **TreasuryGovernor** can spend funds and modify access control, but only through governance votes
- The **Guardian** can only pause/unpause the order book — a safety mechanism, not a governance override

### SBT as Access Control

Beyond the role system, project membership SBTs serve as a broader access control layer:

- **Proposing**: Only SBT holders can create governance proposals
- **Voting**: Only SBT holders can vote
- **Trading**: Only SBT holders can place orders on the Private Order Book
- **Decryption**: Only SBT holders can decrypt private proposal data (via Lit Protocol)

## Guardian Decentralization (Future)

The current Guardian assignment to the deployer wallet is a temporary bootstrapping measure. The goal is to transfer this role to a decentralized entity — either the Main DAO itself or a dedicated Security Council Multisig appointed and revocable by the Main DAO.
