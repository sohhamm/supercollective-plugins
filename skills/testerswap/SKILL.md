---
name: testerswap
description: "Use the TesterSwap MCP tools to manage the user's own TesterSwap account: check credits and which apps need attention, find an app to test and start a test, review and approve or send back tests submitted for the user's apps, list or pause an app, read notifications, and plan Google Play closed testing. Use when the user mentions TesterSwap, app testers, testing credits, or Google Play closed testing with 12 testers for 14 days."
---

# TesterSwap

TesterSwap is an exchange where app developers test each other's live Google Play and App Store apps for credits. The `testerswap` MCP server acts only for the signed-in user.

## Real testing stays with the person

- Starting a test does not test the app. The person installs the app on their own device, uses it for at least the minimum time, and uploads install and finish screenshots in TesterSwap. Give them the store link, the minimum use time and the TesterSwap link from `start_test` or `get_test`, and never say the app was installed or tested.
- No tool uploads proof, writes or suggests a store review or rating, messages other users, makes purchases or deletes the account. Refuse those requests and say why: credits pay for testing, never for ratings or reviews.

## Confirm before sensitive writes

`approve_test`, `reject_test` and `release_test` move held credits or end a test and cannot be undone. Before calling one, show the test, the app and the credits involved and get the user's explicit yes. Read the submitted feedback with `get_app_tests` before recommending approval.

## Common tasks

| Task | Tools |
| --- | --- |
| How many tests can my credits cover, which apps need attention | `get_account`, `list_my_apps`, `get_app_tests` |
| Find an app to test and start | `find_apps_to_test`, `start_test`, `get_test` |
| Follow my own tests and deadlines | `list_my_tests`, `get_test` |
| Review tests of my app | `list_my_apps`, `get_app_tests`, then `approve_test` or `reject_test` after confirmation |
| Cancel a test before installing | `release_test` after confirmation |
| List a live store app, pause or show it | `list_app`, `set_app_visibility` |
| Notifications | `list_notifications`, `mark_notifications_read` |
| Plan a Google Play closed test, explain a Play Console error | `play_closed_testing_guide`, `explain_play_console_error` |

The Play Console tools give planning help only. TesterSwap's closed-testing exchange is not available through these tools; do not promise testers for a closed track.

## Errors

Tool errors come back as a result with a plain reason, such as a test that is not the user's or not in the right state. Report the reason; do not retry a write. Read-only connections (`testerswap:read`) refuse every write: tell the user to reconnect with write access if they want the change. Past 60 requests per minute the server answers 429 until the minute resets.
