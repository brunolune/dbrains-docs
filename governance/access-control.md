# Access Control & Roles

Each project uses a role-based access control system to manage permissions. Roles are set up automatically during project deployment and control which parts of the system can perform which actions.

## Roles

| Role | Holder | What it can do |
|------|--------|----------------|
| **Admin** | TreasuryGovernor | Full control over the access control system |
| **Minter** | Task & Order Book systems | Mint NTTs (as task rewards or trade settlements) |
| **Order Creator** | Order Book Governor | Open, close, and cancel orders on the Private Order Book |
| **Pauser** | Guardian | Emergency pause/unpause of the Private Order Book |
| **Task Admin** | Task & Backlog Governors | Create, verify, reject, reschedule, and cancel tasks |
| **Treasury Admin** | TreasuryGovernor | Transfer ETH and tokens from the project treasury |
| **Burner** | Order Book system | Burn NTTs during trade settlements |
| **SBT Minter** | Freelancer & Investor Governors | Mint and revoke project membership SBTs |
| **Investor POB** | Investor Governor | Place buy orders on behalf of approved investors |
| **Allowance Admin** | Treasury & Freelancer Governors | Set or revoke spending allowances on the treasury (used for AI agents) |
| **Order Book Payer** | Order Book system | Settle payouts from the treasury when the project's own buy orders fill |
| **NTT Settings** | Setting Governor | Adjust the voting power curve (α) on the NTT token |
| **Creator Config** | Setting Governor | Set the project's creator-reward configuration |
| **Idea Config** | Setting Governor | Set the default idea-reward pools |
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
- The **FreelancerGovernor** can mint/revoke SBTs and adjust treasury allowances, but cannot move treasury funds directly — this lets onboarding and revocation proposals bundle SBT changes with allowance changes in a single vote (essential for safely adding and removing AI agents)
- Only the **TreasuryGovernor** can actually move funds out of the treasury. A payment attached to any other kind of proposal would pass its vote but could never be carried out — which is why sending gas to a new AI agent is a separate Treasury Transfer proposal rather than part of the onboarding vote

### SBT as Access Control

Beyond the role system, project membership SBTs serve as a broader access control layer:

- **Proposing**: Only SBT holders can create governance proposals
- **Voting**: Only SBT holders can vote
- **Trading**: Only SBT holders can place orders on the Private Order Book
- **Decryption**: Only current SBT holders can decrypt private proposals and chat. Encryption is **self-controlled** — each member derives an encryption key from their wallet and publishes a matching public key on-chain, so content is locked to the live membership with no dependency on any outside service. When a member is revoked, the project's key is rotated so they can no longer read new content (past content they already had access to stays readable).
  - The wallet signature used to derive your key is shown by your wallet as a clear, structured request from DBrains rather than an unreadable message, so you can see what you are signing.
  - When a new project turns on encryption for the first time, a single member — the largest NTT holder, normally the project's creator — sets up the shared project key. Other members wait for that step instead of each creating their own, which guarantees that everyone ends up reading and writing with the same key.

## Guardian Decentralization (Future)

The current Guardian assignment to the deployer wallet is a temporary bootstrapping measure. The goal is to transfer this role to a decentralized entity — either the Main DAO itself or a dedicated Security Council Multisig appointed and revocable by the Main DAO.
