# Decentralized Backend

DBrains keeps its off-chain data — proposals, chat, tasks, profiles, applications — on a **decentralized, peer-to-peer database** rather than a single company server. This is a deliberate, values-driven choice: a platform built for self-organizing communities shouldn't have one operator who could be pressured to censor it or take it down.

## Why It Matters

Most apps store their data on one server run by one company. That's a single point of control — and a single point of failure. If that server is shut down, seized, or compelled to remove content, the platform goes with it.

DBrains removes that chokepoint. Its data lives in **shared, append-only logs that many peers replicate**, with no central server that any one party controls. The goal is simple: **censorship-resistance and availability that don't depend on trusting a single operator.**

## How It Works (In Plain Terms)

- **No central server** — Data is replicated across a peer-to-peer network. Every participant keeps a copy and syncs changes with the others.
- **Always-on anchor nodes** — A small set of independent "relay" nodes stay online to pass updates between members and hold a full copy of the data. Several run in parallel and back each other up, so any one can go offline without interrupting the platform. They can run on ordinary, low-cost hardware (even a Raspberry Pi) — entirely off big-cloud infrastructure.
- **Wallet-signed writes** — Instead of a username-and-password login on a central server, every change is **signed by your wallet**. This proves who made each edit and prevents forgery, with no login server to trust or take down.
- **Privacy carries over** — The [self-controlled, membership-gated encryption](../governance/access-control.md#sbt-as-access-control) works exactly the same here. Private proposals and chat are readable only by current project members; the network stores nothing but encrypted, unreadable data.

## Status

The decentralized backend is the **main database running in production** at dbrains.xyz, replicated across a redundant set of independent nodes. It's an ongoing, values-first direction — the aim is a platform that stays open and available even when no single party is willing or able to keep it running.
