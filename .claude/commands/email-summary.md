---
description: Read recent email, prioritize what needs attention, and post a summary to Slack #emails
---

# Daily Email Summary → Slack #emails

You are doing a daily inbox triage. Work through these steps in order.

## 1. Pull recent email

Use the Gmail MCP tools. Search for threads received in the last day:

- Query: `newer_than:1d in:inbox`
- Also run: `is:unread newer_than:2d in:inbox` to catch anything still unread from the day before.

For each thread that looks substantive, use `get_thread` to read the actual
content. Skip obvious bulk/marketing/automated noise (newsletters, receipts,
notifications, calendar spam) unless it clearly needs action.

## 2. Understand and prioritize

For every meaningful email, determine:
- Who it's from and what they want.
- Whether it needs a reply, a decision, or an action — and by when.
- How urgent/important it is.

Sort everything into three buckets:
- **🔴 Needs attention today** — time-sensitive, awaiting your reply, money,
  clients, deadlines, anything that breaks if ignored.
- **🟡 Worth a look** — useful but not urgent; can wait a day or two.
- **⚪ FYI / low priority** — informational, no action needed.

## 3. Post the summary to Slack

Find the `#emails` channel (use `slack_search_channels` if you need its ID),
then post one message with `slack_send_message`.

Format the message like this:

```
*📬 Daily Email Summary — <today's date>*
<one-line overview: total new emails, how many need attention>

*🔴 Needs attention today*
• *<sender>* — <what they want / why it matters> _(<deadline if any>)_
• ...

*🟡 Worth a look*
• *<sender>* — <short note>
• ...

*⚪ FYI*
• <brief one-liners, grouped if many>
```

Rules for the Slack post:
- If a bucket is empty, write "None" under it — don't drop the heading.
- Keep each bullet to one line. Be specific (names, amounts, dates), not vague.
- Lead with the most urgent item in the 🔴 bucket.
- If there's truly nothing of note, still post a short "Quiet inbox today" message.

## 4. Wrap up

After posting, reply in chat with a one-line confirmation of what was posted
and the count per bucket. Do not modify, archive, or reply to any emails —
this is read-only triage.
