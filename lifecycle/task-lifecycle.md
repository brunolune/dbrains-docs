# Task Lifecycle

Tasks are the fundamental units of work in DBrains. Every task flows through governance — from proposal to verification to reward.

## The Cycle

### 1. Task Proposal

A project member proposes a new task (or set of tasks) through governance:

- **Structure**: Includes feasibility analysis, schedule (start/end dates), and specific sub-tasks with individual NTT rewards
- **Assignee & reward**: Each task specifies who will do the work and the NTT reward upon completion
- **Refinement**: Proposals can link to previous ones to track version history — useful for iterating on backlog items

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

Tasks appear on a **Kanban board** in the project dashboard, sorted into four columns based on their on-chain state and the current time:

| Column | Meaning |
|--------|---------|
| **Planned** | Scheduled but not yet started |
| **Active** | In progress |
| **Awaiting Verification** | Either the assignee signaled completion, or the deadline has passed |
| **Verified** | Work accepted by the DAO; rewards minted |

While tasks are in progress, governance can:

| Action | When |
|--------|------|
| Reschedule a task | If delays occur |
| Cancel a task | If the task is no longer needed |

Both require a governance proposal and vote.

### 5. Flagging & Verification

An assignee can **flag a task as done** directly from their card — no proposal needed — which moves the card to "Awaiting Verification" for early review. Alternatively, when the task's deadline passes, the card moves to "Awaiting Verification" automatically.

From there, DAO members can open the verifier actions on the card:

- **Verify** — Drafts a verification proposal that, if passed, marks the task complete and mints NTT rewards
- **Reject** — Drafts a reschedule proposal with new dates, sending the task back to Planned/Active

### 6. Reward

If the verification vote passes:

- The task is marked as verified
- NTT rewards are **automatically minted** to the assignee
- The minted NTTs immediately grant the assignee additional voting power and profit share

### 7. Archival

Verified tasks move to an **Archived** view seven days after verification. Once all tasks tied to a backlog proposal are verified or cancelled, the parent proposal is considered archived off-chain.

## Task States

```
Proposed → Active → Verified
                  ↘ Cancelled
                  ↘ Rescheduled → Active → ...
```

## Key Points

- **Fast governance** — Short voting periods keep the development pace high
- **On-chain accountability** — Task creation, verification, and rewards are all recorded on-chain
- **Automatic rewards** — No manual token distribution; NTTs mint on verification
- **Flexible** — Tasks can be rescheduled or canceled through governance if circumstances change
- **Assignee self-signal** — Assignees can flag work as done without waiting for the deadline, allowing early verification
