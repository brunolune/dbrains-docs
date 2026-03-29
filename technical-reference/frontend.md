# Frontend

The DBrains frontend is a Next.js application with a cyberpunk aesthetic, deep Web3 integration, and real-time governance interfaces.

## Tech Stack

| Technology | Purpose |
|------------|---------|
| Next.js (Latest) | React framework |
| TailwindCSS | Styling |
| Aceternity UI + Magic UI | Cyberpunk-themed components |
| RainbowKit | Wallet connection modal |
| wagmi | React hooks for contract interactions |
| viem | Low-level EVM utilities and address normalization |

## Key Pages

### Project List (`/projects`)

- **Public view**: Shows only deployed (active) projects
- **Admin view**: Additionally shows pending applications with validation actions
- Admin detection via wallet address check

### Project Dashboard (`/projects/[id]`)

The dashboard is composed of several widgets:

- **Treasury Widget** — Real-time USD balance + Private Order Book status (Open / Scheduled / Closed)
- **Active Tasks** — Ongoing work, assignees, NTT costs, verification buttons
- **Voting Widget** — Visual progress bars for active governance proposals
- **Team Widget** — Member leaderboard by NTT balance (ownership %)
- **Project Chat** — Live chat panel via `useChat("project", projectId)`

### Onboarding Hub (`/projects/[id]/onboarding`)

Dedicated sub-page for reviewing candidate applications:
- Freelancer and investor applications from PocketBase
- Candidate details (GitHub, LinkedIn, email, requested NTTs/price)
- One-click button to draft an onboarding proposal

### Proposals Page (`/projects/[id]/proposals`)

- **Sidebar navigation** — Filter by category (backlog, task-manager, freelancer-onboarding, investor-onboarding, pob-config, project-creation)
- **Dynamic creation** — "Create Proposal" button adapts its form based on the selected category
- **Deep linking** — URL parameters for pre-filled proposal creation (e.g., from the Onboarding Hub)
- **List view** — Filtered by status (Proposed, Approved, Voting, Executed, Rejected)
- **Detail view** — Full metadata, voting visualization, discussion chat

### Voting UI

Each proposal shows dual vote bars:
- **% of Votes Cast** — For vs Against relative to total votes
- **% of Total NTT Supply** — For vs Against relative to total supply, with a 60% early execution threshold marker

## Web3 Integration

### Contract Interactions

- `useWriteContract` — Submit transactions
- `useWaitForTransactionReceipt` — Track confirmations
- `useReadContract` — Read on-chain state
- Multicall batching for efficient RPC usage

### Address Handling

All addresses must be normalized with `viem`'s `getAddress()` before contract calls. Display-formatted (truncated) addresses must never be stored in data models.

### BigInt Serialization

A global `BigInt.prototype.toJSON` polyfill (in `src/lib/utils.ts`) prevents React DevTools from crashing during state serialization of deeply nested `BigInt` arrays from contract reads.

## Navigation

Global navbar with:
- Persistent wallet connection
- Home, Projects, Dashboard, Governance links
- **My Projects** dropdown — Filters projects by membership, separating Active / Pending / Validated states
- Dashboard shows a "Not Yet Deployed" guard for projects lacking on-chain contracts
