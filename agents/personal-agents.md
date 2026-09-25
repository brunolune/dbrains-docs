# Personal Agents

A **personal agent** is your own AI assistant for writing proposals. It belongs to you, not to a project, and answers one question before you submit: *is this proposal clear enough for people to vote on?*

## What It Is (and Isn't)

A personal agent is simply a saved AI setup: a name, the AI model to use, your standing instructions, a spending ceiling per review, and your own **OpenRouter** API key (OpenRouter is a service that gives access to many AI models under a single account).

It is **not** a project member. It has no wallet, no membership SBT, no onboarding vote, no treasury budget, and it never reads project chat. It only runs when you ask it to, from the proposal form.

You create it once and it follows you into **every project** you belong to. Its cost is charged to your own OpenRouter account — never to a project treasury.

## Reviewing a Proposal

The proposal form has an **Agent review** button for every proposal type that contains written text (it isn't offered on forms that are just numbers and dates, such as order-book or governance settings).

1. Pick one of your agents and a token ceiling. You see the **maximum** the review can cost before you run it.
2. Run the review. The agent's improved version **replaces your draft directly** in the form.
3. Edit anything you disagree with and review again as many times as you like — each pass works on whatever the form currently contains.
4. **Undo review** brings back your own words at any time.

After each run you see what it actually cost (usually well below the maximum), plus a running total.

Writing a proposal entirely by hand, without ever touching an agent, remains a perfectly normal way to use DBrains.

### What Gets Reviewed

- The title, description, and feasibility
- Each task's description
- Each roadmap milestone's title and description

When refining an existing proposal, the agent is told so, and focuses on sharpening what changed rather than rewriting the original.

If your proposal has **no tasks yet** (or no milestones, for a roadmap), the agent can suggest them based on your description — following the structure you laid out. The form warns you when it is about to draft rather than rewrite, since drafting takes longer and needs a higher token ceiling.

### What Is Never Changed

Some fields are too important to leave to an AI. The agent can see them — it needs to, to judge whether the work is well-scoped — but it can **never change them**:

| Field | Why it is protected |
|---|---|
| Task assignee | A wallet address — one wrong character would send the reward to the wrong person |
| Task reward | It becomes a real NTT payment |
| Task dates | Your scheduling decision |
| Milestone target dates and status | Your planning decisions |

Instead, the agent leaves a **comment** beside each task or milestone, plus an overall commentary. These comments are for you only — they are never submitted with the proposal.

On rewards, the agent has no market-rate reference, so it doesn't claim what a task "should" cost. It only points out whether a reward looks out of proportion compared with the other tasks in the same proposal.

## Your API Key Stays Yours

DBrains' shared database is replicated to every participant, so your API key needs strong protection:

- It is **encrypted** before being stored, and is never stored or returned in readable form.
- It is **bound to your wallet**: it can only be used by someone signed in with your wallet. Copying someone else's encrypted key is useless — nobody can spend another member's credits.
- Only you can create, edit, or delete your personal agents.

## Related

- [AI Agents Overview](overview.md) — How personal agents differ from project agents
- [Task Lifecycle](../lifecycle/task-lifecycle.md) — Backlog proposals and refinements
- [Roadmap](../lifecycle/roadmap.md) — Roadmap proposals
