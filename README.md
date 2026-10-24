# Real Estate WhatsApp Lead Automation

An n8n workflow system that turns incoming WhatsApp messages from property leads into clean, validated database records, with an AI agent that handles the conversation.

**Demo (about 5 minutes):** https://youtu.be/A774L_G5KpU

## Stack

n8n, WhatsApp Business Cloud API, Supabase, PostgreSQL, OpenAI-based AI agent

## Design principle

The AI never touches core logic. Saving data, duplicate checks, conversation creation and timestamps run on fixed workflow rules. The AI only understands the message and writes the reply. This keeps behavior predictable when the model makes a mistake.

## How it works

1. **Inbound webhook.** Every WhatsApp message arrives through the WhatsApp Business Cloud API.
2. **Normalization.** The workflow converts each message into a fixed set of fields: phone, message ID, contact name, message type, text, time received.
3. **Validation.** Each message is validated before anything is saved.
4. **Data layer (Supabase / PostgreSQL).** Three entities: leads, conversations and messages. A lead is identified by phone number, and the same WhatsApp message ID is never stored twice.
5. **AI agent.** An agent with Supabase tools reads the conversation and replies to the lead.

## Reliability

- Fixed field schema and validation before any write
- Idempotent storage: duplicate message IDs are ignored
- Leads identified by phone number to avoid duplicate lead records
- Core operations (save, deduplicate, create conversation, timestamp) are rule-based, not AI-driven

## Status

The data layer and inbound workflow are built. The AI sales agent on top is in testing: natural conversation, edge cases, and answers the AI makes up.

## Author

Ziad Mohamed, AI Automation Engineer
[LinkedIn](https://linkedin.com/in/ziad-mohamed-832807340)
