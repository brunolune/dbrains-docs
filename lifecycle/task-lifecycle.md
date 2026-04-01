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

While tasks are in progress, governance can:

| Action | When |
|--------|------|
| Reschedule a task | If delays occur |
| Cancel a task | If the task is no longer needed |

Both require a governance proposal and vote.

### 5. Verification

When a task's end date has passed:

1. A **"Request Verification"** button appears on the task card in the Dashboard
2. Clicking it auto-creates a verification proposal
3. DAO members review the deliverables and vote

### 6. Reward

If the verification vote passes:

- The task is marked as verified
- NTT rewards are **automatically minted** to the assignee
- The minted NTTs immediately grant the assignee additional voting power and profit share

### 7. Archival

Once all tasks for a proposal are verified, the parent proposal is considered archived off-chain.

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
