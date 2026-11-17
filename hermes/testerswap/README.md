# TesterSwap for Hermes Agent

Connect Hermes Agent to [TesterSwap](https://testerswap.com), the exchange where app developers test each other's live Google Play and App Store apps for credits. Your agent can check your credits, find apps to test, start tests, review the tests submitted for your apps, and plan Google Play closed testing. Real people install and test every app.

This folder is the Hermes package: `plugin.json`, `mcp.json` and one skill in [`skills/testerswap/`](skills/testerswap/SKILL.md). It ships no code of its own. The server is hosted by TesterSwap at `https://api.testerswap.com/mcp` and signs in with OAuth, so there are no API keys to copy. Full documentation: [testerswap.com/developers](https://testerswap.com/developers). The Cursor and Claude Code plugin is in [`plugins/testerswap`](../../plugins/testerswap).

## Install

You need Hermes Agent 0.21.6 or newer and Node.js 20.18.1 or newer with `npx` on your `PATH`.

From the Hermes plugin catalog:

```
hermes plugins install testerswap
hermes plugins enable testerswap
```

On first use a browser opens TesterSwap. Sign in with Google, Apple or an emailed link, check that the client is Hermes Agent and the permissions, and choose Allow. Revoke access any time in TesterSwap under Settings → Account.

## Before you install

- Every tool call goes to TesterSwap's hosted server at `api.testerswap.com` and acts on your own TesterSwap account. The tool list comes from that server at run time, not from this package.
- Sign-in runs the pinned `mcp-remote@0.1.49` through `npx`. It opens a browser and a local callback port on first use and stores OAuth tokens under `~/.mcp-auth`.
- `plugin.json` marks the server `untrusted`. Hermes asks before every tool the server does not mark read-only (adding or pausing apps, starting, cancelling, approving or sending back tests, marking notifications read) and refuses them in cron and other unattended runs.
- Approving a test transfers its held credits, and starting a test commits you to install and use the app yourself.

## Permissions

| Scope | Allows |
| --- | --- |
| `testerswap:read` | Read your credits, apps, tests and notifications |
| `testerswap:write` | Add or pause apps, start or cancel tests, approve tests and transfer credits, send back or decline tests, mark notifications read |
| `offline_access` | Stay connected until you revoke access |

## Tools

| Tool | Access | What it does |
| --- | --- | --- |
| `get_account` | Read | Your name, available credits, reliability and unread notification count |
| `list_my_apps` | Read | Your apps with visibility, credits availability and test counts |
| `get_app_tests` | Read | Tests and private feedback for one of your apps |
| `find_apps_to_test` | Read | Up to 20 apps you can test, with credits and minimum use time |
| `list_my_tests` | Read | Your tests, deadlines and next steps |
| `get_test` | Read | Your test and the in-app link for uploading your own screenshots |
| `list_notifications` | Read | Your recent notifications, optionally unread only |
| `play_closed_testing_guide` | Read | Plan a Google Play closed-testing window |
| `explain_play_console_error` | Read | Explain a supported Google Play Console error and how to resolve it |
| `list_app` | Write | Add your live Google Play or App Store app from its store URL |
| `set_app_visibility` | Write | Show your app to new testers or pause it |
| `start_test` | Write | Start testing an app; you install and use it yourself |
| `mark_notifications_read` | Write | Mark notifications as read |
| `release_test` | Sensitive write | Cancel your test before the install screenshot, returning held credits |
| `approve_test` | Sensitive write | Approve a submitted test of your app and transfer its held credits |
| `reject_test` | Sensitive write | Send back or decline a submitted test with a reason |

Sensitive writes move held credits or end a test and cannot be undone; the skill tells Hermes to confirm each one with you. Each connection allows 60 requests per minute.

## What the agent cannot do

Credits pay for testing, never for ratings or reviews. The agent cannot upload test proof, write or suggest store reviews, message other users, make purchases or delete your account. Installing, using the app and uploading screenshots stay with you. The Play Console tools give planning help only; TesterSwap's closed-testing exchange is not available through the agent.

## Example prompts

- How many tests can my credits cover, and which of my apps need attention?
- Find an Android app I can test and tell me exactly what to do next.
- Show the tests submitted for my app and summarize the feedback.
- Plan a 14-day Google Play closed test starting today with 12 testers.

## Support and policies

- Support: [support@testerswap.com](mailto:support@testerswap.com)
- [Privacy policy](https://testerswap.com/privacy/) · [Terms](https://testerswap.com/terms/) · [Security](https://testerswap.com/security/)

TesterSwap is a [SuperCollective](https://supercollective.studio) product. This package is MIT licensed; the TesterSwap service is governed by its terms.
