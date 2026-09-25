# Member Alerts

Many decisions on DBrains have a deadline: a vote that nobody notices can fail simply because members didn't know it existed. **Member Alerts** let members be notified on **Telegram** when something needs their attention — without opening the app.

Alerts are **opt-in**: nothing is sent unless a member links their account.

## What You Get Alerted About

| Category | Examples |
|---|---|
| **Proposals** | A new proposal, votes, a proposal executed or canceled |
| **Tasks** | A task assigned to you, your task verified or rejected, a teammate's task flagged as done and ready for verification |
| **Membership** | Someone applies to join, a member joins or is removed |
| **Chat** | New messages in project chat, sent as a short digest (one summary every 15 minutes), never one alert per message |

Task alerts are personal: "your task was verified" goes to the person who did it, while "a task was flagged as done" goes to the rest of the team, since they are the ones who can verify it. You are not alerted about your own actions.

Only **current members** receive alerts. Membership is checked on-chain every time, so a member who is removed stops receiving alerts immediately.

## Privacy: Pointers, Never Content

An alert only says *what kind* of thing happened, in which project, and gives a link to open it in the app. It **never contains project content** — not even a proposal title, since titles often describe exactly what the project's encryption is there to protect.

This means the alert system doesn't need to be a project member and holds no encryption keys. It couldn't read your private data even if it tried.

Linking your wallet to Telegram also stays private. The link is set up with a one-time code and a wallet signature; your Telegram chat ID is stored only on the alert server, encrypted, and never on the shared peer-to-peer database.

## Setting It Up

1. Go to **Settings → Notifications** and choose to link Telegram.
2. Sign a short message with your wallet — this proves the link is really yours, so nobody can redirect your alerts to their own account.
3. Press **Start** in the Telegram bot. You're linked.

## Controlling the Volume

You can fine-tune what you receive, either from **Settings → Notifications** or directly from the bot (`/mute`, `/unmute`, `/quiet`, `/status`, `/stop`):

- Turn each category (proposals, tasks, membership, chat) on or off
- Mute a single project, or everything
- Set **quiet hours** in your own time zone

Muting means "I don't want these" — alerts missed while muted or during quiet hours are skipped, not saved up and delivered later.

## Alerts and Unread Badges

The unread badges on the project dashboard are remembered **per device**: opening DBrains on a new computer starts fresh. Member Alerts are what follow you everywhere.

## A Note on Centralization

Telegram is a centralized service: it can see that an account receives DBrains alerts, and when. Project data, encryption, governance, and membership are not affected, and alerts are entirely optional — but the trade-off is real.

The alert system is therefore built so that Telegram can be swapped out. A self-hosted alternative (such as Matrix) could be added without rewriting the system, and a project that doesn't want to depend on the platform can run its own alert bot.
