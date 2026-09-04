---
name: share-prs-on-slack
description: Draft and, after explicit approval, publish pull-request links in Slack using computer use. Use when the user asks to share, send, or post one or more PRs to Slack.
---

# Share PRs on Slack

Use computer use for every Slack inspection and publication. Do not use a
Slack connector, API, CLI, or webhook for this workflow.

1. Gather the PR links, titles, purpose, and dependency order from the user's
   request or the current repository. Ask only for details that cannot be
   determined safely.
2. Ask the user which Slack workspace and channel to use every time. Do not
   infer either from the repository, the active Slack view, prior sends, or
   this skill's examples.
3. Open Slack with computer use and verify that the visible workspace and
   channel exactly match the user's answer. If either does not match or cannot
   be verified, stop and ask the user to clarify.
4. Draft the exact top-level channel message. Match this concise, informal
   style:

   - One PR: `PR with the <purpose>: <PR_URL>`, optionally followed by one
     sentence of context or a review request.
   - Several PRs: a short lead-in ending in a colon, then one PR per bullet as
     `PR #<number> — <short scope>`, optionally followed by a one-sentence
     impact and the PR URL.
   - Dependent PRs: call them `stacked PRs`, use an ordered list, and append
     dependencies such as `→ main` or `→ PR #<number>`.

   Greetings are optional. Mention a person only when their approval or
   decision is specifically needed. Do not use `@here` unless the user asks.
5. Show the destination and complete draft, then ask for explicit approval to
   send it. Draft-only requests stop here. Approval applies only to this
   message or explicitly described batch.
6. After approval, use computer use to publish the message in the verified
   channel. Do not react, edit, delete, or send anything else.
7. Verify in the Slack UI that the message appeared in the intended workspace
   and channel, then report the result.

For reference, the observed Meridian convention uses workspace `Meridian` and
channel `#bekk-internal`. This is a style example, never a default destination.
