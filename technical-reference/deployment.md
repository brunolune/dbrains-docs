# Deployment & Testing

## Network

- **Testnet**: Sepolia (Ethereum testnet)
- **Production target**: Layer 2 network (Base, Polygon, or similar)

## Smart Contract Deployment

### Deployment Script

Contracts are deployed using `DeployDBrains.s.sol` via the `redeploy.sh` helper:

```bash
./redeploy.sh
```

The script automates:
1. **Simulation** — Dry-run to estimate costs
2. **Cost estimate** — Display expected gas costs
3. **Broadcast** — Deploy to the network
4. **Address extraction** — Parse deployed addresses from logs
5. **contracts.ts update** — Automatically update the frontend address file

### What Gets Deployed

A full deployment creates ~30 contracts:

| Category | Count | Examples |
|----------|-------|---------|
| Implementation contracts | 11 | Governors, tokens, treasury, order book, task manager |
| Libraries | 1 | ProjectDeployer |
| Factory | 2 | ProjectFactory (impl + proxy) |
| Factory Governor | 2 | ProjectFactoryGovernor (impl + proxy) |
| Main DAO | 13 | 12 proxies + AccessManager |
| Mock tokens | 1 | Mock USDC (testnet only) |

### Gas Cost

Full redeployment costs approximately **0.3-0.5 ETH** on Sepolia. Allow ~10 minutes for all transactions to confirm.

### Address Management

All deployed addresses are stored in `web/src/lib/contracts.ts`. This file is the single source of truth for the frontend.

## Test USDC Faucet

Developers and users can obtain test USDC for the Sepolia testnet:

### Setup

1. Configure `.env` with your `PRIVATE_KEY`
2. Run:

```bash
./mint.sh <recipient_address>
```

This executes the `MintUSDC.s.sol` Foundry script, minting test USDC to the specified address.

## PocketBase Deployment

### Production (Railway)

- Dockerized PocketBase v0.22 running on Railway
- Persistent volume for SQLite database
- Domain: `api.dbrains.xyz`
- Auto-creates admin account from `PB_ADMIN_EMAIL` / `PB_ADMIN_PASSWORD` env vars via `entrypoint.sh`
- Migrations in `pb/pb_migrations/` auto-run on startup with `--automigrate`

### Local Development

```bash
cd pb
pocketbase serve
```

Available at `http://localhost:8090`. No separate database server required.

### Docker Build

```dockerfile
# pb/Dockerfile
FROM alpine:3.19
# PocketBase v0.22.9
# Copies hooks and migrations
# Runs via entrypoint.sh
```

## Frontend Development

```bash
cd web
npm install
npm run dev
```

The frontend connects to:
- PocketBase at `http://localhost:8090` (local) or `api.dbrains.xyz` (production)
- Sepolia RPC for on-chain reads
- RainbowKit for wallet connection
