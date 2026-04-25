# MEGA - Technical Feature Detail (EN)

Version: Enterprise
Last updated: April 25, 2026
Language: English

## 1. Purpose

This document explains how core MEGA features are implemented from a technical perspective.
It complements [features.en.md](features.en.md), which is focused on commercial and presentation use.

## 2. Base stack and architecture

- Main backend: Ruby on Rails.
- Dashboard frontend: Vue 3.
- Enterprise overlay: extensions and overrides under enterprise.
- Async processing: Sidekiq background jobs.
- Realtime layer: Action Cable for conversations, rooms, and boards.
- Persistence: PostgreSQL as primary database.
- API security: permission policies and role-based controls.

## 3. Functional domains

### 3.1 Messaging and voice channels

- WhatsApp Cloud API: official channel with templates and delivery events.
- WhatsApp Evolution, WAHA, and Uazapi: alternative providers with multimedia and group support.
- Notificame: official-oriented variant for LATAM operations.
- Instagram, Facebook, TikTok, Telegram, X, SMS, and Email exposed as inbox channels.
- API Channel: generic gateway for proprietary platforms via API/webhooks.
- Twilio voice and WhatsApp Cloud calls: WebRTC flow with unified timeline.

### 3.2 Conversation core

- Status model: open, pending, resolved, snoozed.
- Priority model: urgency handling per conversation.
- Participants: multi-agent collaboration in the same thread.
- Drafts and pinned: per-agent workflow continuity.
- Advanced filters and custom views: high-volume operational segmentation.
- Assignment V2: smart distribution with capacity and policy rules.

### 3.3 Automation and bots

Supported events:

- Conversation created and updated.
- Message received and created.

Conditions:

- Status, inbox, labels, language, attributes, content.
- Private note condition for internal-only workflows.

Actions:

- Assign agent or team.
- Assign last responding agent.
- Remove agent or team assignment.
- Labeling, status/priority update, webhook send, mute.

Bots:

- Agent Bots per inbox with smart handover.
- Extended Typebot with MEGA_CMD commands for agent/team assignment.
- Per-channel webhook signatures for outbound authenticity validation.

### 3.4 Captain AI

- Supported providers: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: inbox-level configuration with custom instructions and context.
- Captain Documents: upload, indexing, and auto-sync fields.
- Captain Scenarios: activation rules and priority ordering.
- Captain Custom Tools: HTTP integrations with GET, POST, PUT, PATCH, DELETE.
- MCP Servers: capability extension through Model Context Protocol.
- Auto-resolve mode: evaluated, legacy, or disabled per account.

### 3.5 CRM and contact management

- Custom attributes by data type and automation usage.
- Role-based visibility controls for sensitive attributes (Enterprise).
- Labels on contacts and conversations.
- Companies grouped by domain with unified timeline.
- Active WhatsApp blocking to drop inbound messages from blocked contacts.

### 3.6 Campaigns

- Ongoing campaigns for widget/live chat.
- One-off campaigns for WhatsApp, SMS, and API Channel.
- Meta template builder with approval lifecycle and sync.
- Rate control, multi-inbox rotation, and execution metrics.

### 3.7 Help Center

- Multi-language articles with per-language draft state.
- Editor with slash menu and native table support.
- Conversation insertion flow with stable popover search.
- Embedding search in Enterprise for semantic retrieval.

### 3.8 Sales Kanban (Mega)

- Funnels with configurable stages and default stage support.
- Board and list views for distinct team workflows.
- Filters by inbox, channel, stage, and activity.
- 360 item workspace: checklist, notes, attachments, offers, agents, attributes.
- Native links to contact and conversation.
- Stage-driven automations and quick-message options.
- Realtime synchronization with chat list and contact panel.

### 3.9 Integrations and extensibility

- Webhooks with enriched payload and global HMAC-SHA256 secret.
- Dashboard Apps for embedded iFrame extensions by context.
- Dashboard Scripts (Super Admin) for global customization without core edits.
- Platform Apps for high-level external integrations via API.
- Business integrations: Slack, Linear, Shopify, WooCommerce, Notion, CRM.

### 3.10 Security and compliance

- 2FA/MFA, SAML/SSO, custom roles, and audit logs.
- Mega license protection in deployment flows.
- Release observability for version-level traceability.

## 4. Operations and validation

Recommended checklist for feature-level changes:

1. Validate role permissions and account boundaries.
2. Validate realtime events under concurrent usage.
3. Run unit tests for the affected domain.
4. Run browser-level manual validation for full user flow.
5. Verify i18n parity in ES, EN, and PT-BR for new strings.

## 5. Related technical references

- [docs/kanban_api_reference_en.md](../kanban_api_reference_en.md)
- [docs/chat_rooms_api_reference_en.md](../chat_rooms_api_reference_en.md)
- [docs/scheduled_messages_api_reference_en.md](../scheduled_messages_api_reference_en.md)
- [docs/platform_banners_api_reference.md](../platform_banners_api_reference.md)
- [docs/whatsapp_voice_calls.md](../whatsapp_voice_calls.md)
