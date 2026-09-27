# Bizopa CRM for Claude

Work your [Bizopa](https://bizopa.com) CRM by talking to Claude. The plugin connects Claude to
your workspace and teaches it two everyday jobs:

| Skill | Try saying |
|---|---|
| **Set up your workspace** — a few plain questions about your business, then a plan of tables, fields and stages to rename, add or switch off, built only after you agree. | "Set Bizopa up for my aircon servicing business." · "I also need to track vehicles." |
| **Log a conversation** — finds the right customer, records the call, meeting or visit the way your workspace tracks it, updates the deal where the conversation changed something, and offers a reminder for the next step. | "Log this call with Dr Tan: she wants the quote by Friday." · *paste your meeting notes* |

Everything else your role allows works too: search, reports, dashboards, "what needs my
attention today", adding and updating records.

## Connect

1. Install the plugin (or add the **Bizopa** connector) in Claude.
2. Sign in with your usual Bizopa account when Claude asks. If you belong to several
   workspaces, choose which ones Claude may use.
3. Ask away.

Claude acts as you: it sees and changes only what your role in the workspace allows. It asks
before anything that affects other people (deleting, unlinking, sending email). Deleted records
stay in "Recently deleted" for 30 days. You can see or disconnect Claude any time under
**Settings → AI assistants** in Bizopa.

## What's inside

- `.mcp.json` — the Bizopa connector, `https://bizopa.com/mcp` (sign-in through OAuth).
- `skills/set-up-workspace` and `skills/log-conversation` — the two jobs above.

## Help

Setup guide: [bizopa.com/claude](https://bizopa.com/claude) · [Privacy](https://bizopa.com/privacy) ·
[Terms](https://bizopa.com/terms) · hello@bizopa.com

## Licence

MIT — see [LICENSE](LICENSE).
