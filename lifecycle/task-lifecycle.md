# Task Lifecycle

Tasks are the fundamental units of work in DBrains. Every task flows through governance — from proposal to verification to reward.

## The Cycle

### 1. Task Proposal

A project member proposes a new task (or set of tasks) through governance:

- **Structure**: Includes feasibility analysis, schedule (start/end dates), and specific sub-tasks with individual NTT rewards
- **Assignee & reward**: Each task specifies who will do the work and the NTT reward upon completion
- **Refinement**: Backlog proposals can link to a previous proposal as their parent, forming a version history (see [Refining a Backlog Item](#refining-a-backlog-item) below)

### 2. Vote

Project members vote on the task proposal:

- Task governance has the **shortest voting period**, typically one to two days, suited to task cycles that span a few days to a week
- Early execution threshold applies — overwhelming consensus can fast-track approval

### 3. Execution (Active Cycle)

If the vote passes:

- The proposal executes **directly** — no queueing or delay
- Tasks become active on-chain
- Assignees begin work off-chain (details tracked in the database)

### 4. During Active Work

Tasks appear on a **Kanban board** in the project dashboard, sorted into five columns based on their on-chain state and the current time:

| Column | Meaning |
|--------|---------|
| **Planned** | Scheduled but not yet started |
| **Active** | In progress |
| **Awaiting Verification** | Either the assignee signaled completion, or the deadline has passed |
| **Rejected** | The verification vote did not pass; awaiting reschedule or cancellation |
| **Verified** | Work accepted by the DAO; rewards minted |

While tasks are in progress, governance can:

| Action | When |
|--------|------|
| Reschedule a task | If delays occur, or after a rejected verification |
| Cancel a task | If the task is no longer needed |

Both require a governance proposal and vote.

### 5. Flagging & Verification

An assignee can **flag a task as done** directly from their card — no proposal needed — which moves the card to "Awaiting Verification" for early review. Alternatively, when the task's deadline passes, the card moves to "Awaiting Verification" automatically.

From there, any DAO member can open a **verification vote** on the card. Verification is a **single vote with two on-chain outcomes** — no second proposal needed to record a rejection:

- **If the vote passes** → the task moves to **Verified** and NTT rewards are automatically minted to the assignee.
- **If the vote fails** → the task moves to **Rejected**. **No NTT is minted.**

Once voting ends, anyone can settle the outcome from the proposal page with a single action — labelled **Finalize: Verify Task** (green) on a passing vote or **Finalize: Reject Task** (red) on a failing one.

### 6. After a Rejection

A rejected task is not terminal — the DAO can act on it from the **Rejected** column with two buttons:

- **Reschedule** — Drafts a proposal with new dates. If approved, the task returns to **Active** with a fresh window so the assignee can take another pass.
- **Cancel** — Drafts a proposal to permanently close the task. If approved, the task is terminated.

The same Reschedule action is also available on Planned and Active cards, so an assignee who anticipates a slip can self-signal it before the deadline rather than waiting for a rejection.

### 7. Reward

If the verification vote passes:

- The task is marked as verified
- NTT rewards are **automatically minted** to the assignee
- The minted NTTs immediately grant the assignee additional voting power and profit share

### 8. Archival

Verified tasks move to an **Archived** view seven days after verification. Once all tasks tied to a backlog proposal are verified or cancelled, the parent proposal is considered archived off-chain.

## Task States

```
Proposed → Active → Verified
                  ↘ Cancelled
                  ↘ Rejected → Active (rescheduled) → ...
                             ↘ Cancelled
                  ↘ Rescheduled → Active → ...
```

## Refining a Backlog Item

Plans change. A backlog proposal that's still in flight can be **refined** by another proposal that supersedes it — useful when the scope shifts, an estimate was off, or the team learns something mid-stream.

### When Refinement Is Allowed

A proposal is refinable as long as it still has work in flight:

- It hasn't been executed yet (still up for vote, queued, or pending), **or**
- It has been executed and at least one of its tasks is still active

Once every spawned task is verified or cancelled, the parent is considered archived and can no longer be refined. Proposals that were defeated, cancelled, expired, or rejected are never refinable — there's no live work to revise.

### How a Refinement Replaces the Original

A refinement is itself a backlog proposal, with one twist: it carries an explicit link to its parent. When members open the **Refine this proposal** action from a parent's detail panel, the new proposal modal pre-fills every field — title, description, feasibility, the full task list — so the team starts from the existing plan and edits from there.

When the refinement is voted in and executes, two things happen atomically in the same transaction:

1. **Any still-active tasks spawned by the parent are cancelled** — the refinement carries those cancellation calls in its own payload, captured at proposal time
2. **The refinement's new tasks are created** — replacing the old work on the Kanban board

If the parent hasn't been executed yet (no tasks to cancel), only the new tasks are created.

### Supersedence

The moment a refinement executes, the parent is **marked superseded** on-chain. From that point:

- The parent can no longer be voted on or executed, even by direct contract calls — the lock is enforced by the governor itself, not just the UI
- Already-terminal parents (executed, defeated, cancelled, expired) keep their status as-is — their in-flight task cleanup was handled by the refinement's cancellations

This makes the refinement the new source of truth, and prevents stale parents from accidentally being acted on.

### Revision Naming

Refinement titles are auto-composed by extending the parent's name with a `-rev.<n>` suffix:

```
foo → foo-rev.1 → foo-rev.1.1 → foo-rev.1.1.1
```

Sibling refinements increment the trailing segment (`foo-rev.1`, `foo-rev.2`, …). The composed title is locked in at creation time so it matches what voters signed.

### Refinement Tree in the Dashboard

In the proposal list, refinements are rendered as a tree under their parent — indented, with guide lines connecting parent to child, and tagged as **Refinement**. This makes the version history visible at a glance: you can see how a backlog item evolved through successive iterations without leaving the list view.

### Other Proposals That Can Be Refined

The same refinement mechanism also works for [roadmap proposals](roadmap.md) and [idea-reward proposals](idea-rewards.md). Since these don't spawn tasks, they can only be refined while they are **still up for vote** — once executed, a change is simply a new proposal.

### Rewarding the Idea

Every refinement, and the discussion around it, is part of an idea's history. When a backlog proposal is finally validated, the people who shaped it along the way — including through refinements that were voted down — can share an [Idea Reward](idea-rewards.md).

## Key Points

- **Fast governance** — Short voting periods keep the development pace high
- **On-chain accountability** — Task creation, verification, and rewards are all recorded on-chain
- **Automatic rewards** — No manual token distribution; NTTs mint on verification
- **Flexible** — Tasks can be rescheduled or canceled through governance if circumstances change
- **Assignee self-signal** — Assignees can flag work as done without waiting for the deadline, allowing early verification
