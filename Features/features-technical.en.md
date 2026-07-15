# MEGA - Technical Feature Detail (EN)

Version: Enterprise
Last updated: July 15, 2026
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
- Mega Hub for Meta: optional Super Admin mode to connect WhatsApp, Messenger, and Instagram using shared Hub apps; the Hub credentials block is configured in Super Admin → Mega Hub, and created inboxes still send through native services and receive relayed webhook events.
- WhatsApp Cloud connection health: manual-token failures are surfaced without blocking inbound webhook processing, while embedded signup still uses the reauthorization flow.
- WhatsApp Evolution, WAHA, and Uazapi: alternative providers with multimedia and group support.
- Provider-specific connection status: WAHA, Evolution, and Uazapi use their own APIs and webhooks; Meta signature validation is reserved for WhatsApp Cloud.
- WAHA passkey linking: proactive extension detection via `WAHA_PASSKEY_CHROME_EXTENSION_ID`, `PASSKEY_REQUIRED` and `PASSKEY_CONFIRMATION_REQUIRED` states inside `session.status`, challenge retrieval through `/auth/passkey/challenge`, temporary assertion handoff, browser-extension signing on `web.whatsapp.com`, and manual code confirmation; GET requests return `422` when no data is pending.
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
- Inboxes expose `auto_assign_on_agent_reply` to keep unassigned conversations unassigned when an agent sends an outgoing message.
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
- Vuex `chatRooms` centralizes rooms, messages, thread replies, categories, drafts, and search results; the UI exposes filters, sections, quick creation, DMs, drafts, polls, the thread side panel, and channel editing from the header action menu.
- Realtime delivery through Action Cable and `CHAT_ROOM_*` events for message, room, reaction, poll, read state, and typing changes.
- WebRTC audio/video calls persist lifecycle state in `chat_room_calls`, track attendees in `chat_room_call_participants`, relay ephemeral SDP/ICE through `RoomChannel`, and reuse `ring.mp3`/`calling.mp3` tones.
- Accounts with `chat_room_calls` receive only Google's `DEFAULT_STUN_URL`; enabling `premium_call_connectivity` makes `Mega::Calls::IceConfig` load `MEGA_CALL_STUN_URLS`, `MEGA_CALL_TURN_URLS`, `MEGA_CALL_TURN_USERNAME`, and `MEGA_CALL_TURN_CREDENTIAL` through `GlobalConfigService`. Saved Super Admin > Call ICE values take priority, existing environment variables are migrated, and TURN is published only when all three TURN fields are complete.
- Native video normalizes camera and display as independent streams, renegotiates an additional display sender without interrupting camera publication, and renders a bounded or floating workspace with a presentation stage and participant rail; Rails authorizes group mute against the call initiator, and the P2P topology remains intended for controlled small groups.
- Live calls require both account features, `chat_rooms` and the disabled-by-default `chat_room_calls`; `premium_call_connectivity` only selects the ICE transport. The Calls API returns `403 feature_disabled` and `RoomChannel` relays no SDP/ICE when either required feature is off, while stored call messages remain readable.
- Calls with three or more members track each invitee as `pending`/`joined`/`declined`; ringing continues until every invitee declines or the initiator ends the call.
- The audience comes from `OnlineStatusTracker`: a 1:1 call is not created when its recipient is offline, and group calls invite only members with `online` presence.
- Each call creates one `voice_call` `chat_room_message`; that record transitions through `ringing`, `in-progress`, `no-answer`, and `completed`, feeding room history and list previews in real time.
- The audio flow reuses the `FloatingCallWidget` visual pattern: logical RTL/LTR positioning, responsive width, `n-call-widget-*` tokens, status and identity hierarchy, and circular controls; it retains its own WebRTC state and keeps video isolated.
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

- Agent Bots per inbox with smart handover; manual assignment selectors expose only active bots configured on every requested inbox.
- Extended Typebot with MEGA_CMD commands for agent/team assignment.
- Typebot ignores WhatsApp reactions to avoid artificial starts or messages.
- Per-channel webhook signatures for outbound authenticity validation.

### 3.5 Captain AI

- Supported providers: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: inbox-level configuration with custom instructions and context.
- Assistant overview: Enterprise stats, drilldown, and cached summary endpoints backed by `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder`, and `Captain::OverviewSummaryService`; estimated time saved is derived from public assistant replies using a fixed 2-minute agent effort assumption per reply.
- Captain model routing by feature (`assistant`, `copilot`, `document_faq_generation`, `pdf_faq_generation`, `audio_transcription`, etc.) with account overrides and global configuration fallback.
- Captain Documents: upload, indexing, plan-based auto-sync with jitter, a purgable queue, configurable per-account and global limits, and a details view for crawled content, source metadata, and generated FAQ counts.
- Captain Scenarios: activation rules and priority ordering.
- Captain Custom Tools: HTTP integrations with GET, POST, PUT, PATCH, DELETE.
- Native account MCP servers: dedicated endpoints per slug at /mcp/:account_id/:slug.
- MCP OAuth: .well-known metadata, register, authorize, token, refresh token, and PKCE.
- Dual authentication: Bearer OAuth or static Api-Access-Token.
- Curated MCP catalog for daily use: stable domain tool names (conversations, contacts, inboxes, help center, reports, kanban, and more).
- Published MCP tools: base tools (account_context, account_actions_list, account_action_call) + curated catalog; includes Help Center read/search with `help_center_articles_list`, `help_center_articles_search`, `help_center_articles_get`, and `help_center_categories_list`; explicit dynamic tools via allowed_tools.
- Auto-resolve mode: evaluated, legacy, or disabled per account. Evaluated mode sends conversation status and labeled non-private message content to the evaluator; pending handoffs and follow-ups are kept open.

### 3.6 CRM and contact management

- Custom attributes by data type and automation usage.
- Role-based visibility controls for sensitive attributes (Enterprise).
- Labels on contacts and conversations.
- Companies grouped by domain with unified timeline.
- Contact payloads expose `company_id` when Companies is enabled; contact updates can set or clear the company and keep `additional_attributes.company_name` synchronized.
- Contact import and export available to administrators and Enterprise roles with the `contact_manage` permission.
- Intercom import is administrator-only and feature-gated by `data_import`; source credentials and durable mappings are stored per account.
- Contacts and conversation pages are processed through Sidekiq jobs, with idempotent item/mapping records, skip/error logs, resumable runs, and source-bucket API inboxes.
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
- Account-level Google Calendar sync can upsert scheduled/deadline items into `CalendarEvent` records without overwriting legacy `item_details` Google fields.
- Calendar reminders run every minute, create one idempotent `Notification` with `CalendarEvent` as actor for `created_by_user_id`, and reuse targeted ActionCable, Web Push, and snooze delivery; guest email metadata never determines the internal recipient.
- Kanban item calendar controls read `CalendarEvent`/`ExternalCalendarEvent`, expose Google links when available, and keep legacy Google IDs as fallback-only data.
- Stage-driven automations and quick-message options.
- Realtime synchronization with chat list and contact panel.
- The contact/conversation panel reuses the funnel agent candidates and persists assignment/removal through the Kanban item endpoints.
- The contact/conversation panel Kanban block is hidden when the user has no visible items and no accessible funnels to create items.
- The main sidebar Kanban entry is hidden for non-admin users when they have no accessible active funnels.
- Funnel agent changes emit a realtime event to refresh the sidebar, funnels and visible items without a reload.
- A Kanban item can link multiple conversations: `conversation_display_id` keeps the primary conversation for compatibility and `item_details.conversation_ids` stores the full set; visibility, filters, chat-list realtime, and the ContactPanel Kanban block consider any linked conversation. The relationship picker is limited to the funnel inboxes and shows the channel icon/inbox name.
- If a linked conversation is deleted, the Kanban item remains as history and the broken relationship is cleared.
- Consistent access scope across the API, cache, and realtime events: administrators can view every funnel and item; `agent` and the custom-role permission `kanban_view` receive only authorized resources.
- The custom-role permission `kanban_manage` includes the board and manager; funnels containing authorized items are exposed read-only, while only funnels assigned through `settings.agents` may have their content and structure edited. It cannot create, duplicate, delete, set the default, or change `unassigned_visibility`.
- Items retain `created_by_id`, so the creator always keeps visibility. With a valid linked conversation, the current assignee can view it only when also selected on the funnel, and any manually assigned item agent can view it; a stale link is visible only to the administrator and creator.
- `unassigned_visibility` supports `everyone` (the legacy/default value) and `assigned_only`; it determines visibility for items without direct assignment or linked conversations without an assignee.
- Candidates in `settings.agents` must have access to at least one inbox in `settings.inboxes`; the union is recalculated as inboxes change and blocks invalid new assignments.
- Global configuration is readable by `agent`, `kanban_view`, `kanban_manage`, and administrators; create, update, and delete require an administrator. Global automation endpoints are administrator-only; `kanban_manage` modifies assigned funnels only.

### 3.10 Integrations and extensibility

- Webhooks with enriched payload and global HMAC-SHA256 secret.
- `inbox_updated` webhook event for inbox state changes and disconnects.
- Dashboard Apps for embedded iFrame extensions by context; authenticated account users can read them, while only administrators can create, update, or delete them.
- Dashboard Scripts (Super Admin) for global customization without core edits.
- Platform Apps for high-level external integrations via API.
- Business integrations: Slack, Linear, Shopify, WooCommerce, Notion, CRM, Google Calendar.
- Google Calendar uses account-scoped OAuth/config APIs, selected `CalendarConnection`, internal `CalendarEvent`, and provider mapping through `ExternalCalendarEvent`; `settings.import_all_calendars` controls inbound scope independently from the concrete outbound `calendar_id`.
- The operational calendar route `/app/accounts/:accountId/calendar` reads local `calendar_events` for day, week, month, list, create, edit, cancel, sync on save, and manual fallback sync. `CalendarSync::PollConnectionsJob` runs every five minutes and imports Google changes with per-calendar `last_polled_at` stored under `CalendarConnection.settings`; recurring instances are expanded within a rolling one-year lookback and five-year lookahead.
- Calendar navigation, the operational route, composer action, and conversation-panel section require the account feature, complete global OAuth credentials, and a connected `GoogleCalendarIntegration` with `CalendarConnection#calendar_id`; bootstrap payloads expose only availability/configuration booleans.
- The month view limits each cell to two visible events to reserve space for a `+N more` control; right-click opens event actions and each row still opens the editor. Color is stored in `metadata.color_id` and permanent deletion requires an administrator.
- `calendar_events` responses include lightweight contact, conversation, and Kanban item summaries for searchable relation selectors; edit payloads send `null` to unlink relations.
- The calendar relation selector searches Kanban items across the account instead of inheriting the currently selected funnel, and accepts item IDs (including `#ID` format).
- Checklist tasks have independent Google Calendar sync settings and destination calendars; each synchronized task is stored as its own event linked by `checklist_item_id`.
- The assigned checklist agent is added as a Google attendee and receives the platform reminder; completing or deleting the task cancels its event and pending reminder.
- The conversation reply composer loads the account connection and writable calendars before opening the shared `CalendarEventDialog`; the explicit “Create and send” action formats its `saved` result with localized event fields and sends it once through `createPendingMessageAndSend`, using `metadata.google_meet_url` without retrying event creation if messaging fails.
- The conversation contact panel filters `calendar_events` by `conversation_display_id`, recalculates Start-to-End progress every 30 seconds for a pulsing green (<50%), yellow (50–90%), or red (≥90%) dot, fades expired entries, reuses `CalendarEventDialog`, and consumes saved-event updates.
- `GoogleCalendar::EventMapperService` maps event metadata into Google fields for location, attendees, reminders, simple recurrence, availability, visibility, guest permissions, and Google Meet.
- The responsive event editor uses icon-led rows, an IANA time-zone selector, and removable guest chips; the sidebar places vertical MEGA context below guest permissions with floating searches and the inbox channel icon on every conversation result; it persists the writable destination and returned Meet URL.
- Google Calendar supports manual inbound import through `google_calendar_integration/import_events` and legacy Kanban backfill through `google_calendar_integration/backfill_kanban`; Flow Builder triggers remain deferred.
- PWA assets generated dynamically from global configuration, with configurable icon background and cache invalidated by logo, color, and blob timestamp.

### 3.11 Signup and onboarding

- Guided account-profile completion through the dedicated admin endpoint `/api/v1/accounts/:account_id/onboarding`.
- Website persistence as a fully qualified URL for downstream consumers such as Help Center and brand enrichment.
- Separation between general account updates and completion of the `account_details` step.
- The Instagram OAuth callback preserves the signed `return_to` hint to resume inbox setup when authorization starts from onboarding.

### 3.12 Security and compliance

- 2FA/MFA, SAML/SSO, custom roles, and audit logs.
- User session records support an agent-editable `custom_name` label; IP metadata remains internal and is not exposed in dashboard session payloads.
- Suspended-account dashboard state keeps the support widget visible and exposes an explicit support action.
- Mega license protection in deployment flows.
- Release observability for version-level traceability.

## 4. Operations and validation

### API parity and Postman collection

Supported routes under `/api`, `/platform/api`, and `/public/api` are compared with OpenAPI 3.1 by normalized method and path. Validation detects missing, stale, or duplicate operations; it does not claim test coverage for every response field. `bundle exec rake swagger:build` regenerates Swagger and `swagger/postman_collection.json`, organized into `Account API Token`, `Platform App Token`, and `Public / No Token` with independent credential variables.

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
