# MEGA - Technical Feature Detail (EN)

Version: Enterprise
Last updated: July 3, 2026
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
- Mega Hub for Meta: optional Super Admin mode to connect WhatsApp, Messenger, and Instagram using shared Hub apps; created inboxes still send through native services and receive relayed webhook events.
- WhatsApp Cloud connection health: manual-token failures are surfaced without blocking inbound webhook processing, while embedded signup still uses the reauthorization flow.
- WhatsApp Evolution, WAHA, and Uazapi: alternative providers with multimedia and group support.
- WAHA passkey linking: proactive extension detection via `WAHA_PASSKEY_CHROME_EXTENSION_ID`, installation notice, `passkey.required` status/webhook detection, temporary token flow for challenge/assertion handoff, browser-extension signing on `web.whatsapp.com`, and manual code confirmation when WAHA emits `passkey.confirmation.required`.
- On-demand global sync for WAHA and Uazapi: Sidekiq jobs with Redis progress, 24h/7d windows, provider-id deduplication, open-conversation reuse, asynchronous historical media downloads, account-level concurrency locks, and an optional dedicated `whatsapp_history_sync` worker for high-volume installations.
- Per-conversation sync for WAHA and Uazapi: manual action from the conversation menu, with 24h/7d windows and provider-id deduplication.
- WhatsApp reactions: dashboard and API-token actors can add, replace, and remove one reaction per message while preserving WhatsApp Device echoes.
- Notificame: official-oriented variant for LATAM operations.
- Instagram, Facebook, TikTok, Telegram, X, SMS, and Email exposed as inbox channels.
- IMAP email processing with a dedicated timeout to avoid stuck mailbox jobs.
- Email provider inference from signup-domain MX records to suggest Gmail or Outlook integrations during onboarding.
- Attachment uploads with explicit `.pfx` recognition alongside common media and document formats.
- API Channel: generic gateway for proprietary platforms via API/webhooks.
- Twilio voice and WhatsApp Cloud calls: WebRTC flow with unified timeline; Twilio reports normalize data from the Call model, optional native recordings require storage-cost acceptance, and recordings are exposed in conversations and call reports.
- Audio transcription controls: GPT-4o Mini Transcribe defaults for voice notes with Whisper available as an account override; call recordings keep account-level flags for master enablement and per-provider behavior (WhatsApp Cloud and WaVoIP), audio normalization, turn-based diarization, higher-fidelity GPT-4o Transcribe text, contact/assigned-agent name labels, and manual retry from the context menu for audio messages without text.
- WaVoIP with per-inbox session persistence and role-aware credential reuse.

### 3.2 Conversation core

- Status model: open, pending, resolved, snoozed.
- Priority model: urgency handling per conversation.
- Participants: multi-agent collaboration in the same thread.
- Drafts and pinned: per-agent workflow continuity.
- Advanced filters and custom views: high-volume operational segmentation.
- Dedicated unread sort mode in the conversation list.
- Dedicated sidebar filters: unread, mentions, participating, groups, and unattended conversation views.
- Reactive sidebar counters: unread per conversation type and mentions via notification_type=conversation_mention.
- Assignment V2: smart distribution with capacity and policy rules.
- Teams: `icon` and `icon_color` are persisted on `teams`, exposed through API/model JSON, and included in realtime payloads for lists and assignment pickers.
- Enterprise SLA: `AppliedSla` exposes backend-computed FRT/NRT/RT deadlines; when the policy uses business hours, `Sla::BusinessHoursService` consumes the inbox working-hours configuration and the JSON response returns `sla_*_due_at` values to the dashboard. Conversations with blocked contacts reject new SLA assignment, are excluded from processing/reports, and clear `sla_policy_id`, `applied_sla`, and `sla_events` from payloads while blocked.
- V2 report drilldown: `/api/v2/accounts/:account_id/reports/drilldown` returns the conversations, messages, or reporting events behind a chart bar; `V2::Reports::DrilldownBuilder` validates the metric, bucket, administrator permission, pagination, account/inbox/agent/team/label filters, business hours, and last-message serialization, with a dedicated Rack::Attack rate limit.
- Canned responses with reusable attachments also available in new conversation flows.
- Reply editor inline image upload for Email and Web Widget, ProseMirror resizing, and safe `cw_image_width`/`cw_image_height` rendering.
- WhatsApp `reply_to` resolution honors `conversation_history` by matching quoted message identifiers in previous conversations for the same contact inbox, without expanding to account-wide message search.
- Agent offboarding flow with assigned-conversation review and bulk unassign/reassign options constrained by inbox/team access.

### 3.3 Internal communication and rooms

- Chat Rooms remains a dedicated domain on the existing base: `chat_rooms`, `chat_room_members`, and `chat_room_messages`.
- Internal parity is extended with `chat_room_categories`, `chat_room_drafts`, `chat_room_reactions`, `chat_room_polls`, `chat_room_poll_options`, `chat_room_poll_votes`, and `chat_room_teams`.
- Room types: `public_channel`, `private_channel`, and `direct_message`, with optional names for DMs and reuse of existing DMs by member combination.
- Account-scoped API for rooms, members, categories, drafts, reactions, polls, search, read/unread state, archive state, and typing status.
- Search uses `f_unaccent` across channels, DMs, and accessible messages.
- Vuex `chatRooms` centralizes rooms, messages, thread replies, categories, drafts, and search results; the UI exposes filters, sections, quick creation, DMs, drafts, polls, and the thread side panel.
- Realtime delivery through Action Cable and `CHAT_ROOM_*` events for message, room, reaction, poll, read state, and typing changes.
- Webhooks can emit chat room events without mixing the customer conversation contract.

### 3.4 Automation and bots

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
- Typebot ignores WhatsApp reactions to avoid artificial starts or messages.
- Per-channel webhook signatures for outbound authenticity validation.

### 3.5 Captain AI

- Supported providers: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: inbox-level configuration with custom instructions and context.
- Assistant overview: Enterprise stats, drilldown, and cached summary endpoints backed by `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder`, and `Captain::OverviewSummaryService`; estimated time saved is derived from public assistant replies using a fixed 2-minute agent effort assumption per reply.
- Captain model routing by feature (`assistant`, `copilot`, `document_faq_generation`, `pdf_faq_generation`, `audio_transcription`, etc.) with account overrides and global configuration fallback.
- Captain Documents: upload, indexing, and plan-based auto-sync with jitter, a purgable queue, and configurable per-account and global limits.
- Captain Scenarios: activation rules and priority ordering.
- Captain Custom Tools: HTTP integrations with GET, POST, PUT, PATCH, DELETE.
- Native account MCP servers: dedicated endpoints per slug at /mcp/:account_id/:slug.
- MCP OAuth: .well-known metadata, register, authorize, token, refresh token, and PKCE.
- Dual authentication: Bearer OAuth or static Api-Access-Token.
- Curated MCP catalog for daily use: stable domain tool names (conversations, contacts, inboxes, help center, reports, kanban, and more).
- Published MCP tools: base tools (account_context, account_actions_list, account_action_call) + curated catalog; includes Help Center read/search with `help_center_articles_list`, `help_center_articles_search`, `help_center_articles_get`, and `help_center_categories_list`; explicit dynamic tools via allowed_tools.
- Auto-resolve mode: evaluated, legacy, or disabled per account.

### 3.6 CRM and contact management

- Custom attributes by data type and automation usage.
- Role-based visibility controls for sensitive attributes (Enterprise).
- Labels on contacts and conversations.
- Companies grouped by domain with unified timeline.
- Contact payloads expose `company_id` when Companies is enabled; contact updates can set or clear the company and keep `additional_attributes.company_name` synchronized.
- Contact import and export available to administrators and Enterprise roles with the `contact_manage` permission.
- Active WhatsApp blocking to drop inbound messages from blocked contacts.

### 3.7 Campaigns

- Ongoing campaigns for widget/live chat.
- One-off campaigns for WhatsApp, SMS, and API Channel.
- Meta template builder with approval lifecycle and sync.
- Rate control, multi-inbox rotation, and execution metrics.

### 3.8 Help Center

- Multi-language articles with per-language draft state.
- Selectable portal layouts: classic landing page or documentation sidebar mode.
- Editor with slash menu and native table support.
- Article creation directly from category views.
- In-editor image resizing for article composition.
- Conversation insertion flow with stable popover search.
- Embedding search in Enterprise for semantic retrieval.
- Assisted FAQ generation from PDF with additional context and selective publishing (Enterprise).

### 3.9 Sales Kanban (Mega)

- Funnels with configurable stages and default stage support.
- Board and list views for distinct team workflows.
- Filters by inbox, channel, stage, and activity.
- Conversation label filters in board/list views and stage statistics.
- Label management from item cards with an item-level API endpoint.
- 360 item workspace: checklist, notes, attachments, offers, agents, attributes.
- Remote conversation/contact lookup in item relationship selectors.
- Account-level base currency via `accounts.update` (`settings.default_currency`).
- Monetary custom offers support per-offer currency (`item_details.offers[].currency`) as an override over account default.
- Items without offers render without currency and are excluded from monetary totals to prevent fallback-based mixing.
- Native links to contact and conversation.
- Stage-driven automations and quick-message options.
- Realtime synchronization with chat list and contact panel.

### 3.10 Integrations and extensibility

- Webhooks with enriched payload and global HMAC-SHA256 secret.
- `inbox_updated` webhook event for inbox state changes and disconnects.
- Dashboard Apps for embedded iFrame extensions by context.
- Dashboard Scripts (Super Admin) for global customization without core edits.
- Platform Apps for high-level external integrations via API.
- Business integrations: Slack, Linear, Shopify, WooCommerce, Notion, CRM.
- PWA assets generated dynamically from global configuration, with configurable icon background and cache invalidated by logo, color, and blob timestamp.

### 3.11 Signup and onboarding

- Guided account-profile completion through the dedicated admin endpoint `/api/v1/accounts/:account_id/onboarding`.
- Website persistence as a fully qualified URL for downstream consumers such as Help Center and brand enrichment.
- Separation between general account updates and completion of the `account_details` step.
- The Instagram OAuth callback preserves the signed `return_to` hint to resume inbox setup when authorization starts from onboarding.

### 3.12 Security and compliance

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
