# Project Creation

Launching a new project on DBrains is a democratic process that combines an application fee with community governance.

## The Process

### Step 1: Application

The project creator submits an application through the platform UI:

1. **Connect wallet** — A Web3 wallet is required
2. **Fill metadata** — Title, description, mission, tokenomics plan, tech stack, roadmap, etc.
3. **Pay the application fee** — Default 50 USDC, configurable by the Main DAO. The applicant can pay in either USDC or ETH; the USD amount stays constant either way, with the ETH equivalent computed live from a price oracle.
4. **Submit** — The application is stored in the database and recorded on-chain

### Step 2: Governance Vote

The application becomes visible in the Main DAO's proposals list:

* **Who can propose**: Because the applicant paid the USDC fee, they are immediately granted permission to propose project creation — bypassing the standard minimum token threshold (anti-spam via economic cost rather than token ownership)
* **Who can vote**: Only Main DBrains DAO members (Community SBT holders) can vote on new project approvals

### Step 3: Automated Deployment

If the proposal passes, execution triggers the automated deployment of the new project:

1. All the project's DAO contracts are deployed (governors, token, membership, order book, treasury, and access control)
2. The creator receives an SBT (project membership)
3. Optional: initial members and NTT allocations can be specified. These initial members become the project's **creators** (see [Creator Rewards](#creator-rewards) below)

### Output

A fully configured DAO with democratic governance, a treasury, an internal market, and role-based access control — all owned by the creator and members, with the Main DAO retaining a Guardian role.

## Cost

* **Application fee**: 50 USDC equivalent, payable in USDC or ETH (configurable by the Main DAO)
* **Gas**: Deployment costs are covered by the executor of the passed proposal

## Creator Rewards

Founders do a lot of foundational work before a project has any measured value — and at that point nobody knows what an NTT will eventually be worth, so a flat upfront grant is impossible to size fairly. **Creator Rewards** solve this by tying the founders' bonus to the *living* token economy: it's calculated from what members actually earn as the project runs, so it stays meaningful however the token's value evolves, and it streams over a set period of real activity rather than being paid all at once.

### Who Counts as a Creator

Every **initial member** specified at creation (along with their starting NTT allocations) is registered as a **creator** when the project deploys. This set is fixed from day one — it can't be changed afterwards, and it's the group entitled to the creator bonus.

### Choosing a Mode

At creation, the founder picks one of three reward modes:

| Mode | How the bonus works |
|------|---------------------|
| **None** | No extra reward. |
| **Mean-based** | Each creator earns a weekly bonus based on the *average* task earnings across members that week, scaled by a chosen coefficient, and split between creators by their initial allocation. |
| **Multiplier** | Each creator earns a bonus on top of their *own* verified task earnings — e.g. a 1.5× multiplier adds 50% to what they earn from tasks. |

### Duration & Taper

The bonus runs for a set number of weeks from activation. An optional **linear decay** can taper it down over that window — starting full and winding to zero — so the reward front-loads the early, riskiest phase of a project.

### Claiming

Rewards accumulate week by week and are **claimed on demand**: a creator claims their accrued bonus whenever they like, and the newly minted NTT lands in their wallet just like a task reward. The dashboard shows both what's claimable now and what's still accruing for the current week.

### Activation & Governance

Creator Rewards go through governance rather than being set unilaterally:

- The mode and its parameters are chosen at creation, but only take effect once a **governance proposal** locks them in.
- Only **creators** can propose a creator-reward configuration; everyone still votes on it.
- **Every project must set a config — even "None" — before any task can be created.** This is a deliberate gate so the reward terms are agreed up front; the dashboard surfaces a reminder until it's done.

Because creators are fixed at deployment, re-proposing a config can only adjust the reward terms — it can never change who the creators are.
