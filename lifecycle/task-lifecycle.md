# Task Lifecycle

Tasks are the fundamental units of work in DBrains. Every task flows through governance — from proposal to verification to reward.

## The Cycle

### 1. Task Proposal

A project member proposes a new task (or set of tasks) via the `TaskGovernor`:

- **Payload**: Calls `TaskManager.createTask(proposalId, description, assignee, reward, start, end)`
- **Structure**: Includes feasibility analysis, schedule (start/end dates), and specific sub-tasks with individual NTT rewards
- **Refinement**: Proposals can link to previous ones (`parentId`) to track version history — useful for iterating on backlog items

### 2. Vote

Project members vote on the task proposal:

- The `TaskGovernor` has the **shortest voting period** (5 minutes) for rapid iteration
- Early execution threshold applies — overwhelming consensus can fast-track approval

### 3. Execution (Active Cycle)

If the vote passes:

- The proposal executes **directly** — no queueing or delay
- Tasks are created on-chain in `Active` state
- Assignees begin work off-chain (details tracked in PocketBase)

### 4. During Active Work

While tasks are in progress, governance can:

| Action | When |
|--------|------|
| `rescheduleTask(taskId, newStart, newEnd)` | If delays occur |
| `cancelTask(taskId)` | If the task is no longer needed |

Both require a governance proposal and vote through the `TaskGovernor`.

### 5. Verification

When a task's end date has passed:

1. A **"Request Verification"** button appears on the task card in the Dashboard
2. Clicking it auto-creates a verification proposal with calldata `TaskManager.verifyTask(taskId)`
3. The proposal is tagged as type `task-verify`
4. DAO members review the deliverables and vote

### 6. Reward

If the verification vote passes:

- The task state becomes `Verified`
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

- **Fast governance** — 5-minute voting period keeps the development pace high
- **On-chain accountability** — Task creation, verification, and rewards are all recorded on-chain
- **Automatic rewards** — No manual token distribution; NTTs mint on verification
- **Flexible** — Tasks can be rescheduled or canceled through governance if circumstances change
