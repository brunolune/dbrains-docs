# Privacy & Encryption

DBrains uses **Lit Protocol** to encrypt sensitive proposal metadata so only project members (SBT holders) can decrypt and read internal DAO discussions.

## Overview

Lit Protocol is a decentralized key management network. It allows you to define **Access Control Conditions** — on-chain checks that determine who can decrypt data. DBrains uses this to gate proposal content behind SBT ownership.

## Network

- **Development**: `nagaDev` (free development devnet)
- **Production**: `nagaTest` or `naga` (paid, requires $LITKEY token balance or Capacity Credits)

## How Encryption Works

### Encrypting Proposal Data

When a member creates a proposal via the `BacklogGovernor`:

1. An **Access Control Condition (ACC)** is built:
   ```
   ERC721.balanceOf(userAddress) >= 1
   ```
   Checked against the project's `ProjectMembershipSBT` contract on Sepolia.

2. The proposal payload (description, feasibility, tasks, etc.) is encrypted:
   ```
   litClient.encrypt({ dataToEncrypt, accessControlConditions })
   ```

3. The encrypted output is stored alongside the on-chain proposal:
   - `_litCiphertext` — The encrypted data
   - `_litDataHash` — Hash for verification
   - `_litAcc` — The access control conditions

4. The on-chain description contains only the title + a placeholder message + the encrypted fields

### Decrypting Proposal Data

When a member wants to read the full proposal:

1. The UI shows a **"Decrypt Content"** button
2. On click, an auth context is obtained (wallet signature, SIWE-style)
3. Lit Protocol verifies the ACC on-chain: does this wallet hold the project's SBT?
4. If yes, decryption keys are released and the full payload is restored

## Session Caching

After the initial wallet signature, Lit generates a session keypair stored in the browser's `localStorage`:
- Valid for **24 hours**
- Subsequent decryptions reuse this session automatically
- No repeated signature prompts — seamless UX after first auth
- SBT ownership is still verified on each decryption (under the hood)

## Technical Details

### SDK

- `@lit-protocol/lit-client` v8
- `@lit-protocol/auth`
- `@lit-protocol/networks`

### Implementation

Located in `web/src/lib/lit.ts`:
- `createLitClient({ network: nagaDev })` — Singleton, lazily initialized, browser-only
- `createAuthManager` with `localStorage` storage plugin
- `encryptForProject(plaintext, sbtAddress)` — Encrypt data for a project's members
- `decryptForProject(ciphertext, hash, acc)` — Decrypt with wallet verification

### Buffer Polyfill

The browser `buffer` polyfill (v6) lacks BigInt methods that Lit SDK's crypto module needs. A runtime patch for `Buffer.prototype.writeBigUInt64BE` and `readBigUInt64BE` is applied at initialization.

## What Gets Encrypted

- Proposal descriptions and detailed metadata
- Feasibility analyses
- Task breakdowns and reward structures
- Any sensitive project-internal discussions

## What Remains Public

- Proposal titles
- Vote counts and outcomes
- Task states (Active/Verified/Cancelled)
- Treasury balances
- Membership (SBT ownership)
