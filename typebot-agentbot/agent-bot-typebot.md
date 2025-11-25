# Typebot Agent Bot

This document describes how Mega integrates with Typebot when an inbox is connected to a **Typebot** agent bot.

## Overview

- Incoming public messages in a pending conversation are forwarded to Typebot. A Typebot session is started if none exists; otherwise the chat is continued using the stored session id.
- Responses from Typebot are enqueued as bot messages in the conversation. When the flow finishes, Mega hands the conversation back to the human queue.
- A subset of contact, conversation, and account details is sent as **prefilled variables** to Typebot on the first request.

## Configuration (Agent Bot → Typebot)

Set these fields on the agent bot:

- `api_url` (required): Base Typebot URL. Defaults to `https://typebot.io`.
- `api_token` (optional): Bearer token; required for private Typebots.
- `public_name` (required): Typebot public name/slug.
- `trigger_type` (required): `all` (any incoming message) or `keyword`.
- `trigger_operator` (keyword trigger): One of `contains` (default), `equals`, `starts_with`, `ends_with`, `regex`.
- `trigger_value` (keyword trigger): The keyword or regex pattern to match.
- `finish_keyword` (optional): Incoming message content that forces a handoff and session reset.
- `debounce_time` (optional): Seconds to delay sending the request to Typebot (useful when messages come in bursts).
- `default_delay_message` (optional): Seconds to wait between multiple Typebot responses when they arrive in a batch.
- `expire_in_minutes` (optional): If set, the session id is cleared after this timeout and the conversation is reopened.
- Ignoring rules (optional):
  - `ignore_groups` (boolean): Skip Typebot for group conversations (e.g., WhatsApp groups).
  - `ignored_targets` (array): Email/phone identifiers to bypass Typebot (exact match; phone numbers are normalized to digits).

## Prefilled variables sent to Typebot

Sent only on the first request of a session:

- Contact: `contact_name`, `contact_email`, `contact_phone`, `contact_id`, `contact_labels`, `contact_attributes`, `contact_custom_attribute_<key>`
- Conversation: `conversation_labels`, `conversation_id`, `conversation_display_id`, `conversation_attributes`, `custom_attribute_<key>`
- Account: `account_id`

`<key>` values are sanitized to lowercase snake_case.

## Message flow

- Mega aggregates the latest incoming public messages (text + attachment URLs) into a single request payload. The last message id is sent as `metadata.replyId`.
- If a session id is present in state, requests go to `/api/v1/sessions/:sessionId/continueChat`; otherwise to `/api/v1/typebots/:publicName/startChat`.
- Typebot responses are sequenced and delivered to the conversation. `default_delay_message` controls spacing between multiple messages.
- Attachments from Typebot map to Mega file types (image, video, audio, file, embed/document). Videos fall back to link-only content if download is not supported.
- Rich text is converted to Markdown-like text (bold/italic/underline) with block separation preserved.

## Session lifecycle and handoff

- Conversation state is stored under `conversation.additional_attributes['typebot']` (session id, result id, pending message markers, outgoing sequence counters).
- Handoff happens when:
  - Typebot marks the flow as finished (status/keywords) **and** all pending outgoing messages are sent, or
  - The `finish_keyword` is received, or
  - Ignoring rules match the contact/number.
- Closing or reopening a conversation triggers a session reset. `expire_in_minutes` also clears the session id and reopens the conversation when the timer elapses.

## Troubleshooting tips

- Ensure `public_name` matches the Typebot publish slug and `api_token` is set for private bots.
- For keyword triggers, confirm both `trigger_operator` and `trigger_value` are configured.
- If responses stop mid-flow, check `additional_attributes.typebot` on the conversation for a stale `session_id` and consider using the finish keyword or reopening/closing the conversation to reset.
