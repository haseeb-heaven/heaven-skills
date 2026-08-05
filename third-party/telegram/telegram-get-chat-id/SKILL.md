---
name: telegram-get-chat-id
description: >-
  Get the Telegram bot API key (token) from BotFather and read the user's chat ID
  (and group/channel IDs) to use in Bot API calls. Covers /newbot, getUpdates-based
  chat ID discovery, the getMe endpoint, and where IDs appear in Bot API responses.
  Use when you need the bot token or chat ID to send or receive Telegram messages.
version: 1
---

# Telegram: Get Bot Token & Chat ID

Everything you need to obtain the two values every Telegram Bot API call requires: the **bot token** (API key) and the **chat ID** (user, group, or channel).

## When to Use

- First-time bot setup — you need the token
- Reading a user's chat ID to target them with `sendMessage`
- Finding a group/channel ID for sending updates to a channel
- Debugging why a chat ID doesn't work

## 1. Get the Bot API Key (Token)

The token is issued by **@BotFather** — only BotFather can create bots and issue tokens.

```text
1. Open Telegram → search @BotFather → press Start
2. Send /newbot
3. BotFather asks for a name → send it (e.g. "My Notifier")
4. BotFather asks for a username → must end in "bot" (e.g. "my_notifier_bot")
5. Done — BotFather replies with your token:
   Use this token to access the HTTP API:
   1234567890:AAHfQx_AbCdEfGhIjKlMnOpQrStUvWxYz
```

**Token format:** `\d{8,10}:[A-Za-z0-9_-]{35}` — e.g. `1234567890:AAHfQx_...`

### Verify the token works

```bash
curl -s "https://api.telegram.org/bot<TOKEN>/getMe"
```

**OK response** — token is valid:
```json
{
  "ok": true,
  "result": {
    "id": 123456789,
    "is_bot": true,
    "first_name": "My Notifier",
    "username": "my_notifier_bot"
  }
}
```

`401 Unauthorized` means the token is wrong. You can also use `@BotFather` → `/token` → select the bot to regenerate/rotate it.

> ⚠️ **The token is the password to your bot.** Anyone with it can send messages as the bot. Store it in an env var or secrets manager — never commit it to a repo.

## 2. Get a User's Chat ID

Telegram has no API to look up a chat ID by username. The reliable way: **have the user message your bot first, then read it from `getUpdates`.**

### Step-by-step

```bash
# 1. Tell the user to open your bot and press Start (or send any message):
#    t.me/<bot_username>

# 2. Poll updates (long polling, waits up to 30s for a new message)
curl -s "https://api.telegram.org/bot$BOT_TOKEN/getUpdates"
```

The response contains the chat ID:

```json
{
  "ok": true,
  "result": [
    {
      "update_id": 862093456,
      "message": {
        "message_id": 5,
        "from": { "id": 654321098, "is_bot": false, "first_name": "Alex", "username": "alex_dev" },
        "chat": {
          "id": 654321098,          ← THIS is the user's chat ID
          "first_name": "Alex",
          "type": "private"
        },
        "text": "/start"
      }
    }
  ]
}
```

**For a private chat, `chat.id` == `from.id`** — they're the same number.

### Extract just the chat ID

```bash
curl -s "https://api.telegram.org/bot$BOT_TOKEN/getUpdates" \
  | jq -r '.result[].message.chat.id' | sort -u
```

> If `getUpdates` returns `[]`, the user hasn't messaged the bot yet — ask them to press Start first. Then re-run.

## 3. Get a Group / Channel Chat ID

### Group chat

1. Add the bot to the group
2. Send any message in the group (or have someone else)
3. Poll `getUpdates` — the group chat appears with a **negative ID** like `-1001234567890` (supergroups) or `-123456789`

### Channel chat

1. Add the bot as an **admin** to the channel
2. Post a message in the channel
3. Poll `getUpdates` — the channel shows as `-100xxxxxxxxxx`

## Chat ID Reference

| Chat type | ID looks like | How to get it |
|-----------|--------------|---------------|
| Private (user) | `654321098` (positive, 8-10 digits) | User messages bot → `getUpdates` |
| Group | `-123456789` (negative) | Bot added to group, someone posts |
| Supergroup | `-1001234567890` (`-100` prefix) | Bot added, someone posts |
| Channel | `-1001234567890` | Bot is admin, posts a message |
| By username | `@channel_username` | Works in `chat_id` field directly for public channels |

## Troubleshooting

| Issue | Cause → Fix |
|-------|------------|
| `getUpdates` returns empty | User hasn't messaged the bot yet. Ask them to `/start` |
| `chat not found` when sending | Chat ID is wrong OR the bot was removed from that chat |
| Group ID looks wrong (positive) | You grabbed `from.id` (the sender) instead of `chat.id` |
| Token in commit history | **Revoke now**: BotFather → `/token` → revoke → use new token |
| Want the ID without code | Forward a bot message to [@userinfobot](https://t.me/userinfobot) — it replies with your user ID |

## Output Format

When using this skill, report:

```markdown
## Telegram Credentials
- Bot: @[bot_username]
- Bot token: [token, masked — stored in env var $BOT_TOKEN]
- User chat ID: [chat_id] (from: @[username])
- Group/channel IDs: [list if any]
- Verified with getMe: ok=true
```
