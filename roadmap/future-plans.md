# Future Plans

## Guardian Decentralization

The current Guardian and Pauser roles are assigned to the deployer wallet — a temporary bootstrapping measure. Two paths are being considered:

### Option A: Total Decentralization

Transfer Guardian roles directly to the **Main DAO Treasury** (`projects[1].projectTreasury`). All emergency actions would require a governance vote.

- **Pro**: Maximum decentralization, no trusted individuals
- **Con**: Slower emergency response (requires governance vote)

### Option B: Security Council

Create a **Security Council Multisig** to hold Guardian roles:

- Appointed by the Main DAO through governance
- Revocable by the Main DAO at any time
- Enables rapid emergency response (multisig approval, not full DAO vote)
- **Pro**: Fast emergency response while remaining accountable to the DAO
- **Con**: Introduces a semi-trusted entity

## Production Hardening

### Governance Parameters

Development uses short voting periods (5-10 minutes) for rapid iteration. Production will use:
- Longer voting periods for critical decisions (treasury, settings)
- Higher quorum requirements
- Adjusted early execution thresholds

### Layer 2 Migration

The platform targets deployment on a Layer 2 network (Base, Polygon, or similar) for:
- Lower gas costs for the ~30 contract deployments
- Faster transaction confirmations
- Better UX for frequent governance interactions

### Lit Protocol Mainnet

Moving from `nagaDev` (free devnet) to `nagaTest` or `naga` (mainnet):
- Requires $LITKEY token balance or Capacity Credits
- More reliable decryption infrastructure
- Production-grade uptime guarantees

## Future Features

### AI Agents

Integration of AI agents for:
- Automated task suggestions based on project roadmap
- Code review assistance
- Proposal drafting and refinement

### Multi-Currency Support

The Private Order Book is designed for future multi-currency support beyond USDC.

### Enhanced Privacy

Expanding Lit Protocol encryption beyond proposals to:
- Task details and deliverables
- Member communications
- Financial discussions

### Cross-Project Collaboration

Mechanisms for projects to collaborate, share resources, and create inter-DAO proposals.
