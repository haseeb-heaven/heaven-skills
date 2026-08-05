---
name: telegram-two-way
description: >-
  Two-way Telegram communication: a bot that receives and replies to user messages.
  Covers getUpdates polling, webhooks, reply flows, keyboard buttons, and conversation
  state. Use when you need an interactive Telegram bot that listens for user input
  and responds — commands, buttons, or back-and-forth conversations.
version: 1
---

# Telegram Two-Way Communication

Build an interactive Telegram bot that both **receives** messages from users and **replies** to them — commands, buttons, and full conversations.

## When to Use

- Interactive bots (commands, inline keyboards, menus)
- Agent-to-user chat: the user asks, the bot answers
- Multi-step flows (wizard-style conversations with state)
- Trigger actions from Telegram (run a script when a user sends a command)

## When NOT to Use

- One-way notifications only → use the [send-message skill](../telegram-send-message/SKILL.md)
- High-frequency real-time chat → polling has a delay; consider webhooks or a long-polling library

## Two Ways to Receive Messages

### Option A: Long Polling (`getUpdates`) — simplest for scripts

```bash
# Poll for new messages (offset = last processed update ID + 1)
curl -s "https://api.telegram.org/bot$BOT_TOKEN/getUpdates?offset=$OFFSET&timeout=30"
```

Loop pattern:

```bash
#!/bin/bash
BOT_TOKEN="123456:ABC-DEF..."
LAST_UPDATE=0

while true; do
  # Get updates since the last one
  RESP=$(curl -s "https://api.telegram.org/bot$BOT_TOKEN/getUpdates?offset=$((LAST_UPDATE + 1))&timeout=30")

  # Parse each message and reply
  echo "$RESP" | jq -c '.result[]' | while read -r update; do
    UPDATE_ID=$(echo "$update" | jq -r '.update_id')
    CHAT_ID=$(echo "$update" | jq -r '.message.chat.id')
    TEXT=$(echo "$update" | jq -r '.message.text // empty')

    [ -z "$TEXT" ] && continue
    echo "Received: $TEXT from chat $CHAT_ID"

    curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/sendMessage" \
      -d chat_id="$CHAT_ID" \
      -d text="You said: $TEXT"

    LAST_UPDATE=$UPDATE_ID
  done

  sleep 1
done
```

### Option B: Webhook — for always-on servers

```bash
# Set the webhook (server must have HTTPS + public URL)
curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/setWebhook" \
  -d url="https://your-server.com/webhook"

# Verify
curl -s "https://api.telegram.org/bot$BOT_TOKEN/getWebhookInfo"

# Remove (back to polling)
curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/deleteWebhook"
```

Telegram POSTs a JSON update to your webhook URL on every message. Your server parses it and replies with `sendMessage`.

## Interactive Elements

### Reply to the message (quote it)

```bash
curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/sendMessage" \
  -d chat_id="$CHAT_ID" \
  -d text="I got it!" \
  -d reply_to_message_id="$MESSAGE_ID"
```

### Inline keyboard buttons

```bash
curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/sendMessage" \
  -d chat_id="$CHAT_ID" \
  -d text="Choose an option:" \
  -d reply_markup='{"inline_keyboard":[[{"text":"Start","callback_data":"start"},{"text":"Stop","callback_data":"stop"}]]}'
```

Buttons come back as `callback_query` updates — reply with `answerCallbackQuery`:

```bash
curl -s -X POST "https://api.telegram.org/bot$BOT_TOKEN/answerCallbackQuery" \
  -d callback_query_id="$CALLBACK_ID" \
  -d text="You pressed Start!"
```

### Multi-step conversation (state)

Track state per `CHAT_ID` in a map/file/DB:

```
state[chat_id] = "awaiting_email"
→ next message from that chat is treated as the email address
```

## Common Commands Pattern

| Command | Update shape | Reply |
|---------|-------------|-------|
| `/start` | `message.text == "/start"` | Welcome + menu |
| `/help` | `message.text == "/help"` | Instructions |
| Button press | `callback_query.data` | `answerCallbackQuery` |
| Plain text | `message.text` | Freeform reply |

## Troubleshooting

| Issue | Cause → Fix |
|-------|------------|
| No updates received | `deleteWebhook` (webhook and polling can't both be active); check `getUpdates` isn't stuck on an old `offset` |
| `409 Conflict: terminated by other getUpdates request` | Two pollers running. Only one `getUpdates` at a time per bot |
| Duplicate replies | Processing the same `update_id` twice. Always advance `offset` past processed IDs |
| `Bad Request: chat not found` | Bot hasn't been started by the user in that chat yet — ask them to press `/start` |
| Webhook silently failing | Telegram requires HTTPS + valid cert; check `getWebhookInfo` for `last_error_message` |

## Best Practices

1. **Always ack with `offset`** — after processing update N, request from `N+1` so you never reprocess
2. **Handle `callback_query` and `message` separately** — they're different update shapes
3. **Idempotent replies** — if you crash mid-reply, you may send twice; that's fine for Telegram, just don't spam
4. **Keep state keyed by `chat_id`** — conversations are per-chat, not per-user across chats
5. **Set a generous `timeout=30` on long polling** — it holds the connection open so you react quickly without hammering the API

## Output Format

When using this skill, report the interaction:

```markdown
## Telegram Two-Way Session
- Mode: polling / webhook
- Bot: @[bot_username]
- Commands handled: [list]
- Last exchange: user: "[msg]" → bot: "[reply]"
- State tracked: [any conversation state per chat_id]
```
