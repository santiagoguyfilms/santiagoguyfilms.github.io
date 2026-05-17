---
description: Check Gmail, prioritize what needs attention, and post a digest to Slack #emails
allowed-tools: mcp__Gmail__search_threads, mcp__Gmail__get_thread, mcp__Gmail__list_labels, mcp__Slack__slack_search_channels, mcp__Slack__slack_send_message
---

Produce a daily email digest and post it to Slack.

## Steps

1. **Gather email.** Use `mcp__Gmail__search_threads` to pull threads from the
   last 24 hours. Run these queries and merge the results (dedupe by thread):
   - `newer_than:1d in:inbox`
   - `is:unread in:inbox`
   For any thread that looks important but is unclear from the snippet, use
   `mcp__Gmail__get_thread` to read the full content before judging it.

2. **Triage each thread.** Classify into one of:
   - **Needs attention now** — a direct question awaiting your reply, a
     deadline, meeting request, payment/invoice, client or customer message,
     anything time-sensitive or money-related.
   - **Worth knowing** — informational, FYI, replies in threads you started,
     no action strictly required.
   - **Noise** — newsletters, promotions, automated notifications, receipts.
     Do not list these individually; just give a count.

3. **Prioritize.** Within "Needs attention now", order by urgency: hard
   deadlines and money first, then client/customer messages, then everything
   else. For each item give: sender, one-line summary, and the specific action
   you need to take.

4. **Post to Slack.** Find the `#emails` channel with
   `mcp__Slack__slack_search_channels`, then post with
   `mcp__Slack__slack_send_message`. Format:

   ```
   :email: Email digest — <today's date>
   <N> threads in the last 24h · <X> need attention · <Y> noise

   *Needs attention now*
   1. <Sender> — <summary> → _<action needed>_
   2. ...

   *Worth knowing*
   • <Sender> — <summary>
   • ...

   <Y> newsletters/notifications skipped.
   ```

   If nothing needs attention, say so plainly instead of padding the message.

## Notes
- Read-only on email — never archive, delete, or send replies.
- If a thread's importance is genuinely ambiguous, include it under "Needs
  attention now" and flag the uncertainty rather than risk burying it.
- Keep the Slack message scannable; link or quote sparingly.
