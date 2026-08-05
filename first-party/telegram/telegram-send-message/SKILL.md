---
name: telegram-send-message
description: >-
  Send Telegram messages from a bot via the Bot API using curl. Covers getting
  the bot token (API key) from BotFather, constructing the sendMessage request,
  chat IDs, Markdown/HTML formatting, and pushing updates to a channel or user.
  Use when you need to send notifications or message updates from scripts,
  cron jobs, CI pipelines, or agent workflows to Telegram.
version: 1
---

# Telegram Send Message (One-Way)

Send messages from a Telegram bot to a user, group, or channel using the Bot API over curl. This is one-way communication — the bot sends, you don't receive replies.

## When to Use

- Notifications from cron jobs, builds, or deployments
- Alerts from monitoring scripts or agent workflows
- Sending updates (CI status, task done, error reports) to your phone
- One-way push updates to a channel

## When NOT to Use

- Two-way conversations (user replies handled) → use the [two-way skill](../telegram-two-way/SKILL.md)
- Sending media/files → use `sendPhoto`/`sendDocument` endpoints
- High-volume marketing → Telegram isn't built for spam

## Prerequisites

1. **Create a bot** with [@BotFather](https://t.me/BotFather) → `/newbot` → you get a **token** like `123456:ABC-DEF...`
2. **Get your chat/user ID** — see the [get chat id skill](../telegram-get-chat-id/SKILL.md)
3. Optionally add the bot to a group/channel and get that chat ID

## The Core curl Command

```bash
curl -s -X POST "https://api.telegram.org/bot<BOT_TOKEN>/sendMessage" \
  -d chat_id=<CHAT_ID> \
  -d text="Hello from my bot!"
```

**Success response:**
```json
{
  "ok": true,
  "result": {
    "message_id": 123,
    "chat": { "id": 123456789, "type": "private" },
    "text": "Hello from my bot!"
  }
}
```

If `"ok": false` is returned, read `description` for the error (e.g. `chat not found`, `bot was blocked by the user`).

## Common Patterns

### Send a message to a channel

Replace `<CHAT_ID>` with the channel's `@username` or numeric ID (prefixed with `-100` for supergroups):

```bash
curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/sendMessage" \
  -d chat_id=@my_channel \
  -d text="New update: $(date)"
```

### Format with Markdown

```bash
curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/sendMessage" \
  -d chat_id=$CHAT_ID \
  -d text="*Build passed* ✅" \
  -d parse_mode=Markdown
```

HTML mode is also available (`parse_mode=HTML`) — supports `<b>`, `<i>`, `<a href="...">`.

### Send from a script with variables

```bash
#!/bin/bash
BOT_TOKEN="123456:ABC-DEF..."
CHAT_ID="123456789"

send_tg() {
  curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/sendMessage" \
    -d chat_id="$CHAT_ID" \
    -d text="$1" \
    -d parse_mode=Markdown
}

send_tg "Deploy to production completed in $(git rev-parse --short HEAD)"
```

## Troubleshooting

| Error / Symptom | Cause → Fix |
|-----------------|------------|
| `401 Unauthorized` | Wrong bot token. Check with `getMe`: `curl -s https://api.telegram.org/bot<TOKEN>/getMe` |
| `chat not found` | Wrong chat ID, or bot never talked to that chat. Send the bot a message first, then re-check the ID |
| `bot was blocked by the user` | User pressed Stop/Block. No fix from bot side — ask user to `/start` again |
| `Bad Request: message text is empty` | `-d text=` got nothing; ensure the variable is set |
| `429 Too Many Requests` | Rate limit (≈30 msg/sec per chat). Add a small sleep between sends |

## Best Practices

1. **Keep the token secret** — never commit it. Use env vars or a secrets manager
2. **Rate-limit your sends** — add `sleep 1` in loops; Telegram allows ~30 messages/second per chat, but bursty scripts still get throttled
3. **Set `disable_notification=true`** for non-urgent updates so you don't get pinged off-hours
4. **Use `parse_mode` carefully** — invalid Markdown causes the whole message to fail
5. **Check `"ok": false` responses** — log them; silent failures are how notifications rot

## Output Format

When using this skill, report the outcome:

```markdown
## Telegram Message Sent
- Bot: @[bot_username]
- Chat: [chat_id or @username]
- Message: "[first 80 chars…]"
- Response: ok=true / ok=false ([error description])
```
