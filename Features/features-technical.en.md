# MEGA - Technical Feature Detail (EN)

Version: Enterprise
Last updated: July 31, 2026
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

- WhatsApp Cloud API: official channel with templates and delivery events; outside the 24-hour customer service window, the service locally rejects automation free-form messages without template parameters before contacting the provider.
- Mega Hub for Meta: optional Super Admin mode to connect WhatsApp, Messenger, and Instagram using shared Hub apps; the Hub credentials block is configured in Super Admin → Mega Hub, and created inboxes still send through native services and receive relayed webhook events.
- WhatsApp Cloud connection health: manual-token failures are surfaced without blocking inbound webhook processing, while embedded signup still uses the reauthorization flow.
- WhatsApp Cloud phone health persists its available phone-level data when optional WABA business enrichment fails, retains the last business metadata, and records the enrichment error separately.
- Embedded-signup WhatsApp Cloud inboxes can use a feature-flagged guided manual migration to a customer-owned Meta app; the flow validates WABA, phone-number, and token credentials before updating the connection, while the reauthorization alert remains visible when required.
- On Cloud, `whatsapp_embedded_signup_inbox_creation` is the single gate for embedded-signup inbox creation, proactive reconfiguration, and reauthorization. Self-hosted installations retain `whatsapp_reconfigure` for proactive reconfiguration; the endpoint requires an administrator and preserves recovery when reauthorization is required.
- WhatsApp Evolution, WAHA, and Uazapi: alternative providers with multimedia and group support.
- Unsupported WhatsApp placeholders retain `unsupported_reason`, code, and subtype when Meta provides them. Only `131060` is classified as coexistence unavailability; `131051`, other types, and legacy rows use neutral guidance. Outgoing messages without sendable content or a WAHA response are marked failed rather than unsupported inbound content.
- Provider-specific connection status: WAHA, Evolution, and Uazapi use their own APIs and webhooks; Meta signature validation is reserved for WhatsApp Cloud.
- WAHA passkey linking: proactive extension detection via `WAHA_PASSKEY_CHROME_EXTENSION_ID`, `PASSKEY_REQUIRED` and `PASSKEY_CONFIRMATION_REQUIRED` states inside `session.status`, challenge retrieval through `/auth/passkey/challenge`, temporary assertion handoff, browser-extension signing on `web.whatsapp.com`, and manual code confirmation; GET requests return `422` when no data is pending.
- On-demand global sync for WAHA and Uazapi: Sidekiq jobs with Redis progress, 24h/7d windows, provider-id deduplication, open-conversation reuse, asynchronous historical media downloads, account-level concurrency locks, and an optional dedicated `whatsapp_history_sync` worker for high-volume installations.
- Per-conversation sync for WAHA and Uazapi: manual action from the conversation menu, with 24h/7d windows and provider-id deduplication.
- WhatsApp reactions: dashboard and API-token actors can add, replace, and remove one reaction per message while preserving WhatsApp Device echoes.
- Notificame: official-oriented variant for LATAM operations.
- Instagram, Facebook, TikTok, Telegram, X, SMS, and Email exposed as inbox channels.
- IMAP email processing with a dedicated timeout to avoid stuck mailbox jobs.
- Gmail inbox connection diagnostics with live IMAP/SMTP XOAUTH2 authentication, safe error categories, recent incoming/outgoing activity timestamps, and administrator-only OAuth reconnection.
- Email provider inference from signup-domain MX records to suggest Gmail or Outlook integrations during onboarding.
- Attachment uploads with explicit `.pfx` recognition alongside common media and document formats.
- API Channel: generic gateway for proprietary platforms via API/webhooks.
- Widget pre-chat form: checkboxes marked required use the form acceptance rule, so submission remains blocked until they are selected; the localized required-field message is retained.
- Twilio voice and WhatsApp Cloud calls: WebRTC flow with a unified timeline; Cloud calls from profiles without a conversation safely resolve or create the contact thread while honoring inbox continuity and agent visibility. Call permission can use an approved template selected from ReplyBox or configured as the inbox default, retains the WAMID to correlate the reply, and records the outgoing message in the conversation without sending it to the provider twice. Meta queries are the source of truth: they normalize and persist no-permission, temporary, and permanent states, and honor the `start_call` action before starting a call; every change is recorded as activity, with Meta's expiry date for temporary permissions. Client and server prevent a second active call per agent, including across tabs. Inbox candidates are determined by the standard assignment rules —capacity, team, and overflow— and agents already on a call are excluded; an online administrator who enabled call notifications enters only as a fallback when no eligible agent remains. While a Cloud call is accepting, connecting, or active, both the UI and model reject agent and team changes; a ringing call remains reassignable and reassignment is available again after termination. Calling controls, permission requests, call initiation, and call webhooks are disabled for Cloud channels marked as WhatsApp Business App coexistence, because calling remains in the WhatsApp Business app. Twilio reports normalize data from the Call model, optional native recordings require storage-cost acceptance, and recordings are exposed in conversations and call reports.
- Audio transcription controls: GPT-4o Mini Transcribe defaults for voice notes with Whisper available as an account override; call recordings keep account-level flags for master enablement and per-provider behavior (WhatsApp Cloud and WaVoIP), audio normalization, turn-based diarization, higher-fidelity GPT-4o Transcribe text, contact/assigned-agent name labels, and manual retry from the context menu for audio messages without text.
- WaVoIP with per-inbox session persistence and role-aware credential reuse.

### 3.2 Conversation core

- Widget email-transcript requests disable their button while in flight and for 15 seconds after a successful send, preventing repeated delivery requests while retaining immediate retry after a failed request.
- CSAT feedback visibility is stored per inbox in `csat_config.hide_feedback_from_agents`. Dashboard message serializers and Action Cable redact only `feedback_message` for non-administrator account users, while ratings, persisted data, administrator payloads, and public customer payloads remain unchanged.
- Deleted messages may retain their original text for agents through `inboxes.show_deleted_message_placeholder`; the public API and contact-facing Action Cable broadcasts replace `content` and `processed_message_content` with the deletion notice and omit `content_attributes.original_content` and `translations` without changing the persisted record.
- Status model: open, pending, resolved, snoozed.
- Priority model: urgency handling per conversation.
- Participants: multi-agent collaboration in the same thread.
- Custom attributes API: `POST .../custom_attributes` keeps replacement as the default and accepts `merge=true` to update only supplied keys; `POST .../destroy_custom_attributes` removes specific keys and returns the remaining attributes.
- Drafts and pinned: per-agent workflow continuity.
- Advanced filters and custom views: high-volume operational segmentation.
- Dedicated unread sort mode in the conversation list.
- Dedicated sidebar filters: unread, mentions, participating, groups, and unattended conversation views.
- Reactive sidebar counters: unread per conversation type and mentions via notification_type=conversation_mention.
- Assignment V2: smart distribution with capacity and policy rules.
- Inboxes expose `auto_assign_on_agent_reply` to keep unassigned conversations unassigned when an agent sends an outgoing message.
- Multi-account users keep one avatar selector, but its upload and delete operations target the active `AccountUser` membership. Account-scoped agent and message payloads prefer that membership avatar and fall back to the global `User` avatar; single-account behavior remains global and no permission or account policy toggle is introduced.
- Teams: `icon` and `icon_color` are persisted on `teams`, exposed through API/model JSON, and included in realtime payloads for lists and assignment pickers.
- Enterprise SLA: `AppliedSla` exposes backend-computed FRT/NRT/RT deadlines; when the policy uses business hours, `Sla::BusinessHoursService` consumes the inbox working-hours configuration and the JSON response returns `sla_*_due_at` values to the dashboard. Resolving a conversation records `sla_completed_at`, freezing the displayed duration of FRT/NRT/RT misses; historical SLAs without that timestamp remain visible as static misses. Conversations with blocked contacts reject new SLA assignment, are excluded from processing/reports, and clear `sla_policy_id`, `applied_sla`, and `sla_events` from payloads while blocked.
- V2 report drilldown: `/api/v2/accounts/:account_id/reports/drilldown` returns the conversations, messages, or reporting events behind a chart bar; `V2::Reports::DrilldownBuilder` validates the metric, bucket, administrator permission, pagination, account/inbox/agent/team/label filters, business hours, and last-message serialization, with a dedicated Rack::Attack rate limit.
- Canned responses with reusable attachments also available in new conversation flows.
- Reply editor inline image upload for Email and Web Widget, ProseMirror resizing, and safe `cw_image_width`/`cw_image_height` rendering.
- WhatsApp `reply_to` resolution honors `conversation_history` by matching quoted message identifiers in previous conversations for the same contact inbox, without expanding to account-wide message search. In coexistence, it also links phone-scoped and BSUID-scoped WAMIDs sharing one decoded token; malformed or ambiguous identifiers remain unlinked.
- Agent offboarding flow with assigned-conversation review and bulk unassign/reassign options constrained by inbox/team access.
- Agent invitations atomically reserve daily email capacity in Redis before queueing mail; an exhausted limit rolls back only that invitation and returns HTTP 429, while bulk onboarding continues adding existing users.

### 3.3 Internal communication and rooms

- Chat Rooms remains a dedicated domain on the existing base: `chat_rooms`, `chat_room_members`, and `chat_room_messages`.
- Room names preserve their submitted casing; `chat_rooms` enforces account-scoped case-insensitive uniqueness with a unique `account_id, LOWER(name)` index.
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

- Delayed rules persist one claimed pending execution per rule, conversation, and state episode. A scheduled worker revalidates the feature flag, rule, and conditions before firing; status changes and replies invalidate the matching episode.

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
- New conversations and senderless campaigns for an active Agent Bot stay pending with the bot as owner; explicit human assignments are preserved, and handoff, human open, or bot disconnection clears bot ownership. Dialogflow, Captain, and ignored targets do not receive an Agent Bot owner.
- ReplyBox detects `AgentBot` ownership on pending conversations, forces the effective `NOTE` mode without overwriting reply drafts, and the takeover banner reopens and assigns the conversation to the current agent while updating the local assignee type.
- Extended Typebot with MEGA_CMD commands for agent/team assignment.
- Typebot ignores WhatsApp reactions to avoid artificial starts or messages.
- Per-channel webhook signatures for outbound authenticity validation.

### 3.5 Captain AI

- Supported providers: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: inbox-level configuration with custom instructions and context.
- Assistant overview: Enterprise stats, drilldown, and cached summary endpoints backed by `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder`, and `Captain::OverviewSummaryService`; the client reuses loaded stats for the summary, cancels superseded stats requests, retries a transient failure once, and renders metric skeletons while loading. Summaries use the account language; estimated time saved is derived from public assistant replies using a fixed 2-minute agent effort assumption per reply.
- Captain model routing by feature (`assistant`, `copilot`, `document_faq_generation`, `conversation_faq_matching`, `pdf_faq_generation`, `audio_transcription`, etc.) with account overrides and global configuration fallback.
- Conversation FAQ suggestions: a low-priority mutex job extracts only public customer and human-agent messages plus business context, rejects unsuitable conversations, and groups semantically matching observations by assistant and language; the Enterprise review API lists and previews only sources available to the current agent, supports edit/approve/dismiss while open, and locks reviews against concurrent approval. Approval creates an approved FAQ and retains its source observations; approved FAQs and dismissed suggestions suppress new duplicates.
- Generation details: Enterprise `GET /api/v1/accounts/:account_id/captain/agent_sessions/:message_id` authorizes the message conversation, hydrates citations and scenario titles, and supplies the Captain message popover. Sessions are cached per message; a handoff session is attached to its non-empty private reason note. Model and credit data render only for super administrators or development.
- Captain Documents: upload, indexing, plan-based auto-sync with jitter, a purgable queue, configurable per-account and global limits, and a details view for crawled content, source metadata, and generated FAQ counts.
- Captain Scenarios: activation rules and priority ordering.
- Captain Custom Tools: HTTP integrations with GET, POST, PUT, PATCH, DELETE.
- Native account MCP servers: dedicated endpoints per slug at /mcp/:account_id/:slug.
- The MCP POST endpoint keeps JSON-RPC over `application/json` and supports a `multipart/form-data` extension: `payload` contains the complete JSON-RPC request and `attachments[]` carries local files.
- Multipart uploads are restricted to `conversation_message_send`, its legacy alias, and `outbound_messages_create`; they enforce `MAXIMUM_FILE_UPLOAD_SIZE`, with 15 combined attachments for conversations and exactly one for outbound.
- Multipart is a Mega HTTP extension that requires explicit client support; standard JSON-only MCP clients do not use it automatically.
- The conversation direct-upload JSON handshake accepts the effective MCP user's API token, validates account and conversation access through the API/Pundit stack, and returns Active Storage's signed upload target without browser CSRF.
- `outbound_messages_create` exposes the complete universal contract through MCP: `body` retains the inbox, one recipient identity, text/media/template, and a signed blob; `idempotency_key` is forwarded only as `Idempotency-Key`. Media accepts exactly one source among signed ID, multipart, `file` with a temporary HTTPS URL, and `file_base64`; for template messages, that source is assigned to `template.parameters.header.media_file` instead of a regular attachment.
- The `_meta["openai/fileParams"]` descriptor lets ChatGPT deliver `file.download_url` and `file.file_id`; Claude and other clients can use the same descriptor, multipart, or the JSON base64 fallback. URLs pass through `SafeFetch` with SSRF protection and size limits, and temporary blobs are purged if the API fails.
- The outbound service verifies that every media signed ID resolves to a persisted blob with positive size and an existing storage object. An invalid, expired, or byte-less reference returns `422 invalid_attachment` before creating a message or invoking the provider.
- MCP OAuth: .well-known metadata, register, authorize, token, refresh token, and PKCE.
- Dual authentication: Bearer OAuth or static Api-Access-Token.
- Curated MCP catalog for daily use: stable domain tool names (conversations, contacts, inboxes, help center, reports, kanban, and more).
- Published MCP tools: base tools (account_context, account_actions_list, account_action_call) + curated catalog; includes message scheduling, tasks, templates, campaigns, SLA, policies, calendar, reports, Captain, notifications, internal chat, and the complete Help Center lifecycle; it does not publish data import or export tools; explicit dynamic tools via allowed_tools.
- Auto-resolve mode: evaluated, legacy, or disabled per account. Evaluated mode sends conversation status and labeled non-private message content to the evaluator; pending handoffs and follow-ups are kept open.

### 3.6 CRM and contact management

- Custom attributes by data type and automation usage.
- Role-based visibility controls for sensitive attributes (Enterprise).
- Labels on contacts and conversations.
- The conversation context menu's label submenu uses fuzzy search with `picoSearch`, shows assigned labels first without changing each group's source order, and supports repeated selection without moving focus away from search. Blank queries show every label, and the context menu closes only when focus leaves it.
- Companies grouped by domain with unified timeline.
- Contact payloads expose `company_id` when Companies is enabled; contact updates can set or clear the company and keep `additional_attributes.company_name` synchronized.
- Contact import and export available to administrators and Enterprise roles with the `contact_manage` permission.
- Intercom import is administrator-only and feature-gated by `data_import`; source credentials and durable mappings are stored per account.
- Contacts and conversation pages are processed through Sidekiq jobs, with idempotent item/mapping records, skip/error logs, resumable runs, and source-bucket API inboxes.
- Imports inactive for 15 minutes can be retried through an authorized account endpoint; retry acquires account/import locks, rotates the run identifier, and preserves cursor, statistics, and recorded errors.
- Active WhatsApp blocking to drop inbound messages from blocked contacts.

### 3.7 Campaigns

- Ongoing campaigns for widget/live chat.
- One-off campaigns for WhatsApp, SMS, and API Channel.
- Meta template builder with approval lifecycle and sync.
- Rate control, multi-inbox rotation, and execution metrics.

### 3.8 Help Center

- Multi-language articles with per-language draft state.
- Published article title/content edits are staged in draft columns, with review, publish, and discard flows that preserve the live version until publication.
- Selectable portal layouts: classic landing page or documentation sidebar mode.
- Recommended content per locale is stored in `portal.config.popular_content`, with ordered lists capped at 3 categories and 6 articles; deleted records and unpublished articles are omitted while popularity-based fallback remains available.
- Editor with slash menu, native tables, and supported-video URL insertion through a validated field; the URL is converted into the existing embed for preview in the editor and public portal.
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
- The shared item-creation form loads account labels and sends selected titles through `kanban_item.labels`; the create endpoint assigns them to the new item before its single persistence operation, without changing linked-conversation labels. Item cards retain the item-level label management endpoint.
- 360 item workspace: checklist, notes, attachments, offers, agents, attributes.
- Long Kanban notes use a details dialog with rendered Markdown, viewport-bounded scrolling, forced wrapping for unbroken text, attachment previews, and a permission-gated direct edit action.
- Remote conversation/contact lookup in item relationship selectors.
- Account-level base currency via `accounts.update` (`settings.default_currency`).
- Active monetary consumers resolve currency through the shared helper/composable with offer → item → account → locale precedence; old/new historical values are formatted independently and zero amounts remain visible.
- `funnels/:id/stage_stats` retains `count` and `total_value` and adds per-stage `value_totals` (`currency` or `label`, code, total, and distinct item count) across the complete filtered policy scope; `KanbanColumn` prioritizes that complete aggregate, uses local grouping only as a compatibility fallback, and exposes an accessible semantic-token tooltip.
- Monetary custom offers support per-offer currency (`item_details.offers[].currency`) as an override over account default.
- Items without offers render without currency and are excluded from monetary totals to prevent fallback-based mixing.
- Native links to contact and conversation.
- Account-level Google Calendar sync can upsert scheduled/deadline items into `CalendarEvent` records without overwriting legacy `item_details` Google fields.
- Calendar reminders run every minute, create one idempotent `Notification` with `CalendarEvent` as actor for `created_by_user_id`, and reuse targeted ActionCable, Web Push, and snooze delivery; guest email metadata never determines the internal recipient.
- Kanban item calendar controls mount only when the account has a connected `GoogleCalendarIntegration` and a `CalendarConnection#calendar_id`; they then read `CalendarEvent`/`ExternalCalendarEvent`, expose Google links when available, and keep legacy Google IDs as fallback-only data.
- Stage-driven automations and quick-message options.
- Timed `send_message` stage rules capture the primary conversation ID and latest incoming message ID when scheduled. `StageTimeAutomationJob` revalidates the stage entry and rule, while `KanbanItems::StageFollowUpService` locks the item, cancels after any newer contact reply, and deduplicates with an item/rule/stage-entry key in message content attributes. Text and persisted funnel media use `Messages::MessageBuilder`; the shared Woot editor exposes ReplyBox Liquid variables and the message `Liquidable` concern resolves them against the target conversation. Approved templates are exposed and accepted only for configured `whatsapp_cloud` inboxes, retaining their inbox-specific `template_params` and the existing 24-hour window enforcement.
- Entry stages persist `ignore_group_conversations`; when enabled, `AutoCreateItemJob` does not create items for conversations whose `contact_inbox.source_id` ends in `@g.us`, without changing legacy condition-based stages.
- Automatic stage-template delivery is keyed by `kanban_item_id` and the stable stage-template ID in the outgoing message content attributes. The template editor enables the standard variable picker when `{{` is typed; `Liquidable` resolves values such as `{{contact.name}}` when creating the outgoing message. Existing templates default to one delivery per item; `resend_on_entry` opts a template into delivery on every qualifying stage entry, while manual quick messages do not consult this history.
- `notify_team` stage rules resolve selected team members and current item assignees at execution time, exclude the user who performed the move, deduplicate users, and create live per-user `kanban_stage_automation` notifications. A non-blocking Kanban banner displays one alert directly or groups multiple alerts into an expandable list with individual and bulk dismissal; email delivery is intentionally excluded.
- A pending checklist task with a due date schedules an internal alert for its assigned agent. The job verifies the task, recipient, and deadline are still current before delivery, locks the Kanban item to prevent duplicate concurrent alerts, and recreates a dismissed alert only after the funnel-configured interval while the task remains pending.
- Realtime synchronization with chat list and contact panel.
- `GET /kanban_items?contact_id=<id>` keeps the authoritative Kanban policy scope, resolves membership through all linked conversation display IDs, and filters open items before pagination only for funnels with `settings.contact_panel_contact_wide_items` enabled. The setting defaults to false; ContactPanel unions the expanded result with `currentChat.kanban_items` and refreshes it on Kanban events.
- The contact/conversation panel reuses the funnel agent candidates and persists assignment/removal through the Kanban item endpoints.
- The board opens a linked conversation from its channel icon without reinitializing board data. On mobile, item details separate business content from the profile/accordions and reuse status, move, and agent dialogs from ContactPanel.
- The contact/conversation panel Kanban block is hidden when the user has no visible items and no accessible funnels to create items.
- The main sidebar Kanban entry is hidden for non-admin users when they have no accessible active funnels.
- Funnel agent changes emit a realtime event to refresh the sidebar, funnels and visible items without a reload.
- A Kanban item can link multiple conversations: `conversation_display_id` keeps the primary conversation for compatibility and `item_details.conversation_ids` stores the full set; visibility, filters, chat-list realtime, and the ContactPanel Kanban block consider any linked conversation. The relationship picker is limited to the funnel inboxes and shows the channel icon/inbox name.
- `AutoCreateItemJob` guarantees one open item per contact and funnel: it serializes processing with the contact lock, reuses the oldest open item, and appends the new conversation when its inbox belongs to the funnel. Separate contacts are not inferred from their attributes, funnels are evaluated independently, and `won`/`lost` items allow a new opportunity.
- When a conversation opens from the Kanban drawer, `ConversationSidebar` passes `hidePreviousConversations` to `ContactPanel` to hide the previous-conversations accordion; the standard conversation panel keeps that accordion. The card deduplicates serialized conversations by `inbox.channel_type` and, when absent, `inbox_id`, to display one icon per channel and filters the selector to the clicked icon's channel.
- If a linked conversation is deleted, the Kanban item remains as history and the broken relationship is cleared.
- Consistent access scope across the API, cache, and realtime events: administrators can view every funnel and item; `agent` and the custom-role permission `kanban_view` receive only authorized resources.
- The current administrator can assign themselves to any item, individually or in bulk, and remove themselves individually, even when absent from `settings.agents` and the funnel inboxes; this exception does not allow assigning other ineligible users.
- The `kanban_view` custom-role permission can operate visible items; `kanban_manage` also creates funnels and is added to `settings.agents` on the funnel it creates. Only assigned funnels may have their content and structure edited; it cannot delete, set the default, or change `unassigned_visibility`.
- Items retain `created_by_id`, so the creator always keeps visibility. With a valid linked conversation, the current assignee can view it only when also selected on the funnel, and any manually assigned item agent can view it; a stale link is visible only to the administrator and creator.
- `unassigned_visibility` supports `everyone` (the legacy/default value) and `assigned_only`; `everyone` grants every funnel agent visibility of every funnel item, including assigned ones, while `assigned_only` preserves the authorized-agent scope.
- Any account member with Kanban access can be added to `settings.agents`, independently of `settings.inboxes`; a custom role requires `kanban_view` or `kanban_manage`. With configured inboxes, new manual item assignments still require access to at least one; moving an item automatically adds its assigned agents to the destination funnel without changing their inbox permissions.
- Global configuration is readable by `agent`, `kanban_view`, `kanban_manage`, and administrators; create, update, and delete require an administrator. Global automation endpoints are administrator-only; `kanban_manage` modifies assigned funnels only.

### 3.10 Integrations and extensibility

- Universal outbound API: `POST /api/v1/accounts/:account_id/outbound_messages` requires an `api_access_token` and inbox authorization; it accepts exactly one of `phone_number`, `email`, `contact_id`, or `source_id`, resolves or creates the contact/contact-inbox/conversation, and hands text, one attachment, or a WhatsApp template to `Messages::MessageBuilder` and `SendReplyJob`. For templates, it renders the synced approved BODY with its variables before persisting the message, so the dashboard and webhooks expose the sent content. Native WhatsApp channel templates (excluding Twilio) with media headers accept `header.media_file` as multipart data or a signed blob ID; the service stores it and generates `header.media_url` for the provider. `Idempotency-Key` is optional: when omitted, every request is a new send; when provided, an identical retry returns the original response and a different payload returns `409`. HTTP `202` confirms local queueing, not provider delivery.
- Webhooks with enriched payload and global HMAC-SHA256 secret.
- `inbox_updated` webhook event for inbox state changes and disconnects.
- Dashboard Apps for embedded iFrame extensions by context; authenticated account users can read them, while only administrators can create, update, or delete them.
- Dashboard Scripts (Super Admin) for global customization without core edits.
- Platform Apps for high-level external integrations via API.
- Business integrations: Slack, Linear, Shopify, WooCommerce, Notion, CRM, Google Calendar, Tasks.
- Tasks is guarded by the `activities` account feature and an enabled account-scoped `Integrations::Hook`; the same pair controls integration visibility, API access, route access, and the sidebar entry.
- `/activities` persists its calendar/list choice and operational criteria in the route query. Without `status` —or with an invalid value—it starts at `all` and sends no filter; valid explicit values are preserved. Calendar requests remain unpaginated; list requests use server-side title search, ordering, grouping order, and opt-in `page`/`per_page` metadata.
- Calendar requests use explicit `overlaps_from`/`overlaps_to` interval intersection. The client projects a multi-day task onto every visible intersected date rather than only its start date.
- Task authorization uses three custom-role permissions: `task_manage` creates tasks and manages only records assigned to or created by the user, `task_view_all` adds account-wide read-only access, and `task_reports_view` grants task reports and their read-only drilldowns. Standard agents implicitly receive the own/assigned scope; administrators retain full access and exclusive deletion.
- `AccountTask` is the source of truth for type, priority, assignee, participants, guests, contact/conversation, and unique Kanban/`CalendarEvent` links; it persists pending/in-progress/completed/cancelled and derives overdue from `ends_at`; every ID is resolved within the current account.
- `ActivityType#color` stores one of the 22 visual palette identifiers shared with Google Calendar. A migration converts the six legacy colors and the UI reuses one class map; status adds decoration without overriding the task type background.
- `outcome_summary` records the closure result and is required by both UI and model for `completed` and `cancelled`; reopening preserves it as editable history.
- `AccountTasks::TriggerDueNotificationsJob` runs every minute and creates one `account_task_due` notification at `ends_at`, exclusively for `assignee_id` and only while the task remains pending/in progress and Tasks is available. The assignee can mark it as seen or snooze it through `snoozed_until`; the global reopener republishes it automatically. Rescheduling, reassignment, or closure removes the previous alert so it can be recalculated.
- Recurrence roots persist type, interval, weekdays, and a date/count limit. `AccountTasks::RecurrenceService` materializes up to 100 independent child tasks, inherits assignee/context/participants/Kanban/Google, updates open occurrences, and preserves closed ones.
- Optional task and `CalendarEvent` projection references use `ON DELETE SET NULL`. Tasks snapshot creator, assignee, contact, conversation, and Kanban context; relation deletion clears live IDs, resynchronizes Google, and keeps readable historical labels. Contact cascading has one owner per level (`ContactInbox` → conversation → message), preventing duplicate jobs.
- Destroying an `AccountUser` synchronously clears that account's assignments, participation, and due alerts, then resynchronizes affected Google events after commit to remove the former attendee. Destroying a task preserves its managed Kanban item, removes task ownership metadata, and retries a failed Google cancellation.
- `/account_tasks` transactionally coordinates the task and one customer-linked or free Kanban item. Editing updates or moves the same item; detaching never deletes it.
- The UI loads and displays Kanban only when the account has `kanban_board`; the API ignores new Kanban links while the feature is disabled and preserves any existing hidden link when the task is edited.
- Selecting a conversation loads its visible Kanban items. Linking an existing item never mutates it and the item may be shared by multiple tasks; “Create new” keeps the managed funnel/stage workflow.
- ReplyBox exposes quick creation only when the Tasks feature and hook are enabled. It loads types, agents, funnels, and Google capabilities on demand, then opens `TaskDialog` with the current contact and conversation; the dialog automatically resolves their related Kanban items.
- ContactPanel renders a dedicated Tasks accordion using the calendar visual pattern and queries `/account_tasks?contact_id=...&status=open`; each card shows the linked conversation's stable `display_id`, while the filter includes persisted pending/in-progress states so derived overdue work and tracking survive conversation changes for the contact.
- `/activities` uses a `CalendarEvent` projection for optional outbound synchronization with exact start/end and deduplicated attendees; provider failures remain visible without rolling back valid local work.
- On mobile, `/activities` reorganizes filters and navigation while preserving the desktop month canvas with horizontal scrolling so its cells are not compressed. `TaskDialog` bounds its scrollable area with `dvh`, stacks its header, and keeps the footer outside scrolling content.
- `TaskDialog` opens existing records in read mode, enters editing explicitly, and requests `outcome_summary` in a secondary dialog for complete/cancel actions. Deletion requires confirmation, is shown only to administrators, and `AccountTaskPolicy#destroy?` enforces the same restriction in the API.
- Kanban item details show the operational Tasks tab only when the feature and hook are enabled; it queries `/account_tasks?kanban_item_id=...`, keeps item history in a separate tab, and prefills the contact, conversation, and item when creating.
- `AccountTasks::KanbanHistoryService` appends `account_task_changed` events to the item's bounded JSONB history inside the local transaction; it records lifecycle and link changes without duplicating them as conversation messages.
- The complete account-scoped Tasks and Task Types CRUD contract is maintained in modular `swagger/` sources, the resolved Swagger/public audience documents, `docs/openapi.yml`, and the generated Postman collection. It documents filters, `q`, interval intersection, safe sort allowlists, opt-in pagination metadata, rich relationships, recurrence, Kanban/Google conditions, permissions, and validation responses.
- Reports adds a route visible only while the feature and hook are active plus `GET /account_tasks/reports?since=&until=`, authorized for administrators and `task_reports_view` only. `AccountTasks::ReportsService` filters by `COALESCE(ends_at, starts_at)`, builds the daily completed series, and aggregates total, pending, in-progress, completed, overdue, and cancelled tasks by responsible agent and type. Each task belongs to exactly one status category. Charts and rows open a drawer that queries `GET /account_tasks` by effective scheduled date, responsible agent, or type; it then reuses `TaskDialog` in read mode. Elapsed-time metrics remain hidden because tasks do not yet persist a completion timestamp.
- Google controls appear only when the feature is enabled, the integration is connected, the outbound connection is active, the `calendar` module is enabled, and a writable calendar exists. Destination and external-guest fields appear only after opting into synchronization.
- Google Calendar uses account-scoped OAuth/config APIs, selected `CalendarConnection`, internal `CalendarEvent`, and provider mapping through `ExternalCalendarEvent`; `settings.import_all_calendars` controls inbound scope independently from the concrete outbound `calendar_id`.
- The operational calendar route `/app/accounts/:accountId/calendar` reads local `calendar_events` for day, week, month, list, create, edit, cancel, sync on save, and manual fallback sync. `CalendarSync::PollConnectionsJob` runs every five minutes and imports Google changes with per-calendar `last_polled_at` stored under `CalendarConnection.settings`; deleted Google events remove their mapped local projections, and recurring instances are expanded within a rolling one-year lookback and five-year lookahead.
- Calendar navigation, the operational route, composer action, and conversation-panel section require the account feature and a connected `GoogleCalendarIntegration` with `CalendarConnection#calendar_id`; custom-role users additionally need `calendar_manage`, while integration configuration remains administrator-only.
- The month view limits each cell to two visible events to reserve space for a `+N more` control; right-click opens event actions and each row still opens the editor. Color is stored in `metadata.color_id`; permanent deletion requires an administrator and removes a linked Google event before deleting its local record.
- `calendar_events` responses include lightweight contact, conversation, and Kanban item summaries for searchable relation selectors; edit payloads send `null` to unlink relations.
- The calendar relation selector searches Kanban items across the account instead of inheriting the currently selected funnel, and accepts item IDs (including `#ID` format).
- Checklist tasks have independent Google Calendar sync settings and destination calendars; each synchronized task is stored as its own event linked by `checklist_item_id`.
- The assigned checklist agent is added as a Google attendee and receives the platform reminder; completing or deleting the task cancels its event and pending reminder.
- The conversation reply composer loads the account connection and writable calendars before opening the shared `CalendarEventDialog`; the explicit “Create and send” action formats its `saved` result with localized event fields and sends it once through `createPendingMessageAndSend`, using `metadata.google_meet_url` without retrying event creation if messaging fails.
- The conversation contact panel filters `calendar_events` by `conversation_display_id`, recalculates Start-to-End progress every 30 seconds for a pulsing green (<50%), yellow (50–90%), or red (≥90%) dot, fades expired entries, reuses `CalendarEventDialog`, and consumes saved-event updates.
- `GoogleCalendar::EventMapperService` maps event metadata into Google fields for location, attendees, reminders, simple recurrence, availability, visibility, guest permissions, and Google Meet.
- The responsive event editor uses icon-led rows, an IANA time-zone selector, and removable guest chips; the sidebar places installation-branded context below guest permissions with floating searches and the inbox channel icon on every conversation result; it persists the writable destination and returned Meet URL.
- Google Calendar supports manual inbound import through `google_calendar_integration/import_events` and legacy Kanban backfill through `google_calendar_integration/backfill_kanban`; Flow Builder triggers remain deferred.
- Notification and PWA assets generated dynamically from `NOTIFICATION_ICON` (default `/favicon-badge-16x16.png`), falling back to `LOGO_THUMBNAIL`, with configurable background and cache invalidation by asset, color, and blob timestamp; the favicon keeps `LOGO_THUMBNAIL`, switches to `NOTIFICATION_ICON` for messages received while hidden or unfocused, and restores on return.

### 3.11 Signup and onboarding

- Guided account-profile completion through the dedicated admin endpoint `/api/v1/accounts/:account_id/onboarding`.
- Website persistence as a fully qualified URL for downstream consumers such as Help Center and brand enrichment.
- Separation between general account updates and completion of the `account_details` step.
- The Instagram OAuth callback preserves the signed `return_to` hint to resume inbox setup when authorization starts from onboarding.

### 3.12 Branded email layouts

- The `branded_email_templates` account feature flag enables account-level fallback and Email-inbox override layouts.
- `EmailTemplate` scopes layouts by installation, account, and inbox, validates Liquid syntax and the `content_for_layout` slot, and limits bodies to 256 KiB (262,144 characters).
- The account layout endpoint and Email inbox update endpoint are administrator-only; the OpenAPI schemas expose the same limit.

### 3.13 Security and compliance

- 2FA/MFA, SAML/SSO, custom roles, and audit logs. Super Admin's deletion-evidence report queries retained `audits` rows only: Inbox destruction uses its Account association, while Conversation and Contact destruction use the `account_id` snapshot in `audited_changes`; it never joins deleted live records or infers Message deletions.
- User session records support an agent-editable `custom_name` label; IP metadata remains internal and is not exposed in dashboard session payloads.
- Web authentication sends a validated, persistent 128-bit browser-profile ID as the token client ID. Tabs reuse one logical `UserSession`, reauthentication rotates the same slot, and successful sign-out removes both token and row. New profiles receive the blocking picker only at `MAX_USER_SESSIONS`; mobile clients retain generated IDs and silent eviction.
- Suspended-account dashboard state keeps the support widget visible and exposes an explicit support action. On Cloud, the route guard and suspended screen allow only administrators to access billing so they can restore the account; agents remain on the suspended screen. Super Admin validates a category and a 256-character reason, appends events under `accounts.internal_attributes.suspensions`, retains unrelated internal metadata, and permits corrections to the latest event without changing its timestamp.
- Mega license protection in deployment flows.
- Release observability for version-level traceability.

## 4. Operations and validation

### API parity and Postman collection

Supported routes under `/api`, `/platform/api`, and `/public/api` are compared with OpenAPI 3.1 by normalized method and path. Validation detects missing, stale, or duplicate operations; it does not claim test coverage for every response field. `bundle exec rake swagger:build` regenerates Swagger and `swagger/postman_collection.json` in an import-ready structure: Application API resources are top-level folders inheriting `api_access_token`, while Mega Platform APIs and Mega Public APIs retain dedicated folders and authentication. Collection variables centralize `host`, `api_version`, `account_id`, credentials, and path identifiers. Multimedia messages include separate examples for selecting a file with `multipart/form-data` or using a JSON `signed_blob_id`. `Idempotency-Key` is optional and disabled; it can be enabled with `{{$guid}}` or a fixed key to verify retries.

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
