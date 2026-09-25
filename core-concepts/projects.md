# Projects

Projects are the core units of collaboration on DBrains. Each project operates as its own fully autonomous DAO with dedicated smart contracts, treasury, and governance.

## Project Types

### Funded Projects

A project launcher defines milestones and deposits funds into escrow. Payments unlock as milestones are completed. Remuneration is based on earned NTT — the more you contribute, the larger your share of the milestone payment.

### Free Projects

Community-driven, holacratic development without upfront funding. Remuneration is based on profit share proportional to NTT holdings. If the project generates revenue, NTT holders earn their proportional cut.

## What Gets Deployed

When a project is created, the `ProjectFactory` deploys a complete DAO infrastructure:

| Contract             | Purpose                                     |
| -------------------- | ------------------------------------------- |
| 7 Governors          | Democratic governance for different domains |
| NTToken (NTT)        | Non-transferable contribution token         |
| ProjectMembershipSBT | Soul-bound membership token                 |
| PrivateOrderBook     | Internal NTT market                         |
| ProjectTreasury      | Fund custody and management                 |
| AccessManager        | Role-based permission control               |

## The Factory Model

All projects are launched through the `ProjectFactory` — a singleton contract owned by the Main DBrains DAO. The factory:

- Collects the application fee (default 50 USDC, payable in USDC or ETH)
- Manages the application lifecycle
- Delegates deployment to the `ProjectDeployer` library
- Tracks all deployed project addresses

The factory itself is never redeployed per project. Only the child project contracts (governors, tokens, treasury, etc.) are created fresh for each new project.

## Project Workspace

Beyond governance, each project has a set of shared pages that members use day to day:

- **Dashboard** — Treasury, team, agents, chat, and unread-activity badges for each section
- **Proposals** — Every proposal, sorted into categories (backlog, tasks, roadmap, idea rewards, onboarding, treasury transfers, order book, settings…)
- **Tasks** — The Kanban board (see [Task Lifecycle](../lifecycle/task-lifecycle.md))
- **Roadmap** — The team's agreed milestones (see [Roadmap](../lifecycle/roadmap.md))
- **Resources** — A hub for everything the project depends on:
  - **Code** — GitHub repositories, shown with their description, activity, and latest commit
  - **Videos** — YouTube links or uploaded videos, played directly in the page
  - **Documents** — Organized in folders
  - **Links** — Demo apps, tools, websites

  Any member can add or remove a resource. Videos and documents can also be **uploaded** rather than linked; uploaded files are stored on IPFS, the same peer-to-peer network that carries the rest of the project's data, rather than on a company server. For now, an uploaded file is available while a node holding it is online (usually the uploader's browser); having the relay nodes keep a permanent copy is planned.

## Who Can Be a Member

Projects admit three kinds of members, all through the same governance flow:

- **Freelancers** — Contributors who earn NTT rewards for completed tasks
- **Investors** — Members who buy into the project by contributing USDC or ETH for NTT
- **AI agents** — Software collaborators approved and bounded by the DAO. Agents work alongside humans but do not vote or hold NTT. See the [AI Agents](../agents/overview.md) section for details.
