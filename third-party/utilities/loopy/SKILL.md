---
name: loopy
description: >-
  Discover, find, compare, and use Loopy-related tools and workflows. Covers Loopy's
  API integrations, automation patterns, bot configurations, message templates, and
  scheduling. Use when building or managing Loopy-powered messaging automations.
version: 1
---

# Loopy

Discover, find, compare, and work with Loopy — a platform for building conversational bots and messaging automations.

## When NOT to Use

- Non-messaging automation — use general workflow automation tools instead
- Direct API integrations without chat interface — Loopy is conversation-focused
- Enterprise-grade compliance needs beyond Loopy's framework — evaluate custom solutions

## Core Concepts

| Concept | Description |
|---------|-------------|
| **Loops** | Conversation flows that users interact with over time |
| **Triggers** | Events that start a loop (webhook, schedule, user action) |
| **Blocks** | Individual steps in a conversation (text, image, form, logic) |
| **Variables** | State storage across conversation turns |
| **Integrations** | Connected services (CRM, database, calendar, etc.) |

## Common Workflows

### Creating a Loop
1. Define the trigger (what starts the conversation)
2. Design the flow blocks (message → action → response)
3. Add variables for state tracking
4. Configure integration endpoints
5. Test with simulation before going live

### Integration Patterns

| Integration Type | Use Case | Example |
|-----------------|----------|---------|
| Webhook | Real-time event handling | New signup notification |
| Schedule | Time-based messages | Daily digest, reminders |
| User Action | Interactive responses | Quiz, survey, support ticket |
| Data Lookup | Personalized content | Fetch user profile, order status |

## Best Practices

1. **Keep loops focused** — One objective per loop. If it has multiple goals, split into separate loops
2. **Handle errors gracefully** — Always have fallback paths for failed integrations
3. **Respect rate limits** — Queue outgoing messages if hitting provider thresholds
4. **Test with real data** — Simulation is good; actual user testing catches edge cases
5. **Version your loops** — Changes affect all active users; test in staging first

## References

- [API Documentation](https://docs.loopy.ai)
- [Integration Guides](https://docs.loopy.ai/integrations)
- [Block Reference](https://docs.loopy.ai/blocks)
- [Webhook Setup](https://docs.loopy.ai/webhooks)
