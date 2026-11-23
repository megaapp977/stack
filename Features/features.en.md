# 🚀 MEGA - Omnichannel Communication Platform

## Mega Assistant

Administrators can ask which contacts sent the most messages in a recent period. Mega Assistant counts incoming public messages across each contact's conversations and summarizes subjects observed in a clearly labeled sample of recent text messages. Tool discovery finds actions by meaning and shows the parameters needed to query them or propose changes.

When reviewing inboxes, Mega Assistant distinguishes channels without a health endpoint from a WhatsApp Cloud connection whose credential needs reauthorization. It presents these as diagnostics and avoids repeating the same unchanged check.

Before proposing a change, Mega Assistant checks that the details are complete and valid. If something is missing, it fixes it or asks in the same reply, so no confirmation card appears that would fail afterwards. It also doesn't repeat lookups it already made or duplicate a pending proposal.

Mega Assistant answers the most common requests in a single lookup: conversations waiting for a reply, a contact's full profile with their conversations and latest messages, a period against the previous one by channel, and Captain's state with its assistants, inboxes and scenarios. For requests with several parts it first records a plan and accounts for each item. While it works it shows what it is reading (inbox, contact, status, period), computes “today” and “last week” in the browser's time zone and replies in the language of your latest message. Several proposals from one reply can be confirmed or cancelled together. Plans and accounts can pick a complex-tasks model, which handles multi-part requests, diagnoses and comparison reports and takes over if the main model fails.

When a change applies to many conversations at once (resolve, assign or label them), confirming it applies it one conversation at a time and the card shows how many changed, how many already had it and which ones could not be changed and why, with a link to each conversation. You can keep chatting while it runs, and the assistant reports the outcome when it finishes.

For requests over many records (every conversation of a period, the messages that mention an order, every contact with a label), Mega Assistant selects all of them on the server, up to 5,000, gives the exact total and keeps the selection for the next steps: the conversations of those messages, the contacts of those conversations, follow-up questions about the same set, or one change for all of them that you confirm once.

To judge what conversations say (which customers asked for a refund, which ones are most urgent, how they feel), Mega Assistant reviews the selected conversations one by one in the background, the newest 100 per request, and a card shows how far it got. When it finishes, it answers in the chat with what it found, how many it read and how many are left, and offers to continue with the next 100. The matched conversations can then be used for the next step, such as listing their contacts or labeling them all. Each reviewed conversation is charged at the review model's price in AI Actions; the review stops if the account runs out of them.

Mega Assistant knows what you are looking at. With a conversation or contact open, “summarize this”, “transfer this conversation to Sales” or “add a note to this contact” work without typing an id; with conversations selected in the list, “resolve these” acts on exactly that selection. Only references are shared (the record, the list filters and the selected conversations, never the page text), and every one is checked against your permissions before the assistant sees it. A line above the message box shows what the assistant will use, with a button to ignore it. Confirmation cards name the record they change, mark when it came from your screen, and warn you if you are no longer viewing it; a change to a record that was deleted or that you lost access to cannot be confirmed. It also knows the Kanban board and task, the flow open in the Flow Builder, the inbox whose settings you are editing, the contacts you selected in the list and the record of single-record pages: the Captain assistant, the chat room, the company, the Help Center portal (with its locale), the report of a campaign, an agent, an inbox, a team or a label, the dashboard app, the capacity policy, the monitor and the data import. When you ask it to schedule something, it tells apart a scheduled message, a campaign, a task, a calendar event or snoozing a conversation by what has to happen at that time, and asks when it is not clear.

It also knows which form is open over the page even though the address does not change: creating or editing a canned response, a custom attribute, a bot, an automation, a campaign or a scheduled message, and in Captain a new assistant, a FAQ, a document, a scenario, a rule, a tool or an MCP server. “Fill in this form” or “change this campaign” mean what you have open, and once you move to another page it stops using it. It can also change what it could only read before: an inbox's satisfaction survey (and create its WhatsApp template), message templates, dashboard apps, Captain monitors, Kanban offers and your own profile (name, display name and signature; email, password and two-factor authentication are changed on the profile page). Like any change, it proposes it first and you confirm.

When you confirm a change, Mega Assistant checks again that you may still make it: if the feature was turned off or you no longer have the role the change needs, it is not applied. If someone changed the values the card showed as current since it was proposed, it does not overwrite them either: it tells you what changed and proposes it again only if you still want it.

After applying a confirmed change, Mega Assistant reads the record again and checks that it holds the values it sent. The card says “Change applied and checked on the record”, or warns you when the record shows other values, and the assistant tells you in the chat without claiming more than it checked.

Before explaining how to set something up or offering to do it, Mega Assistant checks in your account whether that feature is enabled, whether your role may change it and whether a tool can do it from the chat. If it is off or needs another role, it tells you so and who can enable it, without promising to configure it; if there is no tool, it guides you step by step on its screen. “What can you set up for me?” is answered with your account's real list of modules and their status.

You can tell it what you want to achieve in your own words, for example “I want to automate WhatsApp support, answer frequent questions, spot sales opportunities and hand off to a person when needed”. Mega Assistant splits it into needs, checks which modules you have and what is already set up so it can reuse it, recommends a solution and explains why, builds the plan and asks only for the details still missing. Then it sets it up step by step, with your confirmation, checking each result and going on to the next step.

When you ask “how does … work?”, Mega Assistant answers from each module's functional documentation, shipped with the app: what it is, how it works, its requirements, limits, how to set it up and examples, with the date it was checked and the product documentation section it comes from. It reads only the module you are talking about, and when a module has no documentation it says so instead of inventing menus or options.

When a question turns into a setup of several steps (“go ahead, let's configure it”), Mega Assistant notes in the chat the goal, the decisions you took and the steps left. In later messages, when you come back to the chat or in a voice call, it carries on from there with your decisions and only asks for what is missing; if you change your mind it updates the decision, and it closes the goal when the setup is done or dropped. In Captain it notes each phase of the setup and resumes at the first pending one. It is the chat's memory, not a permission: every change is still proposed and confirmed.

If you come back to a setup you left days ago, Mega Assistant first checks that you still want it and reads the current configuration again before going on.

In a voice call, when the reply shows cards, tables or charts, the voice also gets their values: it says the figures that answer what you asked (not just that it is on screen) and answers follow-up questions such as “and the resolutions?” from that same data.

In the Flow Builder, Mega Assistant changes an existing flow block by block: it adds, changes or removes only the blocks and connections you ask for and leaves the rest exactly as it was. Before proposing it, it checks that the flow is still valid, and if someone edited it meanwhile, confirming the change does not overwrite that edit. It never publishes on its own: publishing needs you to ask for it and confirm it.

To measure how the assistant works in each account, every reply records how long it took, how many tools it used, which failed or were refused for permissions, the modules asked about that were off, forbidden or undocumented, and how it ended. A per-account report combines that with the model cost and the outcome of confirmed changes (applied, refused on confirmation, and checked on the record).

Administrators see it on the assistant page, in the history's Metrics tab (the chart icon), for the last 7, 30 or 90 days: replies, failed ones, ones without a source (long answers that read no data or documentation, an estimate), average and slowest time, cost, changes applied, not applied, checked and with other values, and the tools and modules that fail or are refused most.

Confirmation cards show what each change does in plain terms (who a conversation goes to, which labels are added or removed, the task or flow it creates or changes) and let you adjust the team, agent or labels before confirming. Every adjustment, yours or the assistant's when you say “actually, Support”, becomes a new revision of the same card, and only the latest one can be confirmed. Tables, charts and other results appear as soon as they are ready, can be updated in place in later replies, and open in a larger view. Forms and suggested steps send exactly what you chose, checked against the form the assistant showed.

Voice: the composer microphone records what you say, transcribes it and sends it as your message. The waves button opens a realtime voice conversation: an animated orb shows whether the assistant is listening, thinking or speaking, and you can keep typing, mute yourself or hang up with the X. What you ask by voice goes through the same assistant as the chat, with the same tools, cards and proposals, and lands in the thread like a typed message; the assistant reads you a short summary. A spoken “yes” to a proposal starts a 5-second countdown on its card that you can cancel by voice or with a click; deletions, merges and bulk changes always need the click. Voice is charged in 5-minute blocks of AI Actions and each request counts as one message. In Settings → Captain you pick the voice (Marin and Cedar recommended), the speed and, if you have one, your OpenAI custom voice. Refreshing the page during a call lets the next call take over the previous one. During a call you can change screens: the call stays in the pet or, when it is closed, in a small control that takes the pet's place, with the pet inside it and a colored ring (green while it listens or talks, amber while it works, waits for your confirmation or the microphone is muted), that says "Call with …" and what it is doing, with mute, "Open chat" and hang up; dragging it by the pet or the text moves the pet with it; it only ends when you end it. The voice knows which screen you are on and remembers what was already said in the chat, also in a new call. It knows the account's names (your recent contacts, inboxes, teams, agents and labels) so it writes them as stored even when they sound alike, and when a spoken name is not found, the assistant tries how the transcription heard it and its parts before saying it does not exist. The assistant can open any dashboard screen to guide you (for example an inbox's settings, a contact or a Captain assistant), by chat or by voice, only among the pages you are allowed to see and that the account has enabled. When a request takes a while, the voice tells you what it is doing (for example, that it is looking up the contact) instead of going silent, never talking over you. While it works, a “thanks” gets a brief reply without stopping the task, “wait” keeps it quiet, a correction (“only WhatsApp ones”) runs as soon as it finishes and “cancel” stops the search on the server. Each user can give the assistant their own name (in their profile or by asking: “from now on I want to call you Rio”, saved once confirmed), and an administrator can name it for the whole account in Settings → Captain; the same name is used on screen, in the chat and by voice. When the call connects, the assistant greets once with its name. What you say in the call and what the voice answers are written into the call's chat, so the chat, the text assistant and the next call remember them (a spoken request stays as its request message; the greeting and progress updates are not written). If you confirm or cancel a proposal with a click during the call, the voice hears it and tells you the real result. While a call runs, the panel always shows its chat: the voice button takes you to that chat instead of creating an empty one. If you type a message or attach a file in the chat during the call, it is as if you had said it: the voice answers out loud, as the same assistant as the chat (type "hi" and it says "Hi! How are you?"), reads the file when it needs to, and its answer is written into the chat; what you say is kept in your own words and what you hear is what stays written, in short sentences; the voice knows which screen you are on as you move around the dashboard; when it picks a chat up again, the call opens naming what you were talking about.

Assistant preferences: in your profile you choose, only for the account you are in, the reply language (the one of your message, or always Spanish, English or Portuguese), the style (balanced, brief or detailed), how lists of records are shown (automatic, table or cards) and whether a voice call starts with a spoken greeting. They are optional and apply to the chat and the voice; they are style hints, never permissions: they do not change what the assistant can see or do. An administrator can write the call greeting in Settings → Captain, in the voice section: plain text of up to 200 characters, where {name} is replaced by the assistant's name.

Privacy and retention: your preferences and the name you gave the assistant are stored on your user, separately per account; only what you changed is stored, they are never learned from your conversations, and “Delete my preferences” removes them (the name, by leaving it empty). As part of your user data, other members of the account can read them through the agents API. From a voice call we store the session record (start, end, model and blocks charged), the requests the voice passed to the assistant and its written replies, and the text of what you said and what the voice answered, as thread messages; you and the account administrators see them, and deleting the thread deletes them. The audio is not stored. The audio goes straight from your browser to OpenAI, and its retention follows OpenAI's API data policy.

Administrators see next to each reply what it cost in model calls, including any review it started. Mega Assistant also knows what each conversation status and priority means and judges urgency or topic by reading the conversations, not from the priority field alone.

For requests that mix questions and changes, it keeps room to propose the changes even after using all its lookups, and it accounts for every item asked: answered, proposed, or pending and why. If a lookup fails on the server, it continues with the rest instead of ending the reply.

### Current behavior (September 2026)

This block takes precedence over older paragraphs in this section.

- **Who can use it:** account administrators and members whose custom role includes “Use the AI assistant”. Administrators can read their team’s assistant chats (read-only) from the Team tab of the full page; chats are no longer private to their owner.
- **History:** search, Pinned, Today, Previous 7 days and Older, shared by the full page and the floating panel. An amber dot marks chats with an action waiting for confirmation.
- **Actions:** each proposal shows a card with its title, status, recipient, a link to the conversation and a preview of the text and files that will be sent, or the fields that will change with their current and new values. Text messages can be sent or kept as a draft in the reply box.
- **Progress and errors:** while answering, the assistant lists the tools it is using. Failed replies say why (no AI model available, AI service not responding).
- **Rich replies:** when you ask for a report, table, chart or comparison, the assistant answers with visual blocks below its text: text, markdown, table (sortable, CSV export), metrics, card, chart (bar, line, area, pie, doughnut), timeline, contact, conversation, kanban, form, suggested actions and HTML report. An executive report is built in the chat with blocks (metrics, chart, findings, table) and the assistant offers the PDF version as a suggested action; the HTML report is only generated when you ask for it, opens by itself in the full-page canvas, and can be downloaded or saved as PDF through the browser's print dialog. Forms and suggested actions answer in the same chat, so the assistant keeps the context. In the pet, blocks adapt to the width: metrics in 2×2, tables show 3 columns and expand, kanban scrolls sideways. Reports and PDF, HTML, Markdown and text files open in a canvas: on the full page it is a column to the right of the chat (you can keep chatting), and in the pet it opens over the screen, with preview or code view, download and print.
- **Plans and AI Actions:** each completed reply is charged the AI Actions of the model that answered (the automatic reply after a confirmation is not). With no AI Actions left, messages are refused and administrators get a link to buy a package; administrators see the remaining balance. Plans can include the assistant for questions only or with actions. Administrators of accounts without the assistant see what it offers and a link to the plans.

The full-page sidebar separates Pinned from Recents: each section collapses independently, and pinned chats never repeat in Recents. Pinned is shown only when it contains chats; both groups retain newest-activity-first ordering.

Each full-page history row offers Rename, Pin/Unpin and Delete through its three-dot menu, available on hover, keyboard focus and touch. Titles (1–100 trimmed characters) and pins persist. Pinned chats come first, then recent activity descending within each group, with at most 50 chats returned. Only the current user's private assistant chats in the current account can be managed, and the Mega Assistant feature must be enabled. Deletion requires confirmation and permanently removes the chat, messages, actions and attachments. Chats generating a response or executing an action cannot be deleted until finished. Deleting the selected chat starts a new chat and clears its draft and files; managing another chat preserves the current chat and draft.

The assistant history sidebar starts with New chat, followed by a collapsible Recents section with pinned chats first and activity descending within each group. Opening or renaming an older conversation does not change its activity order; new messages update its position.

The assistant’s name follows your Custom Branding setting: Brand Name + “Assistant”, for example “Acme Assistant”. Your brand appears consistently in the sidebar, chat and keyboard help. If no name is configured, “Mega Assistant” is used.

The pet displays the Mega Assistant Pet image configured in Custom Branding, preserving its proportions and drag controls. It defaults to the bundled Mega Assistant pet image and is independent from the Logo Thumbnail.

The floating Copilot launcher is hidden on the full Mega Assistant page and remains available elsewhere in the dashboard.

The keyboard-help entry is only shown when the current account has the Mega Assistant feature enabled, matching the sidebar. The shortcut is inert when the feature is disabled; opening also requires assistant availability.

Alt + Shift + M toggles the floating assistant: when its chat is open, it closes the chat and hides the pet; otherwise it restores and opens it. In the full page it focuses the existing editor without leaving the conversation.

Alt + Shift + M recalls a hidden pet and opens its chat on dashboard pages where the assistant is available. On the assistant page it focuses the existing editor. The close control has a larger, high-contrast X; the shortcut is listed in keyboard help.

The pet can be hidden with its own X and enabled again from the assistant page header. The floating chat’s expand button opens that page with the same conversation, draft and selected attachments. Visibility is saved in this browser; chat transfer stays in memory and does not survive a reload.

When starting an empty chat, the page centers the welcome and composer. The shared replybox uses the conversation editor’s solid surface and border, with subtle elevation and a visible focus state; once messages appear, it stays at the bottom.

The primary sidebar includes a full assistant page with history and a centered conversation. It shares the rounded attachment composer with the floating panel; the pet is hidden while this page is open.

Mega Assistant starts with named contact, conversation, count, inbox and Captain read tools. It can discover any other eligible named account tool in explicit pages, keeping at most 40 named tools active at once. Configuration questions require reading the relevant APIs, not merely listing available routes; an empty or partial search is reported as such, not as proof that a record or capability does not exist. Captain is identified as the platform AI module; read outcomes and proposed changes are retained in the private conversation action history.

Within each private chat, Mega Assistant reuses eligible tools and stable prompt context across replies so supported providers can cache repeated input and reduce response cost.

When a reply proposes an action, the assistant's message appears first; the confirmation card appears beneath it once the message finishes displaying.

The conversation stays beside the pet while it moves, flips to available space near screen edges, and keeps both within the viewport. A compact header exposes history and new conversation controls; suggestions populate the composer without sending automatically.

Mega Assistant is a private account assistant with a movable, resizable keyboard-accessible pet and a Copilot-based conversation panel. It discovers account operations, answers using authenticated API results, and proposes changes for explicit confirmation. Counts use API totals rather than page sizes. No MCP server, token or public API entitlement is required.

Providers independently opt into Captain and Mega Assistant. Super Admin account model cards select chat, image/PDF and audio transcription routes per account. Upload up to five images, PDFs, text documents or audio files (20 MB each) with the + button, by dragging and dropping them onto the composer, or by pasting them (for example, a screenshot). Files and histories remain private to their owner. Confirmed actions display their real outcome and cannot be executed twice. If a server restarts while the assistant is answering, the reply resumes on its own within a few minutes instead of hanging. Dictation and realtime voice are included (see Voice); telephony is not.

## Your Command Center for the Future of Customer Service

AI provider cards summarize model count, verified capabilities and credit warnings. Models and tests opens a dialog with each model's assigned uses, check status and saved errors, without expanding the grid. Test, edit and protected deletion actions remain available.

Reasoning and tools work together on every provider: each model gets its reasoning in the form its API accepts (a level, a thinking budget, or nothing when it does not reason), and OpenAI models are called through the Responses API. OpenAI-compatible providers take a preset: OpenRouter, xAI, DeepSeek, Mistral, Perplexity, Ollama and GPUStack run on their own integration, while Groq, Together, Fireworks, DeepInfra, Cerebras, SambaNova, Qwen, Z.ai, vLLM, LM Studio or any custom gateway connect as generic gateways whose API (Responses or Chat Completions) the capability test detects per model.

Provider forms are centered. A visible bulk-add button opens a modal to paste model names and select capabilities; Cancel or Escape closes it without adding rows.

Add/edit provider pages use a two-column connection section and a compact model table. Bulk entry accepts newline- or comma-separated names and shared capabilities; existing names are merged without duplicating rows.

Legacy catalog selections remain available for their original features after editing an imported provider. New provider-qualified selections still require assigned, verified capabilities. Legacy PDF/audio clients resolve current native OpenAI credentials, falling back to installation settings when no active native provider exists. Audio prefers the account OpenAI integration; Captain fallback requires its feature and available quota. Call recordings retain their specialized path.

A one-time upgrade repair restores missing `whisper-1`, `gpt-4o-mini-transcribe` and `text-embedding-3-small` entries on the native provider with slug `openai`. It preserves credentials, custom models, existing assignments, test results and account selections. Restored entries are configured, not automatically verified; provider-qualified selection still requires testing. The repair can restore a previously removed base entry, but does not re-add it on ordinary saves. Models marked coming soon are not added.

Models OpenAI is retiring (the GPT-4.1 series, `gpt-4o`, `whisper-1`, `gpt-4o-mini-transcribe` and `gpt-4o-transcribe`) are replaced by GPT-6 Luna for text and GPT Transcribe for audio. Captain features default to Luna (Copilot uses GPT-5.1) and run it without reasoning unless AI Providers sets another effort for the model. A migration moves the choices saved on accounts, plans and installation settings to Luna or GPT Transcribe; a provider choice only moves to the same provider when that provider already validated the replacement, and Mega Assistant keeps its choice until it is validated. OpenAI providers get both models priced (GPT Transcribe US$0.0045 per minute) and unvalidated: test them in AI Providers. Diarized call transcription stays on `gpt-4o-transcribe-diarize` because OpenAI has not published a replacement. Captain and AI model lists also offer GPT-6 Sol and GPT-6.1 Terra.

FAQ regeneration preserves existing responses on errors or empty results. It replaces only unedited responses when valid results are available, in a transaction that rolls back replacement if any insertion fails. Legacy PDF generation checks the remote file and, only on a 404, uploads the retained original again using the same credentials as generation. Permission, credit, or connection errors do not trigger another upload; if the original is missing, previous knowledge is retained.

Provider forms list each model once, with Chat, PDF, Audio and Embeddings checkboxes. Tests run only for selected capabilities. Existing selections and verified results are preserved; models without a selected capability remain visible with a prompt to select one. Changing credentials or the endpoint requires revalidation.

Capability checks use a valid one-page PDF and a one-second PCM WAV. The silent audio sample checks file acceptance, not transcription accuracy.

Provider model tests show provider-reported insufficient credit or exhausted quota on the provider card. These results do not establish model incompatibility; top up or review billing and retry.

Twilio Voice call recordings can optionally be transcribed, displayed with the recording, and found in conversation search.

**Version:** Enterprise
**Based on:** MEGA Platform and Exclusive MEGA Features
**Last Updated:** September 1, 2026

---

### Verified APIs ready for Postman

Swagger/OpenAPI 3.1 maintains automated parity with supported routes and generates a Postman collection separated by account token, platform app token, and public routes.

## 📋 Table of Contents

1. [Communication Channels](#-communication-channels)
2. [Conversation Management](#-conversation-management)
3. [Internal Team Communication](#-internal-team-communication)
4. [Automation & AI](#-automation--ai)
5. [CRM & Contact Management](#-crm--contact-management)
6. [Mass Campaigns](#-mass-campaigns)
7. [Help Center](#-help-center)
8. [Reports & Analytics](#-reports--analytics)
9. [Team Management](#-team-management)
10. [Integrations](#-integrations)
11. [Enterprise Features](#-enterprise-features)
12. [Mega Exclusive Features](#-mega-exclusive-features)

---

## 📱 Communication Channels

- **Clear inbox identification** *(Mega)* - Lists and the sidebar show each inbox name alongside its public identifier (phone number, email, or URL). Facebook page IDs and X profile IDs remain available for provider operations but are not shown. Inbox search also accepts displayed identifiers.
- **Preserved social identity** *(Mega)* - Facebook, Instagram, and TikTok inboxes retain their provider page or username without overwriting a custom inbox name when the channel reconnects.

### WhatsApp Business

- **Brazilian contact deduplication** *(Mega)* - Cloud, coexistence, Twilio WhatsApp and Cloud calls reuse existing mobile contacts when the provider omits the ninth digit; exact matches take priority and landlines do not generate mobile alternatives.

Connect with your customers through the world's most popular messaging channel.

- **WhatsApp Cloud API** - Official Meta integration with all enterprise features
- **WhatsApp Cloud registration recovery** *(Mega)* - Complete the connection from the same inbox with separate steps for SMS or voice ownership verification and two-step PIN registration. If no PIN is stored, one is requested; a forgotten PIN is recovered in Meta. Connection status reflects the phone status reported by Meta.
- **Premium Cloud calling connectivity** *(Mega)* - Companies with restrictive networks can use managed STUN/TURN relay connectivity for WhatsApp Cloud WebRTC calls
- **Guided manual WhatsApp setup** *(Mega)* - Administrators can prepare their own Meta app, validate a production number, WABA ID, and permanent token before creating a Cloud inbox; the flow displays webhook/subscription status and permits a webhook retry without leaving setup
- **WhatsApp Business App coexistence signup** *(Mega)* - Embedded signup supports onboarding a WhatsApp Business App number, including coexistence completions that do not provide a phone-number ID, while MEGA configures the required connection and webhooks
- **Mega Hub for WhatsApp** *(Mega)* - Optional connection with shared apps from Super Admin, using dedicated Hub credentials, relayed webhooks, forward-aware webhook health, and no manual callback/token setup
- **WhatsApp Evolution** *(Mega)* - Direct connection without official API, ideal for personal accounts
- **WhatsApp WAHA** *(Mega)* - Alternative provider with full multimedia message support
- **WhatsApp Uazapi** *(Mega)* - Low-cost solution for multiple lines
- **Connection health alerts** *(Mega)* - Token and session issues appear in inbox lists, the primary sidebar, and inbox settings with a shortcut to session configuration
- **Phone health resilience** *(Mega)* - Cloud API phone health remains available when linked business-account details cannot be refreshed
- **WhatsApp business profile in Account Health** *(Mega)* - Account Health shows the read-only customer-facing business profile, clearer display-name review guidance, and the portfolio-wide messaging limit
- **Manual WhatsApp reconnection** *(Mega)* - Eligible embedded-signup inboxes can be reconnected to your own Meta app through a guided flow that preserves the inbox and its customer-service history
- **Embedded-signup reconfiguration** *(Mega)* - Administrators can refresh the credentials and WhatsApp Business configuration of an existing Cloud inbox connected through embedded signup without enabling an account feature; the creation feature remains required only for new inboxes
- **Multi-server architecture** *(Mega)* - Configure multiple servers per provider with automatic credential resolution
- **Per-server capacity** *(Mega)* - Define limits by server to distribute operational load
- **BSUID support** *(Mega)* - Reliable contact identification and delivery even when traditional `wa_id` is missing
- **More reliable WhatsApp Cloud calls and attachments** - Attachments are uploaded to Meta before sending (fewer download rate-limit failures), calls also reach contacts that only have a BSUID, Messenger receives Get Started buttons and the HUMAN_AGENT tag is used only when it applies
- **Provider-aware unsupported messages** *(Mega)* - Distinguishes unsupported content from coexistence-unavailable messages; only the latter instructs agents to check WhatsApp Business
- **Template Messages** - Send messages outside the 24-hour window with approved templates; automations locally block free-form sends in that state and prompt users to use a template
- **WhatsApp Cloud Direct Send (beta)** *(Mega)* - Once Meta enables the inbox in the beta, the WhatsApp button in the reply box and in new conversations lets agents choose between a template and Direct Send: a form to send a utility message without picking a template, also outside the 24-hour window, with up to 3 reply buttons, one link button or a Call on WhatsApp button, a text, image, video or document header, an optional footer and a delivery time limit. Meta creates the templates itself. The API can also set the template name and send verification codes (authentication messages) once Meta enables them for the account. Account Health shows whether the inbox likely qualifies (100K or unlimited messaging limit); the switch only appears in that case, and Direct Send turns off if the inbox stops qualifying. Free text still needs a template outside the window. It is turned on per inbox
- **WhatsApp Cloud interactive messages** *(Mega)* - While the 24-hour window is open, the WhatsApp button in the reply box and in the new conversation form offers "Interactive message": a form with a WhatsApp-style preview to send up to 3 reply buttons, a list of up to 10 options with descriptions, a link button, a carousel of 2 to 10 image or video cards, a Pix charge (copy-and-paste code with the amount, for Brazil) or a location request, with an optional text, image, video or document header and footer. Files are uploaded from the same form, or a public URL can be pasted. Every field takes the platform variables (`{{contact.first_name}}`, custom attributes, etc.). In the conversation they render like templates, with header, footer and buttons, the list expands, the carousel scrolls and Pix lets agents copy the code. Also available through the messages API, Outbound Messages (`type: interactive`), MCP and Mega Assistant, documented in Swagger/OpenAPI and Postman.
- **WAHA interactive messages** *(Mega)* - WAHA inboxes send interactive messages at any time, with no 24-hour window: reply buttons (up to 3), action buttons (open link, call or copy a code, up to 5), list, carousel with an image per card, Pix payment (the customer types the amount), order with "Review and pay" (items, discount, total and Pix key), poll (one or several answers), location, event with date and place, and a reply to a buttons message (API only). The WhatsApp icon in the reply box and in new conversations opens the same form with live preview as WhatsApp Cloud, on desktop and phone, with a text, image, video or document header. Carousel, Pix, order and event need the GOWS engine. Direct chats only: the option does not show in groups. Sent messages show in the conversation like templates, and the customer's answers (tapped button, list option, poll vote or event response) come in as messages. Enabled per WAHA server in Super Admin → WhatsApp Providers (*Interactive messages* switch) or for the whole installation with `WAHA_INTERACTIVE_MESSAGES=true`, and per account with the *WAHA Interactive Messages* feature. Also available through the messages API, Outbound Messages and MCP, with the 10 examples in Swagger/OpenAPI, Postman and the Super Admin API docs.
- **UazAPI interactive messages** *(Mega)* - UazAPI inboxes send interactive messages at any time, with no 24-hour window, in direct chats and groups: reply buttons, action buttons (open link, call or copy a code), list with sections, poll, carousel with an image, video or document per card, Pix button, payment request with "Review and pay" (amount, item, invoice, Pix key, boleto, payment link and attached PDF), event with date, place, link and reminder, and location request. The WhatsApp icon in the reply box and in new conversations opens the same form with a preview, on desktop and phone; buttons take an image, video or document header. In the conversation they show like templates; customer answers (tapped button, list option, poll vote, event answer) come in as messages that quote the original, and the agent can send the customer the order status (payment requested, preparing, shipped, delivered, completed or canceled, paid or pending) from the payment request bubble. The add-on can be sold for the whole account or per inbox: then each unit turns interactive messages on in one inbox (*Interactive messages* switch in the inbox settings) and the others show it locked until another unit is bought; the same goes for WAHA interactive messages. Turned on per UazAPI server in Super Admin → WA Providers (*Interactive messages* switch) or for the whole installation with `UAZAPI_INTERACTIVE_MESSAGES=true`, and per account with the *UazAPI Interactive Messages* feature. Also available through the messages API, Outbound Messages, the account MCP and Mega Assistant, with 11 examples in Swagger/OpenAPI, Postman and the Super Admin API docs.
- **Mark chats as read on WhatsApp (UazAPI)** *(Mega)* - Per UazAPI inbox option, off by default, in the *Chats* card of the inbox settings: when an agent opens a conversation with unread messages or a reply goes out to the customer, the chat shows as read on the line's phone (its unread badge clears). The contact sees the blue ticks only if the WhatsApp account has read receipts turned on in its privacy settings.
- **Chosen option id in WhatsApp answers** *(Mega)* - When a customer picks a list option or taps a reply button (WhatsApp Cloud, WAHA and UazAPI), the message keeps the id the option was sent with, besides its text. Integrations that send lists or buttons through the API or Outbound Messages get that id back in the webhook and in the messages API and know exactly which option was chosen. Documented in Swagger/OpenAPI, Postman and the Super Admin API docs. Reply buttons can carry an id of their own too (`{ id, title }`), not only lists.
- **Contact Sync** - Keep your database automatically updated
- **Share contacts** *(Mega)* - Send a saved contact as a native WhatsApp contact card from the reply box (Cloud, WAHA, Uazapi, NotificaMe and Twilio WhatsApp); forwarded contacts keep their name and phone number
- **Group Support** - Manage WhatsApp group conversations directly

**WhatsApp Ad Tracking:**

Measure your WhatsApp advertising ROI:

- **Click-to-WhatsApp Ads** - Detect conversations from Facebook/Instagram ads
- **Ad Data Capture** - Automatically save ad source, campaign, and creative info
- **Visual Indicator** - See ad information card in conversation
- **Attribution** - Connect leads with specific ad campaigns

**Group Members Management:** *(Mega)*

Complete control of WhatsApp groups directly from MEGA:

- **Member List** - View all group participants with their role and status
- **Automatic Sync** - Members are automatically synced when conversation is created
- **Add Participants** - Add new members to the group from the platform
- **Remove Participants** - Remove members from the group without leaving MEGA
- **Change Roles** - Promote or demote members to admin
- **Group Mentions** - Use @ to mention specific members in messages, including when editing WAHA group messages
- **Member Search** - Quickly find participants in large groups
- **Smart Pagination** - Efficient loading for groups with many members
- **Member Avatars** - View each participant's profile picture
- **Background Sync** - Periodic updates of names and photos
- **Multi-provider Support** - Works with Evolution, WAHA, Uazapi and Cloud API

### Instagram Direct

Connect with your Instagram audience and convert followers into customers right where they already interact with your brand.

**Why Instagram?**

With over 2 billion active users, Instagram is essential for visual brands. 90% of users follow at least one business, and DMs are the preferred channel for inquiries.

**Supported interaction types:**

- **Direct Messages (DMs)** - Respond to private inquiries from your followers
- **Mega Hub for Instagram** *(Mega)* - Connect Instagram through shared Hub apps using dedicated credentials configured in Mega Hub
- **Story Replies** - Engage with those who react to your stories
- **Story Replies with Content** - See images and videos attached when replying to your stories
- **Story Mentions** - Get alerts when you're mentioned
- **Reactions** - See when they react to your messages

**Ad Tracking:**

A powerful feature to measure your Instagram advertising ROI:

- **Lead Origin** - Automatically detect if the message comes from an ad
- **Campaign Data** - Save which ad generated each conversation
- **Automatic Attribution** - Connect sales with specific campaigns
- **Clear Metrics** - Know exactly how many leads each ad generates

**Extended Response Window:**

- **7 days to respond** - Instead of the standard 24 hours, you have up to 7 days to respond
- **Automatic Activation** - Applied without additional configuration

**Multimedia Content:**

- **Images and videos** - Send and receive visual content
- **Quick replies** - Buttons for customer options
- **Product catalogs** - Send products directly in chat
- **Conversation starters** - Help customers start the chat

**Benefits for your business:**

- Convert followers into buyers
- Customer service where your fans already are
- Measure your Instagram advertising impact

### Facebook Messenger

Serve your customers directly from the world's most used messaging app, integrated with your Facebook pages.

**Why Facebook Messenger?**

With over 1.3 billion active users, Messenger is the preferred channel for customers to contact businesses. Your customers can message you from your Facebook page, ads, or directly from the app.

**Main features:**

- **Connect in minutes** - Link your Facebook page with a couple of clicks, no technical setup required
- **Mega Hub for Messenger** *(Mega)* - Use shared Hub apps as a configurable alternative with dedicated Hub credentials
- **Multiple pages** - Manage all your Facebook pages from a single platform
- **Accurate contact names** - Keep the name provided by Facebook without adding missing name parts
- **Read receipts** - Know when the customer read your message
- **Delivery confirmations** - Verify that your messages arrived correctly
- **Welcome messages** - Automatically greet first-time customers
- **Bot integration** - Seamlessly combine automated responses with human support
- **Instagram linking** - Connect your associated Instagram account to manage both channels

**Benefits for your business:**

- Respond where your customers already are
- Complete conversation history with each customer
- Smooth transition between chatbots and human agents
- Performance metrics by channel

### Facebook and Instagram comments *(Mega)*

Handle the comments on your posts, reels and ads from the same inbox where you already answer direct messages.

**Key features:**

- **Comments in the conversation** - Each comment arrives as a message in the commenter's conversation, next to their direct messages, with the post card (picture, text and a link to open it, kept on the platform so it does not get lost), just like WhatsApp ads
- **Public reply from the comment** - Reply from the message menu ("Reply to comment") and the answer is published below it, visible to everyone
- **Private message** - Take the conversation private with a direct message to the commenter (one per comment, within 7 days)
- **Moderation** - Hide, show again or delete comments without leaving the platform
- **API, MCP and Mega Assistant** - Reply publicly or privately, hide and delete comments through the API (also with `comment_reply` in Outbound Messages, with just the comment id), from the account MCP server and with Mega Assistant; all documented in OpenAPI/Swagger and Postman, shown in the Super Admin API docs
- **Comment-to-DM with Flow Builder** - A flow can start on every comment (by post or by keywords), and "Message received" flows and bots can handle comments too; the flow can reply publicly, send the private message, or hide or delete the comment
- **Per-inbox opt-in** - Each Facebook or Instagram inbox decides whether it receives comments with "Receive comments from posts and reels" (off by default; without it, comments do not come in) and whether it takes only top-level comments
- **Conversations for the bot or for the team** - A conversation started by a comment stays pending when the inbox's Flow Builder bot includes comments; otherwise it opens for agents

### TikTok Business

Connect with the youngest and most dynamic audience in the world through TikTok, the fastest-growing social network.

**Why TikTok?**

With over one billion active users, TikTok has become an essential platform for reaching Gen Z and Millennials. Now you can handle customer inquiries through direct messages.

**Main features:**

- **Text messages** - Send and receive messages with your followers
- **Images** - Share and receive visual content
- **Stickers** - View stickers your customers send
- **Shared posts** - When a customer shares a post with you, see it directly in the conversation
- **Reply to specific messages** - Respond in context to previous messages
- **Social profile link** - View customer's TikTok profile directly in their contact info
- **Unsupported messages** - Clear indicators when incompatible content is received
- **Configurable API version** - Flexibility to adapt to different API versions

**Benefits for your business:**

- Reach the youngest audience where they spend their time
- Convert social interactions into sales opportunities
- Secure, official connection via TikTok Business API
- TikTok connection access is controlled per account; hosted accounts without access can request it from support in the inbox setup.
- Complete real-time message sync

### Email

Email remains one of the most important channels for business communication. Manage all your emails as if they were chat conversations.

**Why integrate Email?**

Many customers prefer email for formal inquiries, documentation, or follow-ups. With MEGA, all your emails are managed alongside other channels.

**Main features:**

- **More reliable email** - No duplicate emails when IMAP fetches overlap, sender names with commas no longer break sending, SMTP without IMAP (forwarding inboxes), and subject search, with the subject shown in the conversation header
- **Unified inbox** - All emails appear as conversations alongside WhatsApp, social media, and more
- **Rich replies** - Send emails with formatting, images, and attachments
- **Large files by email** *(Mega)* - Super Admin sets the largest attachment allowed in email replies; anything over 20 MB in total reaches the customer as a download link, and the editor tells the agent
- **Large files when starting an email conversation** *(Mega)* - The new conversation window uses the same maximum attachment size as email replies, uploads files straight to storage when direct uploads are on, and warns when attachments go over 20 MB and will arrive as download links; attachments can also be dragged and dropped onto the window
- **Resizable inline images** - Insert images in the email body and adjust their displayed size visually
- **Images inside the email** *(Mega)* - Body and agent signature images travel inside the email reply, so Outlook and other clients that block remote images show them without asking; images over the limit stay as links
- **Tables in email replies** - Insert a table from the editor menu, edit it in place and send it as a bordered table that keeps its look in Gmail and Outlook, light or dark
- **Forward by email** - From any message of an email conversation, forward it to new recipients (To, Cc, Bcc) with your own note, the original email you can edit and the attachments you keep; it goes out as a new email (Fwd:), the contact does not receive it, and replies from each recipient open their own conversation. The regular Forward to contacts stays as it is
- **Custom subject** - Email replies show a Subject field prefilled with "Re: <subject>" (or the last subject you changed); edit it to send that reply with a different subject
- **Other recipients kept in CC** - Replying to an email addressed to several people keeps the other To recipients of that email in CC, so nobody drops out of the thread
- **Custom signatures** - Configure professional signatures per agent or inbox
- **Any provider** - Connect Gmail, Outlook, your own server, or any email
- **Guided setup** - Detect Gmail or Outlook hosting from your domain to suggest the right integration
- **Gmail connection check** - Verify IMAP and SMTP live, review recent email activity, and reconnect the account from inbox settings
- **Permanent Gmail-synced deletion** - Deleting an email or conversation from a Gmail inbox permanently deletes it in Gmail too
- **Complete history** - Entire email thread visible in one conversation
- **Quoted replies** - With quoted replies on for the account, every email reply carries the previous thread behind a collapsed "…" preview under the editor; remove it for one message and bring it back with Cmd/Ctrl+Z. Quoted customer text is never evaluated as variables

**Benefits for your business:**

- One place for emails and instant messaging
- Agents don't need to switch between applications
- Unified metrics across all channels

### Web Widget (Live Chat)

Offer instant support to your website visitors with an elegant, fully customizable live chat widget.

**Why Live Chat?**

Your website visitors want immediate answers. Live chat increases conversions by up to 40% and improves customer satisfaction.

**Form configuration:**

- **Lighter, more private widget** - The email request no longer duplicates, crawlers don't create contacts, public pages set no session cookie and the dashboard stays out of search engines
- **Pre-chat form** - Collect name, email, and phone before starting
- **Custom fields** - Add the fields you need for your business
- **Automatic validation** - Ensure entered data is correct; required checkboxes must be selected before submission
- **Offline mode** - Receive messages even when no agents are available

**Full visual customization:**

- **Your brand colors** - Adjust primary and background colors
- **Your logo** - Display your brand in the widget
- **Flexible position** - Left or right corner
- **Custom icon** - Change the floating button
- **Welcome message** - Proactively greet visitors

**Advanced features:**

- **User identification** - Recognize logged-in users on your site
- **Protected contact details** - The widget does not receive the contact's stored email, name or phone number: it only learns which ones exist, to decide what the pre-chat form asks for. Messages sent by the visitor do not carry their details either.
- **Protected identified contacts** - When a visitor types, in the pre-chat form or the email request, an email or phone number that belongs to a contact your site identified, the contacts are not merged and the detail is not saved: agents see a private note in the conversation with the detail and a link to the matching contact. The merge only happens when the visitor arrives identified with the same identifier.
- **Email transcript** - Customers can request conversation history; repeat requests are temporarily disabled after a successful send
- **Dark mode** - Adapts to visitor preferences
- **Formatted visitor messages** - Lists the visitor sends show their bullets and numbers
- **Integrated Help Center** - Show help articles directly in the widget
- **Predefined messages** - Start conversations with context
- **Inline images in replies** - Send screenshots or visual resources inside the message body and adjust their size
- **Allowed domains** - Restrict widget to authorized domains for added security
- **Show agent name** - Configure per inbox whether the agent's name is shown to visitors
- **Reply auto-assignment control** - Disable per inbox whether unassigned conversations are assigned to the agent when they send a message
- **Resolved-conversation protection** - When an inbox disallows messages after resolution, the widget rejects retries and new text or attachment submissions for that conversation; visitors can start a new conversation instead
- **Layering/background fixes** - Better visual rendering between launcher and portal, including dark mode scenarios

**Benefits for your business:**

- Convert visitors into customers while they browse
- Reduce shopping cart abandonment
- Offer immediate support without customers leaving your site

### SMS

Reach your customers even when they don't have internet or messaging apps, with traditional text messages.

**Why SMS?**

SMS has a 98% open rate, much higher than any other channel. It's ideal for urgent notifications, confirmations, and communication with customers who don't use apps.

**Main features:**

- **Send and receive** - Two-way communication with your customers
- **Virtual numbers** - Configure multiple phone lines
- **Twilio integration** - World-leading SMS provider
- **Verified Twilio webhooks** - Messages and statuses that Twilio sends for SMS and WhatsApp are checked against Twilio's signature. Each inbox starts in log-only mode and, from the first request with a valid signature, rejects requests without one; a setup that does not sign yet keeps working. Inboxes connected with an API Key and without the account auth token are not verified.
- **Twilio WhatsApp inbox health** - Account health also covers Twilio WhatsApp inboxes: it checks the messaging and voice webhooks and shows the WhatsApp sender status, display name, quality rating and messaging limit; registering the webhook works for them too
- **Bandwidth with OAuth** - Bandwidth SMS inboxes connect with Bandwidth's Client ID and Client Secret, which are verified before saving. Bandwidth stops accepting API user credentials on December 2, 2026: for existing inboxes, an administrator must save the Client ID and Client Secret in the inbox settings before that date.
- **Protected Bandwidth webhooks** - Each Bandwidth inbox's callback URL carries a secret token. An administrator copies it from the inbox Configuration tab and pastes it into the Bandwidth application. Until Bandwidth calls the tokened URL for the first time, callbacks without the token are still accepted and logged; from then on they are rejected.
- **Mass campaigns** - Send messages to your entire contact base

**Benefits for your business:**

- Reach customers without smartphones or data
- Notifications that actually get read
- Ideal for reminders and confirmations

### Telegram

Connect with millions of users who prefer Telegram for its speed, security, and advanced features.

**Why Telegram?**

Telegram is especially popular among tech-savvy users and in regions like Eastern Europe, Middle East, and parts of Latin America. It's known for its speed and privacy.

**Main features:**

- **Setup in minutes** - Connect your Telegram bot easily
- **Formatted messages** - Send text with bold, italics, and more
- **Full multimedia** - Images, videos, documents, and more
- **Interactive buttons** - Offer quick reply options to your customers
- **Contextual replies** - Reply to specific messages for clarity
- **Telegram Business** - Support for Telegram business accounts

**Benefits for your business:**

- Automatic profile photos from contacts
- No file size limits
- Messages arrive instantly

### API Channel

For businesses with unique needs: integrate any proprietary or third-party messaging system.

> **Availability:** API-token access and outbound Webhook delivery require API and Webhooks access for the account on hosted plans. They remain available on self-hosted installations.

**When to use API Channel?**

If you have your own messaging system, a mobile app with chat, or need to connect a platform that isn't natively integrated, API Channel gives you total flexibility.

**Main features:**

- **Custom integration** - Connect any message source
- **Incoming webhooks** - Receive messages from external systems
- **Response API** - Send responses back to your system
- **Identity validation (HMAC)** - On inboxes with mandatory identity validation, every public API call about a contact (the contact, its conversations and its messages) must include the `identifier_hash` that signs that contact's identifier; a missing or mismatched hash is rejected. In the account API, HMAC verification is computed on the server from `identifier` and `identifier_hash`, and a client-sent `hmac_verified` is ignored.
- **Universal send API for integrations** *(Mega)* - One authenticated request identifies the recipient by phone, email, contact, or provider ID, automatically prepares the contact and conversation, and sends text, media, or WhatsApp templates through any compatible inbox. WhatsApp Cloud media templates can upload their file in the same request, and rendered template content remains visible in the conversation. Idempotency keys make retries safe.
- **No limits** - Adapt the platform to any imaginable channel

**Use cases:**

- Mobile apps with custom chat
- Customer portals
- Legacy messaging systems
- Integrations with non-natively supported providers

### LINE

Connect with LINE users, the leading messaging app in Japan, Taiwan, Thailand, and Indonesia with over 200 million active users.

**Why LINE?**

If your business serves customers in Asia, LINE is essential. In Japan, 90% of smartphone users use LINE daily.

**Main features:**

- **Simple setup** - Connect your LINE Official account in minutes
- **Text messages** - Fluid communication with your customers
- **Stickers and multimedia** - Send attractive visual content
- **Security** - Credentials protected with advanced encryption

**Benefits for your business:**

- Access to the Asian market
- Highly engaged users
- Ideal for international e-commerce

### Twitter / X

Handle inquiries and manage your brand reputation on the social network where the most important public conversations happen.

**Why Twitter/X?**

Twitter is where customers express complaints, ask questions, and seek public support. A quick, professional response can turn a complaint into a positive review.

**Main features:**

- **Direct Messages (DMs)** - Manage private conversations with your customers
- **Public mentions** - Option to monitor when you're mentioned
- **Automatic contact creation** - Twitter profiles are saved automatically
- **Secure connection** - Official authentication with X API
- **Signed events** - Only X events that arrive with a valid app signature (`TWITTER_CONSUMER_SECRET`) are accepted; the rest are rejected.

**Benefits for your business:**

- Respond quickly to public complaints
- Convert interactions into opportunities
- Improve your brand perception
- Identify trends and customer feedback

### Voice Channel - Twilio *(Enterprise)*

Transform your team into a professional call center with VoIP telephony integrated directly into the platform using Twilio Voice SDK.

**Why add calls to your operation?**

Some customers prefer talking on the phone, especially for urgent or complex matters. With Voice Channel, your agents can receive and make calls without leaving MEGA.

**Technology Stack:**

- **Twilio Voice SDK** - Industry-leading VoIP provider
- **WebRTC** - Browser-based calling, no software required
- **TwiML Apps** - Custom call handling and routing
- **Phone number provisioning** - Get numbers in 100+ countries

**Inbound Calls:**

- **Smart reception** - Calls automatically create conversations
- **Caller identification** - Recognize existing contacts by phone number
- **Automatic new contacts** - If the number is new, contact is created
- **Withheld numbers** - Calls with a hidden caller ID are answered too: each one creates an "Unknown caller" contact with its own conversation, where the call buttons are hidden and only private notes can be written
- **Unified history** - Calls and messages in the same timeline
- **Queue management** - Handle high call volumes

**Caller experience and routing** *(Mega, Voice tab of the inbox)*:

> **Opt-in:** the greeting, business hours, ring time limit and one-agent-at-a-time routing are off on existing and new inboxes; until they are turned on, calls ring every agent who can see them, with no time limit, as before.

- **Greeting** - Callers hear a welcome message, spoken in the account's language, while agents are rung, then wait music
- **Calls only in business hours** - With the inbox's business hours on, a call that arrives while the inbox is closed hears an out-of-hours message and ends without ringing anyone; it is recorded as a missed call marked "Outside business hours". Business-hours exceptions do not apply to calls
- **Ring time limit** - An unanswered call ends after the seconds you choose (10 to 600), the caller hears an optional message and the call is recorded as missed
- **One agent at a time** - Calls ring one free agent at a time with the same policy as WhatsApp Cloud calls: the conversation's assignee first, then the inbox's online agents in turn, then administrators who turned on call notifications. Escalation time, attempts, what to do when the assignee is on another call and the last agent's ring time reuse the WhatsApp call settings. When nobody can take the call it ends with the unanswered message, marked "No agents available". The conversation keeps its assignee: there is no hand-back after the call
- **Busy on any call** - An agent on a Twilio call counts as busy for WhatsApp calls, and an agent on a WhatsApp call counts as busy for Twilio routing
- **Declines that stick** - Each call records who it rings. An agent who declines stops ringing in every open tab and the call does not come back after a reload; a call still ringing for the agent shows again when the page reloads (for up to an hour)

**Outbound Calls:**

- **Click-to-call** - Call any contact with a single click
- **From contact profile** - No manual number dialing
- **Clear call errors** - When a call cannot start, the agent sees the reason, for example a contact without a phone number
- **Conference calls** - Easily connect agent and customer
- **Caller ID customization** - Show your business number

**Complete tracking:**

- Record of all calls (answered, missed, busy)
- Duration and timestamps for each call
- Identification of inbound vs outbound calls
- Full history visible in customer conversation
- Optional Twilio-native call recording with explicit storage-cost acceptance
- Downloadable recordings in the conversation and call reports

**Agent Features:**

- **Browser webphone** - Answer calls directly in MEGA
- **Mute/Unmute** - Control microphone during calls
- **Hold and resume** - The agent on the call puts the caller on hold (the caller hears wait music) and resumes the call; the call shows "On hold" meanwhile
- **In-call keypad** - Send keypad tones during a connected call, for phone menus and extensions; also on WhatsApp Cloud calls
- **Call conversations open on private note** - A conversation whose last message is a call opens the reply box on Private note, for notes about the call; switching to Reply stays for that visit
- **Transfer calls** - Route to another agent or department
- **Only the handling agent hangs up** - Only the agent who accepted the call can end it; an incoming call that is still ringing and nobody accepted can be declined by any agent of the inbox.

**Benefits for your business:**

- Additional channel without switching tools
- Complete customer context when answering
- Call metrics alongside other channels
- Scalable from 1 to 1000+ agents
- Pay-as-you-go pricing with Twilio

### WhatsApp Cloud Calls *(Enterprise/Mega)*

Make and receive voice calls through WhatsApp using Meta's Cloud API with WebRTC technology.

> **Availability:** Calls are not available for WhatsApp Cloud numbers connected through WhatsApp Business App coexistence. They continue in the WhatsApp Business app and are not shown in MEGA.

**Why WhatsApp Calls?**

Many customers prefer voice communication for complex issues. WhatsApp Calls let your agents handle voice calls directly within the platform, using the same WhatsApp number used for messaging.

**Inbound Calls:**

- **Real-time notifications** - Agents receive instant call alerts
- **Accept/Reject from browser** - Handle calls without any external app
- **Smart agent assignment** - Calls routed one at a time to the inbox members who are online, even with auto-assignment off; administrators who enabled call notifications are used only as a fallback
- **Auto-reject when unavailable** - Configurable behavior when no agents online
- **Assigned agent on another call** - Configurable per inbox: the call rings another available agent (default) or only the assigned agent. If the same contact calls again during an ongoing call, that call is not interrupted
- **Calls only in business hours** - Optional per inbox in the call settings: with the inbox business hours on, WhatsApp only lets customers call during those hours, in the inbox timezone, and a lunch break stays closed. If Meta rejects the hours, the call settings are still saved and the reason shows under the switch
- **Caller identification** - See contact info before answering

**Outbound Calls (Business-Initiated):**

- **Click-to-call** - Start calls from a conversation or a contact profile, including contacts without an existing conversation
- **Permission system** - Request and track call permissions inside the 24-hour customer service window
- **One call per agent** - Prevents starting a second call while the agent already has an active one, including from another tab
- **Call-permission templates** - Use approved permission-request templates from the ReplyBox, set one default per inbox, and show the sent request in the conversation timeline
- **Call permission status** - Visually distinguish no permission, 7-day temporary permission, and permanent permission; confirm the status and ability to start a call with WhatsApp and record every change, including temporary expiry, in the conversation activity
- **Ringback tone** - Audio feedback while connecting

**Call Features:**

- **WebRTC native** - High-quality audio without external SDKs
- **Adaptive connectivity** - Uses configured STUN/TURN servers for premium calls when a restricted network prevents a direct connection
- **Protected assignment** - From call acceptance until it ends, the conversation's assignee and team cannot change; reassignment remains available while it is only ringing
- **Mute/Unmute** - Toggle microphone during calls
- **In-call keypad** - Send keypad tones during the call, for phone menus and extensions (WhatsApp Cloud and Twilio; not WAHA)
- **Call duration** - Real-time timer visible during call
- **Only the handling agent hangs up** - Only the agent who placed or answered the call can end it; an incoming call nobody has answered can be ended by anyone who can see the conversation.
- **Server-side audio (beta)** - Turned on per account from Super Admin ("Voice Engine" feature) when the installation has the engine deployed; the account cannot turn it on itself, and once on it covers its WhatsApp Cloud and WAHA inboxes: Mega's voice engine answers the call, so reloading the agent's page no longer drops the caller and the agent rejoins the call
- **Hold music** - With server-side audio, each WhatsApp Cloud inbox chooses what the caller hears on hold: one of five bundled melodies or an audio file of its own (MP3, WAV, OGG or M4A, up to 10 MB and 10 minutes), with a preview player in the settings
- **Call transfer** - With server-side audio, the agent on a call hands it to another available agent of the inbox (searchable by name) without dropping the caller: the caller hears the hold music while the call rings for the other agent (on every tab and device, showing who transfers it). If they take it, the call and the conversation move to them; if they decline, don't answer within 30 seconds or the first agent cancels, the caller is back with the first agent
- **Consultative transfer** - Before handing the call over, the agent can consult another agent: the caller hears the hold music while the two agents talk, then the first agent transfers the call or returns to the caller. If the other agent declines, doesn't answer within 30 seconds or hangs up the consultation, the caller is back with the first agent
- **Server-side call recording** - With server-side audio every answered call is recorded on the server, with both sides (including hold music and the agent a transfer moved the call to), and attached to the conversation as a private note with the audio, like the other call recordings. A page reload or a transfer does not cut it
- **Server-side audio on WAHA** - With the feature on, WAHA inboxes use server-side audio too: incoming and outgoing calls go through Mega's voice engine, so the agent rejoins after a reload and can put the caller on hold with the inbox's music and transfer the call (direct or after consulting another agent). Several WAHA calls can be live at once. WAHA keeps recording the calls
- **Call menu (IVR)** - A Flow Builder flow that starts on "Call received" answers the WhatsApp calls (Cloud or WAHA) of an inbox with server-side audio as a phone menu: the caller hears audio prompts the account uploaded (MP3, WAV, OGG or M4A) or generated with AI from a text, picking the speech model and voice among the account's AI providers (reusable across flows; generated once when saved, and again when the text, model or voice changes), presses a key ("press 1 for sales, 2 for support"), and the flow transfers the call to the whole inbox or a team, plays more audio or hangs up. It asks again after a wrong key or silence, and the business hours and agents available checks work in these flows. If no agent is free, the call can wait in a queue with the hold music and ring the first agent who frees up, in the order calls arrived, up to a longest wait set in the block. Every step shows in the flow's executions Twilio voice inboxes can use the menu too: play prompts, ask for a key, transfer to the whole inbox or a team, and hang up (no waiting queue or AI for now).
- **AI on calls** - In a call flow, "Answer with AI" lets an AI agent talk with the caller in real time and take care of the call itself: it holds a natural conversation, answers with the inbox's Captain assistant (its knowledge and tools) or with instructions written in the block, and puts the caller through to a person only when they ask for one or it cannot help. It tells the caller it is a virtual assistant in its greeting (on by default). What was said is added to the conversation as a private note. "Ask by voice" lets the caller answer a menu by speaking ("sales or support?") instead of pressing keys, which is how menus work on WAHA; it returns the caller's greeting and confirms the option with a friendly sentence ("Of course, one moment") before passing the call on, and the AI agent that follows already speaks the language the caller used. Charged in AI Actions per 5 minutes of talk
- **VoIP optimization** - Audio optimized for voice calls

**Call History:**

- **Answered calls** - With duration and timestamp
- **Missed calls** - Automatic detection
- **Call back** - The latest missed or failed call shows the line it came through and a button to return it from the chat
- **Rejected calls** - Track declined calls
- **Timeline integration** - All calls appear in conversation history

**Technical Requirements:**

- WhatsApp Cloud API inbox
- Business phone number configured with Meta
- Open customer service window or approved template to reopen the conversation before requesting permission
- Modern browser with WebRTC support

---

### WhatsApp WAHA Calls *(Mega)*

Receive and place WhatsApp voice calls from MEGA with numbers connected through WAHA, using the same call widget as WhatsApp Cloud.

**Availability:**

- Enabled per installation with `WAHA_VOICE_CALL=true` or per WAHA server in Super Admin → WhatsApp Providers (*Voice calls* switch); incompatible servers show nothing
- Then turned on per account (*WAHA Voice Calls* feature) and per inbox in the session settings → Apps → *Voice calls*

**Incoming Calls:**

- **Same widget as Cloud** - Real-time alert, accept or reject from the browser, and routing to the conversation's agent or round-robin
- **Same call settings as Cloud** - Under Apps → *Voice calls* → *Call settings*: escalate to the next agent, what to do when the assigned agent is on another call (ring another available agent or only the assignee), auto-reject and unavailable messages
- **The conversation goes back to its owner** - When a call rings another agent because the assigned one is on another call or didn't answer, the conversation shows who it went to and why, and goes back to its assigned agent once the call ends
- **Group calls rejected** - Only direct calls reach agents
- **History in the conversation** - Every call is recorded as a message: completed with its duration, missed, or rejected
- **Automatic recording** - WAHA records answered calls (incoming and outgoing) and the recording is attached to the conversation as a private note

**Outgoing Calls:**

- **Click-to-call** - Call button in the contact panel (or in the method selector when the inbox has several)
- **One call per agent** - A second call cannot start while one is active
- **Unanswered calls end on their own** - If WAHA never reports the end of an unanswered call, Mega ends it after 2 minutes, so the agent can place the next one

**Security:**

- The browser never receives a WAHA credential: Mega negotiates the audio with WAHA, and agents can only open the audio of the call they answered or placed
- Only the agent who placed or answered the call can end it; an incoming call nobody has answered can be ended by anyone who can see the conversation

**Requirements:**

- WAHA server with the GOWS engine, the `voice-calls` app and WebRTC enabled (`WAHA_CALLS_WEBRTC_PUBLIC_IP` and the UDP port open; on Docker Swarm, published with `mode: host`)
- Modern browser with WebRTC support, over HTTPS

---

## 💬 Conversation Management

### Smart Inbox

- **Unified view** - All conversations in one place
- **Advanced filters** - By status, inbox, agent, team, labels
- **Number attributes** - Number custom attributes filter by equal, not equal, present, greater or less; choosing *Contains* shows a warning in the filter instead of failing
- **Sort filtered results** - Advanced filter results and folders can be sorted like the regular list (newest, oldest, priority, waiting time)
- **Date filters in your local time** - Created and last-activity date filters use the day in your timezone, like reports, and a filter's counts no longer flip back to the general totals
- **Email attachment indicator** - Email conversations show a 📎 in the list when the customer sent files, with a tooltip of count and file types (e.g. "2 attachments: CDR, PDF"); inline signature images do not count, and the **Email attachments** filter segments them
- **Multi-select filters** - Select multiple inboxes or teams simultaneously
- **Label filters with AND logic** - Filter by multiple labels that must all match
- **Custom views** - Save frequent filters as quick views
- **Powerful search** - Find conversations by content, contact, or metadata
- **Sidebar quick filters** - Navigate directly to Unread, Mentions, Participating, Groups, and Unattended from the sidebar
- **Reactive unread badges** - Mentions, Participating, Groups, and Unread show live counters without page reloads
- **Exact timestamp on hover** - Relative dates reveal the full date and time in the conversation list, messages, contacts, search, reports, and related dashboard cards

### Custom attribute integrations

Integrations can update only the supplied conversation custom-attribute keys or replace them entirely. They can also remove specific keys without changing the remaining information.

### Message Search in Conversation

Find specific messages within a conversation:

- **Text search** - Search for words or phrases within all messages
- **Audio transcription search** - Find voice notes by words or phrases contained in their transcription
- **Date filter** - Narrow search to a specific date range
- **Result highlighting** - Found messages are visually highlighted
- **Auto-scroll** - Navigate instantly to the found message
- **Result pagination** - Navigate between multiple matches easily
- **Context preserved** - See the message in its original conversation context

### Conversation Status

- **Open** - Conversations requiring attention
- **Pending** - Awaiting customer response
- **Resolved** - Completed conversations
- **Snoozed** - Schedule automatic reactivation using natural language: type "tomorrow at 3pm", "in 2 hours", "next Monday" or any time expression and the system parses it automatically; classic date picker also available
- **One active conversation per contact** - If the contact already has an open or pending conversation in the same inbox, a resolved one cannot be reopened or replied to: the system points to the active conversation to continue there. Search shows each conversation's status with its color

### Prioritization

- **Priority levels** - Urgent, High, Medium, Low
- **Smart sorting** - By recent activity, wait time, priority
- **Unread-first sorting** - Prioritize conversations with unread messages directly from the sort selector
- **Visual indicators** - Quickly identify critical conversations
- **Reply window countdown** - On WhatsApp Cloud, 360dialog, NotificaMe and the other channels with a reply window (Messenger, Instagram, TikTok, Twilio WhatsApp, API with a reply time), the conversation header shows "Window open · closes in 3h 12min" with the exact time on hover, and each list card shows the time left: amber under 2 hours, red once it closes. When it closes while the conversation is open, the editor switches to message templates on its own

### Team Collaboration

- **Agent assignment** - Manual or automatic
- **Team assignment** - Route to specific departments
- **Mentions (@)** - Notify colleagues in conversations
- **Private notes** - Communicate internally without customer seeing
- **Private-note mention counters** - Internal mentions raise the Mentions sidebar badge in realtime

### Conversation Participants

Multiple agents can collaborate on a single conversation:

- **Add participants** - Include additional agents in conversations
- **Participant notifications** - All participants receive message alerts
- **Pin conversations** - Participants can pin important conversations
- **Participant list** - See all agents involved in a conversation
- **Remove participants** - Remove agents when no longer needed
- **Auto-participants** - Agents who interact are automatically added

### Reply editor shortcuts

- Send shortcuts do not accumulate duplicate actions when switching conversations. Enter/Ctrl/Cmd+Enter preferences and closing mentions with Escape are preserved.
- Typing "/" in the reply box or any other text field on the search page stays in that field; "/" only jumps to the search box when no text field has focus.
- The canned response and macro pickers keep the highlighted option when their list refreshes in the background.

### Collapsible reply box

- On desktop and tablet, the reply box folds away to give the conversation more room for reading: use the collapse button next to the expand button, or drag the resize handle below its minimum height.
- A slim bar stays at the bottom with **Reply** and **Private note** (Alt+L / Alt+P, ⌥ on Mac); it shows "Unsent draft" when text or attachments are waiting. Replying to a message, inserting content, a Captain action or pasting a file also brings the reply box back.
- Drafts, attachments and the selected mode are kept while folded. The choice is remembered for the agent across conversations and devices.
- Phones keep their one-row floating composer and are never folded.

### Canned Responses

Quick templates with shortcuts for faster responses:

- **Personal responses** - Visible only to you
- **Shared responses** - Available to entire team
- **Shortcut activation** - Type / to access responses
- **Variable substitution** - Dynamic placeholders for contact info
- **Attachments support** - Include images, documents, and files with responses
- **Multi-file attachments** - Attach multiple files to a single canned response
- **Canned attachments in new conversations** - Reuse canned response files even when starting a brand new conversation
- **Search and preview picker** - Search shortcuts and message content, preview the rendered response, and retain unresolved variables for backend processing
- **Instant cached search** - Load responses once per account and filter locally while realtime invalidation keeps browser data current
- **Rich content** - Format text with markdown support

### Voice Recorder

- **Audio notes** - Record and send voice messages
- **Easy recording** - One-click start/stop
- **Preview** - Listen before sending

### Other Productivity Tools

- **Multimedia attachments** - Images, videos, documents
- **PFX attachment support** - Upload `.pfx` certificates with proper type recognition and iconography
- **Emojis and GIFs** - More personal communication
- **Reply-to** - Respond to specific messages
- **Draft messages** - Automatically saves drafts as you type, restored when returning to the conversation
- **Resizable reply editor** - Manually adjust the reply box height for better handling of long conversations
- **Edit sent messages** - Correct messages after sending (provider dependent)
- **Delete sent messages** - Delete messages for everyone (provider dependent)

### Pinned Conversations

Keep important conversations at the top of your list:

- **Pin conversations** - Pin any conversation to the top
- **Unpin anytime** - Remove pin when no longer needed
- **Per-agent pins** - Each agent has their own pinned list
- **Visual indicator** - Pinned conversations are clearly marked

### Custom Filters (Folders)

Save your frequently used filters for quick access:

- **Create folders** - Save filter combinations as custom folders
- **Conversation filters** - Filter conversations by any criteria
- **Contact filters** - Filter contacts by attributes
- **Quick access** - One-click to apply saved filters
- **Edit and delete** - Manage your folders easily
- **Per-user limits** - Each user can create multiple folders
- **Consistent multi-label behavior** - Normalized values for filters that include multiple labels

### Auto-Resolution

- **Auto-resolve** - Automatically close inactive conversations
- **Configurable timers** - Define times per inbox
- **Orphan conversation cleanup** - Automatically remove conversations without associated contact

### Bulk Actions

Perform mass operations on multiple conversations simultaneously:

- **Bulk resolve** - Close multiple conversations at once
- **Bulk reopen** - Reopen resolved conversations
- **Bulk snooze** - Apply snooze to multiple conversations
- **Bulk read state** - Mark selected conversations as read or unread, including large selections
- **Bulk assign** - Assign agent or team to multiple chats
- **Bulk label** - Apply labels massively
- **Keyboard shortcuts** - Execute bulk actions with hotkeys

### Contact Actions (Bulk)

- **Merge contacts** - Combine duplicate contacts
- **Label contacts** - Apply labels to multiple contacts
- **Delete contacts** - Mass deletion with confirmation

### Command Bar

Quick access to any action via keyboard:

- **Quick activation** - Open with `Cmd/Ctrl + K`
- **Action search** - Find commands by typing
- **Navigation** - Go to conversations, contacts, settings
- **Theme change** - Light, dark, or system mode
- **Quick assignment** - Assign agents or teams
- **Status change** - Resolve, reopen, snooze
- **AI actions** - Access Captain features
- **Macro execution** - In an open conversation, choose **Execute a macro** to run the same ordered macros available in the sidebar

### Dark Mode

- **Dark theme** - Interface optimized for low-light environments
- **Light theme** - Traditional light interface
- **System mode** - Follows operating system preference
- **Adaptive widget** - Widget also supports dark mode

---

## 💬 Internal Team Communication

### Chat Rooms *(Mega)*

Internal chat rooms system for seamless team communication without leaving the platform. Perfect for coordination, quick questions, and internal discussions.

**Why Internal Chat Rooms?**

Keep your team connected and productive. Instead of using external tools like Slack or Teams for internal communication, handle everything in one place alongside customer conversations.

**Main Features:**

**Room Management (Settings):**

- **Create rooms** - Administrators can create rooms with name and description; the name retains its entered capitalization and remains unique within the account regardless of case
- **Public and private channels** - Define visibility and audience for each team workflow
- **Categories** - Group channels by topic, team, or department
- **Add users** - Multi-select team members from your account
- **Edit rooms** - Update name, description, and members from the header overflow menu
- **Delete rooms** - Remove rooms with safety confirmation
- **Room avatars** - Optional custom images for each room
- **Audio and video calls** - WebRTC communication between members in DMs, groups, and channels, with call tones and in-progress, missed, and completed call history
- **Selective call availability** - Calls require the independent `chat_room_calls` account feature, which is disabled by default and can be enabled only for selected accounts; Chat Rooms messaging remains available without it
- **Administrator-managed ICE connectivity** - Super Admin > Call ICE configures STUN/TURN and their credentials without a restart; `MEGA_CALL_*` environment variables remain compatible when no saved values exist
- **Per-account premium connectivity** - `chat_room_calls` uses Google STUN for normal P2P calls; the premium `premium_call_connectivity` feature switches that account to Call ICE and enables TURN fallback when the global configuration is complete
- **Native call experience** - Audio retains the compact WhatsApp/Twilio-style widget; video uses a bounded large workspace or floating in-app window, with simultaneous camera and screen publication, a presentation stage, participant rail, avatar fallbacks, and initiator-authorized mute for controlled small groups
- **Location** - Accessible from Settings > Chat Rooms

> **Note:** Chat Rooms settings manage channels (public and private) only. Direct messages (DMs) are personal conversations managed from the chat sidebar and do not appear, nor can they be edited/deleted, in Settings.

**Permissions & Visibility:**

- **Administrators** - See ALL account rooms in the sidebar, can create/edit/delete any channel, can participate in all rooms
- **Agents & Custom Roles** - Only see rooms where they are members in the sidebar, can only participate in their assigned rooms, cannot create/edit/delete rooms

**Chat Interface:**

- **Sidebar location** - Conversations > Rooms
- **Integrated search** - Find channels, direct messages, and messages inside rooms
- **Quick filters** - All, channels, direct messages, drafts, and archived
- **Visual sections** - Drafts, favorites, direct messages, channels, and archived
- **Quick creation** - Create channels, categories, and direct messages from the list
- **Room view** - Header with room name + message list + send input
- **Clean design** - 100% Tailwind CSS, modern and responsive

**Message Types:**

- **Text messages** - Simple text communication
- **Multimedia** - Images, videos, audio files, documents
- **Reply** - Respond to specific messages (quotes the original)
- **Reply threads** - Open a side panel per message, reply inside the thread, and optionally publish the reply back to the channel
- **Reactions** - Quickly respond to messages with emoji
- **Pinned messages** - Keep important information visible in the room
- **Polls** - Create multiple-option votes from the composer
- **Drafts** - Recover unsent text per user and room
- **Typing status** - See when other members are typing
- **Audio recording** - Integrated audio recorder for voice notes

**Smart Message Layout:**

- **Right side** - Your own messages (outgoing)
  - Different background color
  - Your avatar displayed
- **Left side** - Messages from other users (incoming)
  - Sender's avatar displayed
  - Clear sender identification

**Real-Time Notifications:**

- **WebSocket integration** - Using Action Cable for instant delivery
- **Live updates** - Messages appear immediately without refreshing
- **Room events** - Updates, deletions, read state, unread state, reactions, polls, and typing
- **Smart broadcasting** - Admins receive events from all rooms, regular users only from their rooms
- **Event tracking** - Message created and updated events

**Security & Validations:**

- **Member-only access** - Only room members can view and send messages
- **Admin controls** - Only administrators can manage rooms
- **Account validation** - Room membership is validated against account
- **Unique names** - Room names must be unique per account

**Benefits for your team:**

- No need to switch between tools for internal communication
- Context-aware discussions without leaving customer view
- Organized communication by topic or department
- Complete message history and searchable archive
- Secure, permission-based access control

---

## 🤖 Automation & AI

### Automation Rules

Configure automatic flows based on events and conditions:

- **Wait-based rules** - Run actions after 10 minutes to 30 days while a conversation remains in a selected status, a customer has not replied, or a teammate has not replied. They can combine additional conditions with `AND`; a reply, status change, or condition mismatch cancels the pending run.

**Available events:**

- Conversation created
- Conversation updated
- Message received
- Message created

**Conditions:**

- Status, inbox, labels, language
- Country, browser, email
- Custom attributes
- Message content
- Private note (internal message)

**Actions:**

- Send automatic message
- Assign agent/team
- Assign last responding agent
- Remove agent/team assignment
- Add/remove labels
- Change status or priority
- Send webhook
- Send transcript by email
- Mute conversation
- Redistribute to online agents

### Flow Builder *(Mega)*

Design automated conversations with blocks that show what the customer will receive, ManyChat style.

- **Cards with a preview** - Each block shows its real content on the canvas: the text with variables as tags, attachments, template and one button per row
- **Side panel editing** - Clicking a block edits it in a panel on the right without hiding the flow; with nothing selected, the panel shows the searchable block library
- **Options with their own output** - Send message takes up to 10 options; each one opens its own path and the customer can reply with the option number or text. A reply that matches none goes through "Other reply"
- **If the reply is not valid** - A message with options can ask again when the customer replies with something that is not an option (text, image, audio or a location that was not requested): it sends its own message, optionally sends the options again and waits once more, 1 to 5 times; then it goes on through "Other reply". The invalid reply is not saved in the contact field
- **Going back to a block** - A path can come back to an earlier block (the menu, for example) with a connection or the "Go back to a step of this flow" block, which picks the step from a searchable list and highlights it on the canvas, as long as it goes through a message that waits for the customer's reply; so the flow never repeats on its own
- **Three ways to send the message** - The top of the panel picks "Text", "Interactive" or "Template". "Text" (the default, on any channel) writes the options under the message as "🔷 1 - Medical offices", with the bullet and numbering ("1 -", "1." or "1)") you choose. "Interactive" uses the same format and fields as the conversation's interactive message form, with all its types: reply buttons, list, link, action buttons, location request, carousel, poll, Pix, order, payment request, event, location and the Call on WhatsApp button (Direct Send), with the text or file header and the footer each provider offers. It only shows, and only with its provider's types, where any of the start block's inboxes can send interactive messages (WhatsApp Cloud, or WAHA/UazAPI with interactive messages on for the server, the account and the inbox); with every inbox, while any of them can. Buttons, rows, carousel quick replies and poll answers open one path each (the poll goes on with the customer's first vote), the location request leaves by "Location received" and the types that expect no answer go on right away. An interactive block on an inbox without interactive messages is flagged in the panel and on the card ("Will be sent as text", with "Switch to text") and goes out as text with the header in bold, the options, the footer and the header file. "Template" shows where the reply box offers templates on any of the start block's inboxes (the inbox's Meta templates or Twilio content templates); when several offer them, the inbox is picked first. Pick the approved template, the header file, the variables and the button parameters, and each template quick reply opens its own path
- **The bot waits for the reply** - The flow stops at the message and continues when the customer answers; it can save the answer to a contact custom attribute
- **No reply** - If the customer does not answer within the chosen time, the flow continues through the "No reply" output
- **The same variables as the rest of the platform** - "+ Variable" offers the variables of campaigns, canned responses and the reply box (`{{contact.first_name}}`, `{{contact.phone}}`, `{{agent.name}}`, `{{inbox.name}}`, custom attributes) with the same values, plus the flow's own data (last message). They work in the text, the options, every interactive field and the template variables
- **Live preview** - The top of the panel shows the message as the customer gets it (text with options, interactive bubble or template) with sample values for the variables, and on phones each section opens in its own screen
- **Record audio** - The block records a voice note with the reply box recorder and lets you listen to it, record it again or remove it. When the block also has text, the voice note goes first and the text with its options in a separate message
- **Test as a chat** - Simulates the conversation in the panel by tapping the buttons and choosing each condition's path; nothing is sent to the customer. The test against a real conversation stays in the menu
- **Blocks** - Send message, Condition, By value, Wait, Random split, Loop over a list, Go back to a step of this flow, Start another flow, HTTP request, Actions, Kanban, Find cards, Task, Event, Alert the team, Transfer to an agent, Reply with Captain, End flow and, under Advanced, Code. End flow ends the flow without resolving the conversation: to resolve it, put the Resolve action before it
- **Readable conditions** - They read as a sentence ("If the conversation labels include vip") and combine several rules with All or Any, with Yes and No outputs. The field says what it belongs to ("Conversation · Status", and custom attributes say whether they are the contact's or the conversation's) and the value is picked from a list of real data: statuses, priorities, the account's labels, teams, agents, funnel stages with their color and the options of list attributes; free text (or a variable) is left for text fields, and the operators follow the field. They can also ask whether the inbox is in its working hours, how many agents are online (in the inbox or in a team), which tasks the conversation has, which funnel and stage, status or labels the card has, and whether the last message has an attachment
- **Actions in order** - An Actions block tidies up the conversation with one or more Automation actions (assign, label, priority, status, notes, apply an SLA when the account has SLA on, email teams, participants, webhook), top to bottom. Kanban, sending messages or files and replying to comments now have blocks of their own: saved rows keep running and, when they are the block's only action, the panel offers to convert them. When an action fails, the others still run and the block leaves by "If an action fails" when that output is connected; searching "wait" or "status" in the picker points to the Wait block and the status actions
- **Wait** - Pauses the flow for minutes, hours or days before continuing
- **Random split** - Splits contacts across paths by percentage
- **By value** - Compares one value (variables allowed) with several cases in order, with the same fields, value lists and operators as Condition, and goes on by the first one that matches or by "None matches"; each case can have a name and be reordered, and its outputs show the name of the team, agent or stage
- **Old blocks that keep running** - Business hours, Agents available, Kanban stage and Has an open task? are now rows of the Condition; Update task and Reschedule or cancel event, options of Task and Event; and Post in the internal chat, the Chat room option of Alert the team. They are no longer in the library, but the flows that use them keep running the same. In the panel, "Turn into a Condition" (or into a Task, an Event or Alert the team) moves them to the new block keeping their connections; nothing is converted on its own
- **Loop over a list** - Repeats a path for each item of a list (a variable that holds a list, or text separated by commas or lines), with the current item, its number and the total as variables in messages, fields and conditions; the path comes back to the block and, when the list ends, goes on by "Done". The panel offers the lists of the blocks before it (the cards of Find cards, the Stripe subscriptions or invoices) and the conversation labels. Up to 25 items per pass, also in "Test"
- **Code (JavaScript)** - In the Advanced group of the library, runs JavaScript on the flow data (contact, conversation, last message, inbox, agent, list item and earlier results) and keeps the object it returns under a name (for example `codigo1`), read later as `{{ vars.codigo1.key }}` in messages, fields and conditions. It runs isolated, with no network, files or timers, within 1 second, 32 MB, 10,000 characters and a 32 KB result; a failure goes on by "Error". In "Test" you choose whether it worked and type a sample result. It shows only when the server has the JavaScript runtime installed
- **HTTP request** - Calls an API: you first pick the method (GET, POST, PUT, PATCH or DELETE) and the URL, then, when needed, a saved credential, query parameters, headers and a JSON or text body, all with variables. It keeps the answer under a name (for example `respuesta1`), read later as `{{ vars.respuesta1.status }}` or `{{ vars.respuesta1.body.field }}`; after "Test request", the next blocks can pick the fields of the answer. It goes on by "Success" on a 2xx answer and by "Error" otherwise. Private network addresses are blocked, it waits up to 30 seconds and accepts answers up to 1 MB. "Test request" sends it right away with sample data; flow test runs send GET requests only
- **Connections** - Keep an API's base URL, authentication (Bearer, Basic or API key) and headers once, for any HTTP request block. Secrets are stored encrypted and never shown again; only administrators manage them, from Flow Builder or from the block itself. A connection a flow uses cannot be deleted
- **Answers kept out of the history** - With "Don't keep the answer in the history", the next blocks read an HTTP request's answer during the run and, when it ends, its body is stored as [redacted] in the execution history. The installation can also set how many days finished executions are kept (forever by default)
- **Reply with Captain** - Hands the conversation to the inbox's Captain assistant and the flow ends; the panel warns when an inbox of the start has no assistant
- **Transfer to an agent** - In "To whom?" you choose whether the conversation goes to the inbox (with its assignment rules), to a team or to an agent of the inbox. With "End the flow", on for new blocks, the flow ends there; off, it goes on after the transfer. Blocks saved before keep working as they were
- **Kanban** - Creates the conversation's card, moves it to a stage (running the stage automations), marks it won, lost or open or deletes it; it also assigns an agent to it, adds a note and adds, removes or replaces its labels. "Which card?" picks the conversation's card (optionally the one it has in a funnel, a stage, a status or with some labels), the card that started the flow, the card of the loop or, as an advanced option, another card from a variable; without a card it leaves by "No card". Inside a loop, deleting asks for confirmation. Offered only with Kanban active
- **Find cards** - Finds the account's cards by funnel, stage, status, labels, hours in the stage or a recent status change, up to 100 (20 by default), the ones longest in their stage first, and goes on by "Cards found" or "No cards". With Loop over a list each card is worked on; it needs no conversation, so it fits a Scheduled flow
- **Start another flow** - Starts another published flow of the account in the conversation of a card (the loop's, for example) or in this one, with input data the other flow reads as `{{ inputs.key }}`, and goes on without waiting. The called flow begins at the block after its start, without looking at that start's conditions. The executions say whether the other flow was requested, skipped (there was no conversation or the card was not found) or refused because too many flows were already calling each other
- **Yes/No question to Captain** - In the Captain and AI group, Captain answers Yes or No to a question reading the last message and the conversation; it uses Captain credits and has its own output when it cannot answer. "Try" never asks the AI: the tester picks the branch
- **Update contact or conversation** - Changes the contact's name, email, phone and custom attributes, or the conversation's custom attributes, with variables
- **Run macro** - Runs a public macro as the agent who created it; "Create macro" opens Settings → Macros in another tab and the list reloads on return
- **Task and Event** - Task creates an activity (due time and priority, optionally linked to the card) or completes, cancels or reopens one; Event schedules a calendar event (duration and, with Google Calendar connected, a Meet link) after a while, on a fixed date or on a date from a variable, or reschedules or cancels it. What they create remembers the flow, so a block of a later run finds the task or event this flow left on the conversation; when there is none, it leaves by "Not found". They are created for a Responsible: the conversation assignee, a fixed agent or a rotation over a team or a list of agents (optionally online only), with a fallback agent
- **Schedule message** - Schedules a message of the conversation, with files and variables, for after a while or for a date and time with its time zone (picked in the calendar or taken from a variable), once or repeating as in Scheduled messages. It is sent in the name of the chosen agent (the conversation assignee, a fixed agent or a rotation, with a fallback) and shows in Scheduled messages, where the team can edit or cancel it. When the date does not work or the message cannot be scheduled, it leaves by "Error" when that output is connected. Needs the scheduled messages feature
- **Cancel scheduled messages** - Cancels the scheduled messages of the conversation not sent yet, the repeating ones included: "Only this flow's" (how new blocks start) or "Every pending one", including the ones agents scheduled by hand. It goes on by "Cancelled" or by "None pending". Needs the scheduled messages feature
- **Ask for CSAT** - Sends the inbox satisfaction survey with its own rules (resolved conversation, CSAT on, once per conversation, template or reply window) and goes on by "Sent" or by "Not sent" with the reason, which a Condition can read. With "Resolve first", it first resolves the conversation when it is not resolved yet. Offered only when the flow's inbox has CSAT on
- **Add participant** - Action of the Actions block: adds an agent as a participant of the conversation, as the participants panel does (the agent gets its notification); an agent without access to the inbox is recorded as an error and the other actions go on
- **Contact note** - Action of the Actions block: adds a note to the contact, as the contact notes panel does, with flow and platform variables; a text that comes out empty is recorded as an error and the other actions go on
- **Link company** - Finds the company by its domain (or by its exact name without one), creates it when it does not exist and links the contact to it, as the company contacts panel does; the domain may come from a website or an email, with variables. Goes on by "Found" or "Created". Offered only when the account has Companies on
- **Find contact** - Looks for another contact of the account by email, phone, identifier or a custom attribute (fixed value or with variables), with the same rules as the Contacts filter. Goes on by "Found", with its data in the "Results" group of the variable picker, or by "Not found"
- **Card checklist** - The Kanban block adds an item to the card's checklist or marks done the first open item with that text, as the card checklist does, with variables; the panel offers the items the funnels' stages add to their cards. Without a card it leaves by "No card"; without such an item the flow goes on. Offered only with Kanban active
- **Choose an option with AI** - Captain reads the last message and the conversation and picks one of 2 to 10 options described in plain words; each option has its own output, plus "None" and "Could not answer" (also without credits). It uses Captain credits; "Try" never asks the AI: the tester picks the option
- **Suggest labels or priority with AI** - Captain reads the conversation and, like the sidebar suggestions, picks up to 3 conversation or contact labels, or the priority; the flow applies them and goes on, or leaves by "Could not answer" (also without credits). "Try" never asks the AI
- **Summarize conversation** - Captain writes a summary of the conversation (like the editor's Summarize option) that the next blocks read as a variable under "Results" and, when on, adds it as a private note; it leaves by "Could not answer" without credits or when Captain fails. "Try" uses a sample summary
- **Translate** - Captain translates a text with variables (for example the last message) into the chosen language or into the contact's language (the one detected for the conversation), as a message's Translate action does, and the next blocks read the translation under "Results"; it leaves by "Could not answer" without credits or when Captain fails. It shows only when auto translate is on and Captain is the account's translation service. "Try" uses a sample translation
- **Captain tool** - Calls one of Captain's custom tools (its address, authentication and templates) with fixed or variable parameters and leaves the answer under "Results"; it goes on by "Success" or "Error". The panel marks the required parameters and their type, and when one is left empty the tool is not called and the block leaves by "Error". Only in inboxes with a Captain assistant; tools that are off, need a verified email or are high risk are not offered. Test runs and "Try" never call it: the tester types a sample answer
- **Extract contact data with AI** - Captain reads the contact and the conversation with the inbox's assistant, as its memory does: in Attributes mode it suggests the details the conversation mentions and the contact does not have yet, which the next blocks read under "Results"; you can limit them to a closed list of attributes and, with "Save to the contact", write them to the contact; in Notes mode it writes contact notes. It leaves by "Could not answer" without credits, without an assistant or when Captain fails. "Try" never asks the AI
- **Look up customer in Stripe** - With Stripe connected in Integrations, finds the contact's email in the account's Stripe, as the conversation sidebar does, and the next blocks read the customer's name, email, phone, id and latest subscription status under "Results"; it leaves by "Found", "Not found" (no email or no customer) or "Error" (Stripe failed or the key must be reconnected). Test runs and "Try" never call Stripe
- **Hand over to Typebot / Dialogflow** - The conversation goes to one of the account's Typebot bots (assigned as an agent assigns a bot, pending, with the customer's message) or to the Dialogflow agent connected to the inbox (left pending, with the customer's message), and the flow ends: the bot answers from there. Shows only the bots the account has on, and the panel names the inboxes of the start that have no Dialogflow. Test runs and "Try" change nothing
- **Alert the team** - In "How to alert?" you pick Notification or Chat room. Notification sends an agent (the conversation's assignee by default, a chosen agent or a rotation, with a fallback) a notice about the conversation with a text with variables: it shows in their notifications and goes out by push and email as their notification settings say ("A flow sends you a notice" preference, push on by default); the agent must be able to see the conversation, otherwise the step fails. Chat room posts the message in one of the account's chat rooms in the name of that agent, who must be a member of the room. The flow goes on right after. Test runs and "Try" alert nobody
- **Dyte video call** - Starts a Dyte video call in the conversation as the reply box's video call button does, in the name of an agent (the conversation's assignee by default), and leaves by "Error" when Dyte cannot create it. Only in website and API inboxes with Dyte connected; the panel names the inboxes of the start where it does not work. Test runs and "Try" create no meeting
- **Read account data (advanced)** - Reads what no variable or other block gives (a contact's conversations and notes, a conversation, its messages with their type, sender and whether they are private, labels, canned responses or a company search) in the name of a chosen agent who can use the Mega assistant, and the next blocks read its answer under "Results". In "Which contact?" or "Which conversation?" you pick the flow's one or a variable, without typing ids. Nothing is changed or deleted, and blocks saved with other reads keep running. Only administrators edit flows. Test runs and "Try" run nothing
- **Only available blocks** - The library shows only the blocks whose feature is on for the account (Kanban, activities, calendar, macros, Captain); if a feature is turned off later the block warns in its panel and its step fails without repeating earlier steps
- **24-hour window** - Outside the WhatsApp customer service window (and Messenger's and Instagram's) a message that is not a template is not sent: the block leaves by "Window closed" when it is connected, otherwise the flow ends there
- **Once per conversation** - An event start can be limited so the flow does not start again with every message (on for new flows); in Agent bot mode the flow answers every message
- **Pauses when a person steps in** - If an agent replies or the conversation is resolved, the waiting flow is cancelled
- **Arrange** - Lays the flow out automatically from left to right
- **On the phone** - The flow reads as a list of steps grouped by button or condition, and each block is edited in a bottom sheet
- **Drafts and versioned publishing** - Edit without affecting the published version; waiting conversations keep the version they started with
- **Switch to activate and pause** - Activate or pause published flows from the list or the editor; pausing cancels the conversations that were waiting
- **Validation before publishing** - Detects cycles that neither wait for the customer's reply nor are the way back of Loop over a list, broken connections, buttons over 20 characters, splits that do not add up to 100 and incomplete blocks. The warning names the block and "Show block" opens it; blocks with warnings are marked on the canvas. An output connected to two blocks is an error (only the first one would be followed); connecting an output that already has a destination moves the connection to the new block. It warns about blocks no path from the start reaches (counting Go to block). An unconnected "Other reply" on a message with text options, or "No reply" on a message with a wait time, is only a suggestion on the block itself
- **Four kinds of start** - The Start is an Event (it begins when something happens: a message, a change in the conversation, a comment or an updated card), an Agent bot (the flow is the bot of its inboxes and answers every message until it hands the conversation to the team), Scheduled (it runs at the times you choose, without a conversation) or Webhook (it runs when an external CRM or form sends data to the flow's own URL). Each kind is explained in one line with an example, and fine filters go in a Condition after the start
- **Scheduled start** - Runs every so many minutes (from 5), hours, days or weeks at a time, or on a cron expression, in the account's reports time zone, and shows its next runs while you set it up. A slot that did not run (the server was down or the previous run was still going) is not caught up, but it is recorded in Executions. Since there is no conversation, it uses blocks that do not need one, such as HTTP request, Code, Condition, By value, Loop over a list, Find cards, Kanban on a chosen card, Start another flow and Read account data. E.g. every working day at 9:00, find the cards won yesterday and start a follow-up flow for each one
- **Webhook start** - The flow gets its own URL with a secret (in the URL or in a header) that you can copy, see with a ready-to-use `curl` example and replace whenever you want. An external CRM or form sends any JSON or form fields, gets an answer at once and the flow runs in the background; the data it sent is available in expression fields, e.g. `{{ webhook.body.phone }}`. An optional idempotency key (e.g. phone + email) keeps the same lead, sent twice, from running the flow twice. Every call shows in Executions with the body it received, so you can see what failed
- **Outbound message** - Picks the inbox, finds or creates the contact by phone (with and without Brazil's 9th digit; on WAHA it resolves the `@lid`), opens the conversation and sends a text or a template. From there on the flow works on that conversation, so every other block can follow it (labels, assignment, waiting for the reply). Until it runs, a Webhook or Scheduled flow only uses the blocks that need no conversation. E.g. a lead arrives from the CRM, the flow greets them on WhatsApp and hands the conversation to the sales team
- **Card updated** - The flow starts in the card's conversation when the card is created, moves to another stage or funnel, or goes won, lost or open, and `{{ kanban.change }}` says what changed. A card without a conversation starts nothing. To go on only for a funnel, a stage or a status, put a Condition after the start
- **Message sent by the team** - The flow starts when an agent sends a public message (not a bot, another flow or a campaign) and the blocks read that message in `{{ message.* }}`; it never continues a flow waiting for a reply
- **Changes made by other flows** - With "Starts on changes made by other flows", the start also answers when another flow changes the conversation or a card. Never on its own changes, and a chain of flows stops after 3 hops
- **One run at a time per contact** - When the flow is already running for that contact, the new start waits its turn (about one minute at most). A start that never gets to run stays in Executions as an error with its reason, and a reply or a timer that was waiting is never lost
- **AgentBot-style start** - The start can be bound to one or more inboxes to serve them as a native bot, exclusive against AgentBot, Dialogflow or other active flows in each of them. Major can share the inbox with the flow: the flow answers first and its "Reply with Captain" block hands the conversation to Major; new conversations on that inbox are not assigned to Major
- **Ignore contacts** - The start can leave out WhatsApp groups and specific contacts, searched by name, phone or email: the flow does not start for them and, when it serves the inbox as a bot, the conversation stays open for the agents.
- **Event start on some inboxes** - An event start runs on every inbox or only on the ones picked; "Test" uses a conversation from one of them
- **Flow as an AgentBot** - In AgentBot mode the flow acts as a platform Agent Bot: it has its own bot, named after the flow, and the conversations it takes stay pending and assigned to that bot, without taking over conversations already assigned to a person. Its messages go out as that bot, and the "Transfer to an agent" block hands the conversation over to the team the same way an Agent Bot handoff does. The bot does not show in Settings → Bots or in bot pickers, and it stays as the history of what the flow did after the flow is paused, switched to events or deleted
- **Live visual execution history** - Replays each execution on the canvas, marks blocks as success, error or waiting, and opens each block to review input, output and errors
- **Wider panel and compact library** - A wider, clearer side panel: the library shows blocks in two columns with group filters (the description shows at the bottom on hover), and every block says in one sentence what it does and where each output leads. The Actions block searches and groups actions inside the same panel
- **Test with the path** - Test shows your flow as a WhatsApp chat. Each step is marked between the messages and the path is drawn on the canvas. Wherever the flow would decide with real data, you choose the way
- **Flow list** - The flow list follows the settings pages: click any row to open the flow and see at a glance its status, what triggers it, which inbox it runs in, how many blocks it has and how often it ran today. On phones, rows are larger and a floating button creates a flow
- **Executions** - Every run shows on the same cards as the editor: which blocks ran, how long they took and which output the flow followed. Filter by failed or waiting runs and read each step in plain language, with the technical data one tap away. Nothing is lost silently: a start that could not run and a scheduled slot that did not run stay as failed executions ("Did not start") that say why, and skipped steps show apart from the failed ones. Through the API and the MCP, every execution says why it stopped, which steps failed or were skipped, and which flow started it or which flows it started
- **Comment received** - A start runs the flow on every Facebook or Instagram comment; the same comment never starts the flow twice. To answer only some of them (a platform, a post, some words, no replies), add a Condition after the start with the Comment fields; a start that saved those filters keeps applying them until you click "Move to a Condition". The comment blocks reply publicly, send the private reply (one per comment, within 7 days), hide or delete the comment, and messages read `{{comment.text}}`, `{{comment.platform}}`, `{{comment.permalink}}`, `{{comment.post_caption}}`, `{{comment.is_ad}}` and `{{comment.username}}`. Send message sends a direct message with its 24-hour window, which a comment does not open
- **Comments in "Message received" and in bots** - The "Message received" and AgentBot starts add the "Include post comments (Facebook/Instagram)" option so comments also start the flow. It turns on by itself when a flow that uses the Type condition, a comment block or action, or a Send message block that replies to the comment is saved or published, and it never turns off by itself. Each comment starts the flow only once: "once per conversation" still applies only to direct messages. A comment never continues a flow that is waiting for a reply
- **Type condition** - In the Condition block, the "Last message" group adds "Type" (`{{ message.kind }}`), which tells a direct message (`direct_message`) from a comment (`comment`); the value is picked from a list
- **Comment blocks** - The library adds the "Comments (Facebook and Instagram)" group with "Reply to comment", "Private message to the comment", "Hide comment" and "Delete comment", each ready to use
- **Send as** - Send message blocks saved as "Public reply to the comment" or "Private message to the comment" keep running (text with variables only, not tied to the 24-hour window; if the run did not start with a comment, they go on by the normal output without sending) and the panel offers "Turn into a comment block". New blocks send a direct message; comments are answered with the Comment blocks, and the panel warns when one is in a flow whose start receives no comments
- **API, MCP and Mega Assistant** - Administrators can manage flows outside the editor: every Flow Builder endpoint is in the API docs (Swagger/OpenAPI and the Postman collection, with examples, from Super Admin → API Docs), and the account MCP server and Mega Assistant can list, create, edit, check, test, publish and pause flows, see their runs and manage connections. To build a flow from scratch they read a reference with the settings, outputs and an example of each block. Only when Flow Builder is on for the account and only for administrators

### Macros

Execute multiple actions with a single click:

- **Personal macros** - Visible only to you
- **Global macros** - Available to entire team
- **Chained actions** - Combine multiple operations
- **Reply editor shortcut** - Type `#` to search, preview, and run macros without leaving the conversation
- **Command bar shortcut** - Open `Cmd/Ctrl + K` in a conversation to select the same ordered macro; required attributes use the shared resolution dialog
- **Bulk macros** - Select several conversations in the list and run one macro on all of them from the selection bar (on phones, **More** → **Execute macro**), after a confirmation

### Agent Bots

- **Webhook bots** - Connect with external logic via HTTP
- **Typebot integration** - Connect with Typebot conversational flows
- **Human handover** - Smooth transfer to real agents
- **Smart handover** - If a human replies in a pending bot conversation, ownership is transferred automatically
- **Human replies on the webhook** *(Mega)* - Optional per Webhook bot: also receive the agent's replies, from the dashboard or from the phone on WhatsApp, so the bot keeps the context of the human service. Off by default
- **Expiry handover** - When a Webhook session expires, the conversation opens, releases the bot, and attempts automatic assignment to an eligible agent; if nobody is available, it stays open and unassigned
- **Bots per inbox** - Configure specific bots per channel
- **Explicit bot ownership** - Conversations handled by a connected Agent Bot stay pending and assigned to that bot; a human open, handover, or bot disconnection releases bot ownership without replacing explicit human assignments
- **Bot stays quiet after the handover** - A Webhook Agent Bot only receives the customer's messages while the conversation is pending (or assigned to it); once it is handed over to the team the bot stops getting them, so it cannot keep answering a conversation a person already took. It still learns when the conversation is opened, resolved or changes status, but not the team's edits such as labels or assignee, and bots set to receive human replies keep following the whole conversation
- **Human unassigned queue** - Conversations assigned to an Agent Bot do not appear in the Unassigned queue; it contains only conversations without a human or bot assignee
- **Dashboard takeover** - While an Agent Bot handles a pending conversation, the composer stays in private-note mode and provides an action to take over, reopen the conversation, and assign it to the current agent
- **Inbox-scoped manual assignment** - The agent selector only offers active Agent Bots configured on the conversation inbox
- **Typing indicator** - Bots can toggle the "typing..." indicator for a more natural experience
- **Advanced webhook options** *(Enterprise)* - Configure custom timeout for bot requests, automatic retries on failure, and granular error handling; improves reliability for integrations with slow or unstable external systems
- **Per-channel webhook signatures** - Sign outgoing events for Agent Bots and API Channel inboxes to validate authenticity end-to-end

### Typebot *(Mega — Advanced Options)*

Beyond the standard Typebot integration, MEGA extends its capabilities with special commands:

- **Agent assignment via MEGA_CMD** - Use the `MEGA_CMD:assign_agent:email@company.com` command in Typebot to automatically assign the conversation to a specific agent
- **Team assignment via MEGA_CMD** - Use `MEGA_CMD:assign_team:team_name` to route the conversation to the appropriate team from within the bot flow
- **List placeholders** - Inject dynamic lists of agents or teams as Typebot variables to build custom selection menus
- **Media-only first message handling** - Correctly opens a new conversation when the first interaction is media-only
- **Ignored WhatsApp reactions** - Reactions do not start the flow or get sent to Typebot as messages
- **Location compatibility** - Forwards coordinates as map links for consistent bot flow handling
- **Stable default delay** - More predictable behavior when no explicit delay is configured in the bot
- **No extra code** - Everything is configured directly in the Typebot flow, without modifying the MEGA bot

### Captain *(Enterprise)*

- **AI assistant name with your brand** - Captain shows as **Major** by default, and each installation can give it its own name from Super Admin (Settings → Captain). The name appears across the dashboard, in the MCP server for any connected AI and in Mega Assistant, without changing existing integrations, APIs or tools.
- **Safer Captain replies and takeover** - Captain no longer sends customers raw tool text: it retries once and, if the reply is still wrong, hands off to a human without charging a credit. Agents can take over Captain conversations in one click and stay assigned, without auto-assignment handing them to someone else.
- **Conversation and contact label and priority suggestions** - Captain suggests up to three existing labels for the conversation or contact, and a priority from recent public messages. Agents can accept or dismiss suggestions; requesting them again generates a new model response. The sidebar identifies a recommended priority that is already applied; accepting labels clears the previous suggestion. Enable `captain_classifier` for the account and select the conversation classification model in the Captain account or plan settings; the call does not consume Captain response credits. It runs on the Captain Decision Router: classification can use a decision model such as Jev (through OpenRouter), which answers with probabilities in milliseconds at a very low cost, or any chat model (OpenAI, Anthropic, Gemini or compatible).
- **Smart routing for Captain and Mega Assistant** - The Captain Decision Router can pick the Captain scenario that handles each message, the most useful custom tools when there are many, and, in Mega Assistant, the guides a request needs and whether it needs the complex-tasks model. It understands the request even when the exact words are not used, and decides again on every message: when the customer changes topic, the conversation moves to the matching scenario instead of staying with the first one that answered. Set it up in the Captain Decision Router section of each account in Super Admin: pick a model (for example Jev or any chat model) and a mode, Measure only to compare without changing replies or Active to apply it; when off or without a model the keyword rules stay in place.

Advanced AI assistant powered by large language models for intelligent customer service automation.

**Captain Assistants:**

- **Provider capabilities** - Super administrators declare models for chat, embeddings, audio transcription, and PDF/documents per provider. Gemini supports all four native paths and Anthropic supports chat and PDF/documents; OpenAI-compatible endpoints are selectable only for explicitly configured capabilities. The Decisions capability marks models that answer on the System One API (for example `typesafe/jev-1.13` on OpenRouter).

Create and configure AI assistants tailored to your business needs:

- **Multiple assistants** - Create different assistants for different purposes
- **Custom configuration** - Set temperature, model, and behavior parameters
- **Per-feature models** - Configure separate models for Assistant, Copilot, suggestions, and FAQ generation from documents and PDFs
- **Copilot history and credit alerts** - Copilot keeps your past chats so you can reopen them, and administrators get an email when most of the month's AI Actions are used
- **Captain conditions in automations** - Describe in plain words what a rule should detect ("the customer wants to cancel") and Captain checks each conversation or message against it; each check is charged the AI Actions of its model, and only when the answer matters
- **Provider defaults** - Super administrators securely configure OpenAI, Anthropic, and Gemini, choose Captain's default provider/model, and each account can inherit it or select an available model per feature; Captain inherits compatible options saved for the selected model
- **Internal model routing** - Super administrators can separately configure the inactive-conversation evaluator; account overrides take precedence over the self-hosted installation model, while customer Captain preferences keep internal features hidden
- **Conversation FAQ suggestions** - Resolved conversations with reusable human-agent answers are grouped into reviewable FAQ suggestions; agents can review only suggestions and source conversations they can access, while they can edit, approve, or dismiss open suggestions to publish trusted FAQs
- **Knowledge training** - Train assistants with your business documents
- **Inbox assignment** - Link assistants to specific channels
- **Custom avatar** - Upload an image for each assistant, shown next to its replies in the chat widget; removing it brings back the default logo
- **Settings for administrators** - Assistant settings and scenario pages open only for administrators; agents keep working with Major in their conversations
- **Manual conversation assignment** - Accounts with Captain enabled can select the assistant configured for the conversation inbox; assigning it leaves the conversation pending, while removing it or assigning a human reopens the conversation. Reopening a conversation (by hand, in bulk, with a macro or when a snooze ends) takes it away from Major, and a macro or automation that assigns an agent opens it like a direct assignment. Major only takes and answers conversations while the account has Captain enabled
- **One bot per inbox** - Each inbox is answered by a single bot provider: an Agent Bot, Dialogflow, a Flow Builder flow in AgentBot mode, or Major. Connecting a second one is refused with a message saying which one to disconnect first; inboxes that already had two keep working. The exception is a flow with Major: the flow answers first and its "Reply with Captain" block hands the conversation to Major. Major does not respond or schedule automatic resolution for inboxes with an Agent Bot or Dialogflow
- **Assistant overview** - The Captain overview combines rotating period insights with outcome metrics, resolution flow and trend comparisons, Captain CSAT, runtime quality, usage and knowledge coverage; filter by day ranges, this or last week, or month, and click a metric, handoff reason or the resolution flow to see the conversations behind it (admins)
- **Generation details** - Open the “Generated by Captain” indicator on an assistant reply or handoff reason note to inspect its tool and scenario steps, knowledge-base sources, and reasoning; model and credit usage are limited to super administrators
- **Trusted citations** - Captain V2 renders only server-validated public web links, records the sources actually selected, and keeps rendered URLs out of model history; earlier sessions retain their existing source details
- **Bounded runtime** - Captain V2 limits conversation context and active capabilities per run, uses a compact semantic summary with a safe fallback when history is omitted, rejects irrelevant knowledge matches, records safe runtime metrics, and protects write tools against stale or repeated execution. Generation details expose safe per-run context and summary diagnostics; the quality panel measures summary latency and fallbacks, while configured golden cases run daily without executing tools.
- **Single runtime** - Every account with Captain runs Captain V2; the previous runtime, its false-promise check and its action classifier were retired, so assistants are configured only through scenarios, guidelines and guardrails
- **Image comprehension** - Assistant can analyze images sent in conversations
- **Multimodal support** - Process text and images simultaneously for contextual responses
- **Ignore groups** - Configure assistant to not respond in group conversations
- **Ignored targets** - Define specific conversations or contacts the assistant should skip
- **Audience and schedule** - Limit replies to contacts matching configurable conditions and choose whether the assistant responds anytime, during business hours, or outside them; conversations outside those rules go to the human queue. "Wait before replying" (up to 10 seconds) lets the assistant answer customers who split one request into several messages with a single reply
- **Inactivity resolution** - With Captain V2, each assistant chooses whether Captain reviews the conversation, always resolves it, or waits for the customer; resolving modes use a 5-minute to 24-hour timer and can send an optional closing message. The review has three outcomes: the conversation is complete, it is waiting on the customer, or it needs a human. When the next step is the customer's, Captain resolves the conversation instead of handing it off, with the closing message in the customer's language and no CSAT survey; if the customer writes again, the conversation goes back to pending and a later resolution sends the survey as usual

**Captain Documents:**

Upload documents to train your AI assistant:

- **Document upload** - Add PDFs, text files, and more (up to 10MB)
- **Automatic processing** - Documents are processed and indexed
- **Auto-sync fields** - Track sync status and last sync timestamp to keep knowledge sources aligned
- **Staggered auto-sync** - Refresh web sources by plan with distributed execution to avoid load spikes
- **Related responses** - See which responses use each document
- **Document details** - Review crawled content, source metadata, and generated FAQ
  counts
- **Conversation usage** - Administrators can see the distinct conversations that used a document or a user-created FAQ, sort documents by usage, and open the matching conversation list; handoffs and deleted conversations are excluded
- **Bulk management** - Add and remove documents easily

**Captain Scenarios:**

Configure specific scenarios and workflows:

- **Custom instructions** - Define behavior for specific situations
- **Tool assignment** - Assign specific tools per scenario
- **Status management** - Administrators can enable or disable scenarios; disabled scenarios remain available for management but are excluded from Captain execution
- **Complete MCP creation** - AI clients connected to the account MCP can save and update built-in, custom, and MCP tool IDs; unavailable IDs are explicitly rejected
- **Activation rules** - Define when each scenario applies
- **Priority ordering** - Control scenario precedence

**Captain Custom Tools:**

Create custom tools for your AI assistant:

- **Complete typed contracts** - Custom and MCP tools preserve objects, arrays, enums, and nested fields; scenarios only receive them while they are enabled and connected

- **HTTP integrations** - Connect to external APIs (GET/POST/PUT/PATCH/DELETE)
- **Authentication** - Support for Basic, Bearer, and API Key auth
- **Parameter mapping** - Define input/output parameters
- **Enable/disable** - Toggle tools on or off as needed
- **Safe disabling** - Administrators are warned before disabling a tool used by enabled scenarios; disabled tools remain visible and preserve saved scenario references without running
- **Email verification for sensitive tools** - A tool can require the customer to confirm their email with a 6-digit code before Captain uses it. Captain emails the code (sent with your inbox name), asks the customer to type it in the chat, and then runs the tool. A "verified email" parameter sends that confirmed address to your API, so nobody can look up another person's account by typing their email. New tools that change data start with the option on

**Captain MCP Servers:**

Connect MCP (Model Context Protocol) servers to expand your assistant's capabilities:

- **Native account MCP** - Create account-level MCP servers with dedicated endpoints
- **Agent-ready MCP** *(Mega)* - Every tool tells agents its module, its intent (search, read, create, send, schedule, diagnose), its effects and what it needs, and similar tools say when to use each; errors carry a stable code, whether to retry and a request id; sends and schedules take an optional idempotency key: a retry with the same key is not sent twice, while a call without one sends every time, as before (the protection is opt-in); `account_context` says what the server can do and why not; Flow Builder runs and flows can be read without the whole graph (a 10-step run: 151 KB to 1.7 KB). All additive: existing clients keep working unchanged
- **Secure and flexible access** - Supports OAuth authentication and static token access
- **Files from any AI provider** - ChatGPT discovers its native picker; Claude and other clients can use a temporary HTTPS URL, base64, multipart, or a signed ID without requiring a permanent public URL
- **Authenticated direct uploads** - JSON MCP clients can request signed upload targets through the API without browser CSRF
- **Universal outbound over MCP** - Start text, media, or templates for phone, email, contact, or provider identity; direct files also work in template media headers, and invalid media references are rejected before delivery
- **Daily-use catalog** - Publishes tools ready for everyday account operations
- **Expanded operational coverage** - Includes scheduling, tasks, campaigns, SLA, calendar, reports, notifications, and internal chat; does not expose data import or export
- **Help Center over MCP** - Query, search, and retrieve articles and categories from connected agents
- **Assistant assignment** - Link MCP servers to specific assistants
- **Captain-attributed native actions** - Signed native MCP executions preserve the assistant sender and confirm delivered messages without duplicates or unintended handoff
- **Production-faithful Playground** - The catalog remains available for scenario configuration. With Captain V2, the playground tests real handoffs and loads only the scenario's assigned tools; the legacy flow tests the base assistant without direct selection
- **Playground test setup** - Try saved (even disabled) or temporary scenarios, response guidelines, guardrails and up to 10,000 characters of pasted knowledge in the Playground without changing the assistant; administrators can save a temporary item or the pasted knowledge (as a Markdown document) with one click, and each reply shows who answered, the tools it called, failed calls and its duration. Playground replies use Captain credits
- **Centralized management** - Manage all your MCP servers from settings

**Captain Auto-Resolve Mode:**

Configure how Captain handles automatic conversation resolution:

- **Evaluated mode** - Captain analyzes context, including conversation status and speaker roles, and autonomously decides whether the conversation is complete, waiting on the customer (both are resolved; a close while waiting on the customer sends no CSAT survey) or needs a human (handed off); pending handoffs and promised follow-ups remain open
- **Messages in the customer's language** - When the assistant has no custom handoff or resolution message, the default text reaches the customer in the language they write in, not the account's, and an inactivity handoff also lets the customer know
- **Legacy mode** - Original behavior: automatically resolves pending conversations based on the timer
- **Disabled mode** - Captain does not automatically resolve conversations
- **Per assistant** - Each assistant saves its own policy; assistants without a saved policy retain the account setting as a compatibility fallback

**Captain Copilot:**

Real-time AI assistance for your agents:

- **Copilot threads** - Persistent conversation threads with the AI
- **Context-aware** - AI understands conversation context
- **Agent tools** - Search conversations, contacts, articles
- **Suggestions** - AI-powered response suggestions
- **Assistant-guided drafts** - When suggesting a reply, Copilot uses the selected Assistant's instructions, FAQs, citations, and GET tools; agents review and edit the draft before sending
- **Readable suggestions** - Long suggestions expand the reply editor up to 350px without overriding the size chosen manually
- **Smoother panel** - The Copilot chat follows the reply as it arrives but does not move you if you scrolled up to read; you can paste while the previous message is sending, and on phones the keyboard does not open on its own
- **Stop and expand** - A Stop button in the text box ends the reply Copilot is working on, with no AI Action charged for it; an expand button widens the panel on larger screens, and the panel also fits next to the Major overview
- **Usage limit marked as failed** - When the AI Actions run out, the Copilot notice is saved as a failed message, so integrations do not take it for an answer

**Copilot workflows *(premium, needs both the `captain_integration` and `copilot_workflows` flags)*:**

Copilot works through multi-step requests on the account's own data:

- **Multi-step work** - Copilot plans and runs several steps for one request, shows each step in the panel, and keeps working when the panel is closed; the answer is waiting when you come back
- **Dashboard reports** - Reads the same numbers the reports pages show (conversations, resolutions, first response, resolution and reply times, messages, bot resolutions and handoffs) per day, week, month or year, per agent, inbox, team or label, ranked by the metric asked for, with charts on request
- **Account directory and data** - Finds agents, inboxes, teams and labels by name, and counts, groups and filters the account's records (conversations, contacts, messages, CSAT, articles and an allowlist of other account tables); secret columns, such as tokens and credentials, and JSON keys named like secrets are left out of what Copilot reads
- **Conversation reviews in batch** - Reviews hundreds of conversations in the background against the agent's question, with a progress card, coverage (reviewed, matched, failed, remaining) and a link to every conversation it cites; numbers and links that no tool returned are checked and unknown links are removed
- **Changes behind an approval card** - Copilot proposes changes and an approval card shows what will change before anything happens; on approval each record is checked again against the approving agent's own permissions. 17 actions: set status, priority, agent, team, labels, custom attributes and SLA, add participants, private notes and replies, mute or unmute, and for contacts add labels, notes and attributes or block and unblock
- **Rich blocks under the answer** - Copilot can show tables, headline metrics, charts, cards, timelines, contact and conversation cards and follow-up buttons under its answer, drawn like Mega Assistant's; contacts and conversations appear only when the agent may open them, and a follow-up button sends its question as the agent's next message, never a change
- **Stop rejects pending approvals** - Pressing Stop ends the workflow and rejects the changes still waiting for approval; an unanswered approval expires after 5 minutes
- **Models from Super Admin** - The `copilot_workflows` model route picks the model for workflows and `copilot_screening` the model that screens conversations before a review; screening stays off until a model is routed to it

**AI Actions:**

- **Response suggestions** - AI generates suggested responses
- **Conversation summary** - Get context quickly
- **FAQ lookup** - Find relevant FAQs automatically
- **Handoff** - Smart transfer to human agents
- **Auto labeling** - AI suggests conversation labels
- **Priority updates** - AI recommends priority changes
- **Private notes** - AI can add internal notes

**Conversation Monitors** *(Enterprise/Mega)*:

Follow the topics that matter across your conversations, described in plain words:

- **Plain-language conditions** - Describe what to find (refund requests, login problems, cancellation intent...) and Captain checks every conversation against it
- **Ten templates** - Start from ready-made monitors for support, sales, product, finance and operations
- **Preview before saving** - Try a condition on up to five recent conversations
- **History and live updates** - A new monitor checks the conversations of the last seven days, then every new customer or agent message
- **Report per monitor** - Matching conversations per hour, six hours or day, with the conversations behind each bar for administrators; the report updates by itself
- **Pause and resume** - Pause without losing results; resume checking the paused period or from now
- **Automations** - The new *Monitor Matched* automation event runs actions the first time a monitor finds a conversation on new activity
- **Slack alerts** - Choose a Slack channel per monitor to get a message the first time it matches a conversation from new live activity; disconnecting Slack turns the alerts off. Alerts keep live checking on, which can use more AI Actions
- **Your model, your AI Actions** - Super Admin picks the model (a decision model such as Jev or any chat model); each checked conversation uses that model's AI Actions, and monitors wait while the account has none left
- **Where** - Settings › Captain › Monitors, also in the Captain menu; desktop and phone

**Audio Transcription:**

Automatically transcribe audio messages to text:

- **Automatic transcription** - Convert voice notes into readable text
- **Call recording controls** - Enable or disable call recording transcription by provider (WhatsApp Cloud and WaVoIP)
- **Call diarization** - Splits call recordings by speaker turn using the contact name and assigned agent name
- **Manual transcription** - Queues transcription from the context menu when an audio message still has no text
- **Major keeps answering** - If the provider rejects a voice note (an invalid file or one blocked by its content filters), Major answers without that transcript instead of retrying or going silent
- **OpenAI models** - Uses GPT-4o Mini Transcribe by default for voice notes, with Whisper available as an account override; for call recordings, normalizes audio and combines GPT-4o diarization with GPT-4o Transcribe for better fidelity
- **Multi-language** - Support for multiple languages
- **In-conversation context** - Agents can quickly read audio content

**Supported AI Providers:**

- **OpenAI** - GPT-4o, GPT-4, GPT-3.5 Turbo
- **Anthropic** - Claude (Sonnet, Opus, Haiku)
- **Google** - Gemini (Pro, Flash)
- **Azure OpenAI** - OpenAI deployments on Azure
- **Amazon Bedrock** - AWS-hosted models
- **DeepSeek** - Open-source AI models

---

## 👥 CRM & Contact Management

### Contact Profiles

- **Complete information** - Name, email, phone, location
- **Automatic avatar** - Profile photo when available
- **Last activity** - Interaction tracking
- **Contact type** - Visitor, Lead, Customer; a contact becomes a lead when it has an email, phone, identifier or WhatsApp ID, when it starts a conversation, or when it is created from the dashboard, the API or an import, and never goes back to visitor
- **Contact history in the thread** - At the start of a conversation, a pill opens the contact's previous conversation; the next one is offered on resolved conversations or while the list shows that contact. **View all conversations** in the contact panel (**History** on phones) narrows the conversation list to the contact, newest first, and the clear button returns to the full list
- **Reading mode for older conversations** - Opening a previous conversation from the thread scopes the list to the contact; older conversations open with the reply box folded into **Reply to this older conversation** (with **Go to latest conversation**), so nobody answers an old thread by mistake. Clicking the bar, a reply shortcut or any writing action opens the editor; the latest conversation keeps the normal editor, and clearing the scope returns to it

### Custom Attributes

- **Flexible fields** - Create attributes for contacts and conversations
- **Data types** - Text, number, list, date, checkbox, link
- **Automation integration** - Use attributes as conditions
- **Visibility control** *(Enterprise)* - Define which roles can see each attribute; hide sensitive fields from lower-level agents
- **Copy as shown** - Copying a date attribute copies the date as it is displayed

### Labels

- **Flexible organization** - Categorize contacts and conversations
- **Conversation labels** - Classify by topic or status
- **Quick search when assigning** - Fuzzy-filter labels from a conversation's context menu, with assigned labels shown first
- **Contact labels** - Segment your customer base
- **Custom colors** - Quick visual identification

### Companies *(Enterprise)*

- **Group contacts** - Organize contacts by company
- **Contact company selector** - Assign, clear, or create a company directly from the contact form
- **Custom-role access** - Administrators can grant the "Manage companies" permission to custom roles so they can see and manage the Companies menu
- **Auto domain** - Association by email domain
- **Unified view** - History of all company conversations
- **Automatic favicon** - The system automatically downloads the company's domain favicon to display as its avatar; works with any website that has a configured favicon
- **Company enrichment** *(premium, off by default)* - With the Company Enrichment feature and the installation's Context.dev key, a new company with a domain gets its description, industry, size, location, phone and social profiles filled in automatically (one lookup per domain); administrators can refresh it from the company page

### Notes

- **Contact notes** - Document important information
- **Internal history** - Maintain context between interactions
- **Long notes from the conversation** - The note box in the conversation contact panel has no character counter, so long notes can be written there

### Data Import

- **CSV Upload** - Import contacts massively
- **Field mapping** - Associate columns with attributes
- **Intercom and Freshdesk history import** - Administrators can import contacts, conversations, and historical messages from Intercom or Freshdesk in the background. Imports survive database connection drops (three retries with a growing wait), and Freshdesk imports use the plain-text version of each message, skipping only a single message whose HTML is too deeply nested instead of failing the import
- **Import monitoring** - Review progress, skipped records, errors, and downloadable skip logs
- **Stalled import retry** - Retry a stalled Intercom or Freshdesk import after 15 minutes without losing its progress
- **Auto validation** - Detect errors before importing
- **Controlled access** - Import and export available to administrators and contact managers
- **Safe export** - Values beginning with formula characters are exported as text to prevent their execution in spreadsheets

### Contact Blocking

- **Manual blocking** - Avoid messages from problematic contacts
- **Auto filtering** - Don't appear in main inbox
- **Active WhatsApp blocking** - Incoming WhatsApp messages from blocked contacts are dropped before opening a conversation

### Per-Contact Message Preferences *(Mega)*

- **Skip greeting** - The contact doesn't receive the inbox greeting message
- **Skip CSAT** - The contact doesn't receive the satisfaction survey when the conversation is resolved
- **Skip agent name** - Messages sent to the contact don't start with the agent name
- **Stored on the contact** - Kept across new and reopened conversations
- **Providers** - Apply to WhatsApp inboxes on Evolution, WAHA and UAZAPI; editable from the conversation panel or the contact page

### CRM V2 *(Beta)*

Enhanced contact management with improved flexibility:

- **Contacts without identifiers** - Allow contacts without email or phone number
- **Improved search** - Better contact discovery and filtering
- **Search by company** - Find contacts by company/organization name
- **Resolved contacts** - Smarter logic for identifying real contacts
- **Export compatibility** - Works with all export features
- **Infinite scroll** - Automatic loading of more contacts as you scroll
- **Smart pagination** - Indicator for more results available

---

## 📢 Mass Campaigns

Complete campaign system for proactive customer communication across multiple channels.

### Campaign Types

#### Ongoing Campaigns (Live Chat)

Proactive messages for your website visitors:

- **URL triggers** - Activate campaigns on specific pages
- **Time triggers** - Show message after X seconds on page
- **Event triggers** - Activate based on user behavior
- **Business hours** - Only trigger during work hours
- **Enable/disable** - Easily activate or pause campaigns

#### One-Off Campaigns

Mass sends to a segmented audience:

- **WhatsApp** - Campaigns via WhatsApp Business
- **SMS (Twilio)** - Mass text messages
- **SMS (Bandwidth/others)** - Alternative SMS providers
- **API Channel** - Campaigns through custom channels

### Audience & Segmentation

**Contact selection:**

- **By individual contacts** - Select specific contacts
- **By labels** - Include all contacts with certain labels
- **CSV import** - In WhatsApp and Channel API campaigns, upload a CSV of phone numbers (name and email optional): new contacts are created, all of them get a label, and that label joins the audience. Contacts that already existed (same phone, Brazil, Mexico and Argentina variants included, or same email) keep their data and labels and only get the new ones. An optional `etiquetas` column (comma-separated) also gives each contact its own labels, created if missing, for later segmentation; the campaign audience is still the panel label. Takes lists of up to 50,000 rows, runs in the background and shows progress plus a summary of new, existing, repeated and rejected rows
- **Combination** - Mix direct contacts and labels
- **Auto deduplication** - Avoid duplicates by phone number

**Smart filtering:**

- Exclude contacts without phone number
- Phone deduplication (takes first contact)
- Pre-send audience counter

### In the Conversation

- **Campaign label** - Every message a campaign sent shows a megaphone with the campaign name above its bubble, and the bubble is violet so it stands apart from agent, bot and automation messages; administrators click it to open the campaign report
- **From the report to the message** - In the campaign report, each contact name opens its conversation with the campaign message highlighted

### Scheduling

- **Immediate send** - Execute campaign now
- **Scheduled send** - Schedule for specific date and time
- **Business hours only** - Pause sends outside hours and auto-resume
- **Inbox timezone** - Respects each inbox's configuration

### Campaign Content

**Text messages:**

- Customizable message with free text
- Emoji support
- **Spintax** - Automatic text variations using `{Hello|Hi} {friend|buddy}` syntax for unique messages per recipient

**File attachments** *(Evolution/WAHA/Uazapi/API)*:

- Images (JPEG, PNG, WebP)
- Videos (MP4, 3GP)
- Documents (PDF, Office, etc.)
- Multiple files per campaign

**WhatsApp Templates** *(Cloud API/Notificame)*:

- Meta-approved templates
- Dynamic parameters per contact
- Header, body, and button components
- Multi-language

### Multi-Inbox (Line Rotation) *(Mega)*

Send campaigns from multiple WhatsApp lines to maximize reach and avoid limits:

- **Auto distribution** - Messages are distributed among your lines
- **Configurable rotation** - Define how many messages to send per line before switching
- **Edit rotation** - In WhatsApp campaigns using Evolution, WAHA, or Uazapi and API channel campaigns, keep selected inboxes, add or remove inboxes, and disable rotation when saving an editable campaign
- **Avoid blocks** - By distributing load, you reduce the risk of per-line limits
- **Higher speed** - Send more messages in less time using multiple lines

### Speed Control *(Mega)*

Smart sending that protects your WhatsApp lines:

- **Automatic pauses** - System pauses between messages to simulate human sending
- **Adaptive speed** - Configuration optimized per provider
- **Block prevention** - Prevents WhatsApp from detecting spam behavior
- **No manual config** - Optimal values pre-configured

### Campaign Status

| Status | Description |
| -------- | ------------- |
| **Active** | Campaign ready to run |
| **Running** | Campaign in progress |
| **Completed** | Campaign finished successfully |
| **Error** | Campaign with critical errors |

### Metrics & Tracking

Monitor your campaign performance in real time:

- **Audience counter** - Know how many contacts your campaign will reach
- **Messages sent** - Real-time progress tracking
- **Failed messages** - Identify delivery issues
- **Error report** - Download failed send details for correction
- **Delivery diagnosis** *(Mega)* - Reports and CSV exports include the provider failure code and reason; inbox or template intervention pauses the campaign without failing unattempted contacts
- **Delivery funnel** *(Mega)* - The report counts sent, delivered, read and failed contacts with their send, delivery and read rates, labels each contact Sent, Delivered, Read or Failed and filters by step; delivered and read come from the provider's receipts, so a line that never reports reads shows none
- **Deleting a campaign** - Removes the campaign and its delivery report; the messages it already sent stay in their conversations, without the campaign label

### Anti-Spam Protection

The system includes multiple protections to maintain send quality:

- **No duplicates** - Doesn't send twice to the same contact
- **Auto detection** - Skips contacts who already received the campaign
- **Send history** - Each message is linked to its campaign

### Sender & Conversations

- **Assign an agent** - Campaign responses go to the selected agent
- **Smart reuse** - If conversation exists with contact, uses the same one
- **Auto close** - Option to close conversation after send

### Supported Channels

| Channel | Type | Templates | Attachments | Multi-inbox |
| --------- | ------ | ----------- | ------------- | ------------- |
| Website (Live Chat) | Ongoing | ❌ | ❌ | ❌ |
| WhatsApp Cloud | One-off | ✅ | ✅ (in template) | ✅ |
| WhatsApp Notificame | One-off | ✅ | ✅ (in template) | ✅ |
| WhatsApp Evolution | One-off | ❌ | ✅ | ✅ |
| WhatsApp WAHA | One-off | ❌ | ✅ | ✅ |
| WhatsApp Uazapi | One-off | ❌ | ✅ | ✅ |
| Twilio SMS | One-off | ❌ | ❌ | ❌ |
| SMS | One-off | ❌ | ❌ | ❌ |
| API Channel | One-off | ❌ | ✅ | ✅ |

### Campaign Management

- **Create and edit** - Intuitive interface for configuring campaigns
- **Pause and resume** *(Mega)* - Pause a running campaign and resume it at any time without losing progress
- **Edit before sending** *(Mega)* - Modify the content, audience and configuration of campaigns that haven't been sent yet or are paused
- **View metrics** - Dashboard with real-time statistics
- **Export reports** - Download campaign details

### Campaign Metrics

- **Audience counter** - Know how many contacts your campaign will reach
- **Messages sent** - Real-time progress tracking
- **Failed messages** - Identify delivery issues
- **Error report** - Download failed delivery details for correction
- **Real-time progress** *(Mega)* - Live progress bar that updates automatically as the campaign executes
- **Estimated ETA** *(Mega)* - Estimated completion time visible during campaign execution

---

## 📚 Help Center

### Knowledge Portals

- **Editable slugs, no duplicates** - Change an article's URL from its properties with validation, no duplicate articles on creation and a tidier public portal (logo locale, deleted authors, tables in previews)
- **Multiple portals** - Create knowledge bases per product/brand
- **Custom domain** - Host on your own domain
- **Configurable design** - Colors, logo, header text
- **Analytics integrations** - Administrators can connect Google Analytics 4, Google Tag Manager, Microsoft Clarity, Hotjar, Plausible, Amplitude, and Meta Pixel; tracking scripts are published only when a valid provider ID is configured
- **Selectable layouts** - Choose between a classic landing page or documentation-style sidebar navigation
- **Multi-language** - Articles in multiple languages
- **Original article** - Each translation is linked to its original article from the article properties; a family has one article per language, and AI translation cannot write over the original's language
- **Recommended content per locale** - Select and order up to 3 featured categories and 6 articles for each locale; popular content remains the fallback when none is configured
- **Remove a language with its content** - Removing a language deletes its articles and categories after a confirmation that shows how many; the default language cannot be removed
- **Norwegian** - Norwegian is listed by its name among the help center languages
- **Dark mode logo** - Add a second logo that the public help center shows in dark mode
- **Managed by administrators** - The Help Center menu shows to administrators and roles that manage the knowledge base; agents still insert articles in their replies
- **GuideJar embeds** - Insert interactive GuideJar guides in Help Center content

### Content Organization

- **Categories** - Group articles by topic
- **Subfolders** - Hierarchical organization
- **Articles** - Rich content with markdown
- **Filter by author** - The article list filters by any teammate (with search) instead of the "Mine" tab, and the status counts follow the chosen author
- **Latest version warning** - If a teammate or another tab changes the article you are editing, the editor offers *Load latest version*
- **Create from category view** - Start new articles directly from each category screen
- **Image resizing** - Resize images inside the editor for cleaner article layouts
- **Slash menu in editor** - Insert blocks and commands quickly by typing /
- **Table-safe slash menu** - Inside table cells, use only inline formatting commands that Markdown preserves, with arrow-key and Ctrl+N/P navigation contained in the menu
- **Videos from the slash menu** - Embed supported video links (YouTube, Vimeo, Loom, Wistia, Arcade, Bunny, CodePen, GuideJar, and MP4), or upload an MP4 with progress, cancellation, retry, and a resizable preview in both the editor and published article
- **Reliable media uploads** - Images appear at the caret while uploading in the background; failed uploads can be retried or removed without losing the draft
- **Dividers from the slash menu** - Insert a horizontal divider from the editor menu to separate article sections
- **Native tables in editor** - Create and edit tables directly in the article editor
- **Markdown tables** - Correct rendering for table blocks inside help articles
- **Positioning** - Order articles manually
- **Category reordering** - Drag and drop to reorder help center categories; the order is saved automatically

### Article Status

- **Draft** - In preparation
- **Published** - Visible to users
- **Archived** - Hidden but preserved; the public help center does not show it, not even from its direct link
- **Draft per language** - Each translation of an article can be in draft state independently; publish only the languages that are ready without affecting others
- **Unpublished edits** - Edits to a published article are staged until reviewed and explicitly published; they can be compared with the live version or discarded

### SEO & Access

- **Meta descriptions** - Optimize for search engines
- **Friendly URLs** - Customizable slugs
- **Integrated widget** - Connect portal with live chat
- **Hide from search engines** - From Settings › SEO a help center can stay out of Google and other search engines while it keeps working for visitors; each article can also be hidden from its properties
- **Images on your domain** - Article images and author photos follow the help center's current domain, also on custom domains

### AI Content Generation *(Enterprise)*

- **PDF-to-FAQ drafts** - Upload PDF documents to generate FAQ drafts with AI
- **Additional context** - Provide optional instructions to guide the generated content
- **Assisted publishing** - Review and publish only the generated entries you want to keep

### Insert Articles in Conversations

- **Article search** - Search articles from the reply box
- **Preview** - View the article before inserting
- **Insert as link** - Add article link to message
- **Popover search reliability** - Restored and stable article search results in conversation popover
- **Copy link** - Copy article URL to clipboard
- **Quick access** - Dedicated button in reply panel

### Embedding Search *(Enterprise)*

- **Semantic search** - Find articles by meaning, not just keywords
- **Contextual AI** - Suggest relevant articles in conversations
- **Real article links** - When Major reads a published article, it gets its public help center link, so it shares the right URL

---

## 📊 Reports & Analytics

### Conversation Reports

- **Volume** - New, resolved, pending
- **Resolution time** - Average and distribution
- **First response** - Initial response time
- **Trends** - Temporal evolution
- **Bar drilldown** - Open each chart bar to review the conversations or messages behind the metric, with bucket navigation and result counts; for conversation counts, View all opens a filtered conversation list in a new tab

### Agent Reports

- **Individual productivity** - Conversations handled
- **Response time** - By agent
- **Satisfaction** - CSAT by agent
- **Availability** - Online/offline time

### Inbox Reports

- **Channel comparison** - Performance by inbox
- **Load distribution** - Balance between inboxes
- **Peak hours** - Identify highest demand times

### Team Reports

- **Team performance** - Group metrics
- **Distribution** - Workload among teams

### Label Reports

- **Label usage** - Frequency and trends
- **Categorization** - Analysis by classification

### Bot Reports

Monitor your AI and bot performance:

- **Bot metrics dashboard** - Comprehensive bot analytics
- **Resolved by bot** - Conversations fully resolved by AI/bots
- **Bot responses** - Counts only public messages sent by bots (AgentBot, Captain, and Flow Builder flows running as a bot); agent replies and private notes in bot conversations no longer count, so totals may be lower than before
- **Bot handoffs** - Conversations transferred to human agents
- **Resolution rate** - Percentage of automated resolutions
- **Time savings** - Agent time saved by automation
- **Filters** - By date range, inbox, bot type

### Call Reports *(Enterprise)*

Complete voice channel analytics:

- **Call dashboard** - Comprehensive call statistics
- **Total calls** - Overview of all calls
- **Answered calls** - Successfully connected calls
- **Missed calls** - Unanswered incoming calls
- **In-progress calls** - Currently active calls
- **Inbound/Outbound** - Direction breakdown
- **Duration metrics** - Total and average call times
- **Queue metrics** - Abandoned incoming calls (the caller hung up before being answered), average wait until an agent answers, % answered within the SLA, and calls solved in the call flow without asking for an agent
- **SLA per inbox** - Each inbox sets within how many seconds a call counts as answered on time (20 by default)
- **Transfers by agent** - How many transfers reached each agent and how many they took
- **Filters** - By date, inbox, agent, status, direction
- **Recordings in the report** - Calls with a recording (WAHA, WhatsApp Cloud or Twilio) play in a compact player with position bar, speed (1x, 1.5x, 2x) and download; calls without one show "No recording"
- **Full width** - Call and activity reports use the whole screen width

### CSAT Surveys

- **Customer satisfaction** - Post-conversation surveys
- **1-5 ratings** - Satisfaction scale
- **Comments** - Qualitative feedback
- **Filters** - By agent, inbox, team, date
- **Review notes** *(Enterprise)* - Add internal notes to CSAT responses for quality tracking
- **CSAT via WhatsApp Templates** *(Mega)* - Send CSAT surveys using official WhatsApp templates instead of the classic in-chat message; requires Meta approval; the system automatically creates and manages the template with versioning; configurable per inbox with toggle between classic and template mode
- **Agent feedback visibility** *(Mega)* - Optionally hide written CSAT comments from agents per inbox while keeping ratings visible; administrators retain complete access and the default preserves existing visibility

### Summary Reports

- **Consolidated metrics** - Overview of key metrics in one place
- **Period filters** - Filter by custom date range
- **Grouping** - Group data by agent, team, or inbox

### Export

- **CSV/Excel** - Download data for external analysis
- **Custom filters** - Export exactly what you need
- **Regional CSV compatibility** - CSV export with UTF-8 BOM and `;` separator for spreadsheet tooling

---

## 👨‍👩‍👧‍👦 Team Management

### Agents

- **Roles** - Administrator, Agent
- **Granular permissions** - Access control by functionality
- **Custom profile** - Avatar, name, signature
- **Account-specific avatar** - A shared user keeps one avatar selector while each account stores and displays its own profile picture
- **Named browser sessions** - Agents can label active sessions to recognize workstations, browser profiles, or testing contexts
- **Reliable browser session control** - Tabs in one browser profile share a logical session; signing out removes it, while another browser, profile, or private window uses a separate slot. Login is interrupted only when a new browser reaches the configured limit
- **Availability status** - Online, Busy, Offline
- **Conversations, calls or both** - From the profile menu, each agent chooses per account whether they take conversations, calls or both (at least one stays on). Auto-assignment skips agents with conversations off and WhatsApp and Twilio calls do not ring agents with calls off; manual assignment still works. The switches show when an inbox of the account takes incoming calls; both are on by default
- **Guided agent offboarding** - Before deleting an agent, choose whether to unassign or bulk reassign their conversations
- **Protected invitations** - New-agent invitations respect the account's daily email limit without blocking the addition of existing users
- **Settings in a side panel** - Agents, teams (with their members), labels, macros, SLAs, custom roles, assignment policies, webhooks, dashboard apps and integrations such as Dialogflow are viewed, created and edited in the same side panel, on phones too

### Teams

- **Departments** - Sales, Support, Billing, etc.
- **Auto assignment** - Round-robin within team
- **Visibility restriction** - Members see only their conversations
- **Visual identification** - Configure an emoji or colored icon per team so agents can recognize teams in lists and assignment pickers

### Inboxes & Members

- **Inbox access** - Assign agents to specific channels
- **View conversations** - Each inbox in Settings › Inboxes, and its settings header, has a link that opens its conversations
- **Capacity limit** - Maximum conversations per agent
- **Assignment policies** - Configure distribution rules

### Assignment Policies

Configure intelligent conversation distribution:

- **Round Robin** - Distribute conversations evenly among agents
- **Fair distribution** - Configurable limit (default 100) per time window
- **Distribution window** - Customizable time period (default 3600 seconds)
- **Conversation priority** - Earliest created or longest waiting first
- **Multiple inboxes** - Apply same policy to multiple channels
- **Enable/disable** - Toggle policies on or off

### Agent Capacity Policies *(Enterprise)*

Define conversation limits per agent:

- **Capacity limits** - Maximum active conversations per agent
- **Per-inbox limits** - Different capacity by channel type
- **Exclusion rules** - JSON-based rules to exclude certain cases
- **Balanced distribution** - Smart selector for optimal load balancing
- **Real-time adjustment** - Capacity updates take effect immediately

### Custom Roles *(Enterprise)*

- **Custom permissions** - Create roles with specific permissions
- **Conversation management** - All, unassigned, or only participating
- **Feature access** - Contacts, companies, reports, campaigns, etc.
- **CSAT permissions** - Control which roles can view and manage customer satisfaction surveys
- **One role per member** - Giving a custom role to an administrator makes them an agent with that role, and making a member an administrator removes their custom role. The account always keeps at least one administrator

### Work Hours

- **Inbox availability** - Define service hours
- **Timezones** - Multi-region support
- **After-hours messages** - Automatic responses
- **Lunch break** - Configure break intervals within business hours
- **Out-of-office exceptions** *(Mega)* - In Business Hours, each inbox can leave WhatsApp groups, specific numbers or identifiers and contacts with certain labels out of the unavailable message, with the same rules as bots
- **Per-day schedules** - Define different hours for each day of the week

### Operational Web Push

- **Closed-page delivery** - Calendar reminders, Kanban note assignments, stage automations, checklist deadlines, and Task deadlines can reach subscribed browsers while the dashboard is closed
- **Direct navigation** - Notification actions open the exact calendar event, Kanban item, or Task that generated the alert
- **Channel control** - Agents configure these operational categories as Push-only preferences; foreground popups remain available when MEGA is open

### Notification Settings

Each agent can customize exactly when and how to receive alerts:

**Notification types:**

- New conversation created
- Conversation assigned to you, including pending conversations
- New message in your conversations
- When you're mentioned in a conversation
- Messages in conversations where you participate

**Notification channels:**

- **Email** - Receive alerts via email
- **Push** - Instant notifications in browser or mobile app
- **Full customization** - Choose which alert type to receive per channel

### Notification Snooze

Temporarily pause notifications for specific conversations:

- **Snooze options** - 1 hour, 3 hours, 1 day, 1 week, or custom time
- **Auto-reopen** - Notification reactivates after snooze period
- **Command bar access** - Quickly snooze via keyboard shortcut
- **Per-notification** - Snooze individual notifications without affecting others
- **Visual indicator** - See when a notification is snoozed

---

## 🔌 Integrations

### Webhooks

Connect MEGA with any external system through automatic notifications:

> **Availability:** Outbound Webhook delivery requires API and Webhooks access for the account on hosted plans. It remains available on self-hosted installations.

- **Real-time events** - Receive instant alerts when something happens
- **CRM integration** - Sync data automatically
- **External automations** - Trigger flows in other tools
- **Total flexibility** - Configure which events interest you
- **Subscription normalization** - Consistent validation/normalization of webhook events and aliases
- **Attachment-enriched payloads** - Includes attachment `content_type` and extension in webhook events
- **Agent Bot update event** - Dispatches webhook when a bot-managed conversation is updated
- **`inbox_updated` event** - Notifies inbox lifecycle changes, including channel disconnects
- **Subscription aliases** - Assign descriptive names to each webhook subscription for easier management
- **Global webhook secret** *(Enterprise)* - Configure a security signature at installation level to verify the authenticity of all outgoing webhook events; payloads are signed with HMAC-SHA256 using the configured secret

### Tasks *(Mega)*

Plan and track internal work from shared calendar and list views:

- **Controlled activation** - Super administrators enable the account feature and account administrators connect Tasks from Settings -> Integrations
- **Custom task types** - Administrators define reusable categories and semantic colors for the team's work
- **Retire instead of delete** - A task type can be deactivated so it is no longer offered for new tasks while existing tasks keep it; deleting a type that still has tasks offers that option, and deleting or disabling Tasks always asks for confirmation
- **Consistent palette** - Task types use the same 22-color visual palette as Google Calendar and retain the selected color in calendars, details, and lists without status replacing it
- **Scoped permissions** - Administrators control every task; custom roles can independently receive own/assigned task management, global read access, and task reporting; standard agents only see and manage tasks they created or are assigned to
- **Calendar and list views** - The header of Scheduled messages: search, a filter panel (sheet on phones), a calendar/list toggle, refresh and New task (a floating button on phones). The month uses the ‹ month › control and the Calendar module grid, with up to three tasks per day and their state as an icon (overdue, in progress, struck through when closed); the list is an agenda grouped by day. On phones the month shows dots and the picked day's tasks below. Both open the same detail
- **Operational filters** - Search by title; filter by assignee —including unassigned—, type, and today, this week, or the next 30 days; one status selector starts at All tasks and offers pending, in-progress, overdue, completed, or cancelled work; sort the list by start, due date, title, priority, status, or assignee
- **Multi-day tasks** - A task appears on every calendar day intersected by its schedule, including when it began before the visible month
- **Mobile experience** - On small screens, filters reorganize without compressing the monthly calendar; forms and details keep actions visible without covering content
- **Read before editing** - Opening a task shows its details; complete and cancel actions sit in the header with a required summary, while edit and administrator-only confirmed deletion remain in the footer
- **Clear ownership** - Assign a task to an account agent or leave it unassigned
- **Resilient history** - Deleting a linked contact, conversation, Kanban item, or assignee preserves their historical labels, clears live references, and resynchronizes the Google projection without duplicating the deletion cascade
- **Operational states** - Manage pending, in-progress, completed, and cancelled tasks; overdue work is detected automatically after its deadline
- **Documented closure** - Completing or cancelling requires an outcome summary so the result and next steps remain recorded
- **Assignee deadline alert** - At the deadline, only the assigned agent receives a popup and notification to open, complete, cancel, or edit the task; they can mark it as seen or snooze it to reappear automatically, and unassigned tasks generate no alert. The alert reads like a Google Calendar event card: type color and name, how long ago it was due, date, contact and conversation, high or urgent priority and the start of the description, with a one-click Snooze menu; with several alerts it shows how many are left. Calendar event reminders use the same design, with location and Google Meet link
- **Recurring tasks** - Repeat tasks daily, weekly, monthly, or yearly with an interval, selected weekdays, and an end date or up to 100 repetitions
- **Connected context** - Optionally link a contact and conversation, or create an item in a funnel and stage without requiring a customer
- **Creation from conversations** - ReplyBox shows an action beside the calendar when Tasks is enabled and connected; it opens the form with the contact, conversation, current assignee, and any related Kanban item prefilled
- **Contact-wide tracking** - ContactPanel includes a dedicated Tasks accordion in the calendar format, identifies each linked conversation by its stable visible number, and keeps the contact's pending, in-progress, and overdue work visible across new conversations
- **Feature-gated Kanban** - Kanban item linking and creation appear only when `kanban_board` is enabled for the account
- **Tasks inside the item** - When Tasks is enabled and connected, Kanban details separate technical history from an operational tab used to create, review, and open tasks linked to the item
- **Kanban traceability** - Item history records when a linked task is created, updated, started, completed, cancelled, reopened, linked, unlinked, or deleted, including its status and assignee
- **Participants and priority** - Set priority, responsible agent, account participants, and external guests
- **Optional Google Calendar** - Synchronize exact start, end, and attendees in one event while preserving local work on provider failures
- **Task reports** - Administrators and custom roles with the dedicated task-report permission review tasks by date, responsible agent, type, and status; generic report access does not grant this permission
- **Developer API** - Use the account-scoped Tasks and Task Types CRUD APIs from Swagger/OpenAPI or the generated Postman collection, including search, interval intersection, sorting, opt-in pagination, and linked-workflow fields

### Google Calendar *(Mega)*

- **Personal event reminders** - The event creator receives an in-app and browser push reminder, can snooze it with preset intervals, and can reopen the shared event dialog. New events automatically include the creator email and, when created from a conversation, the contact email as deduplicated guests.

Connect Google Calendar as an account-level productivity integration instead of an inbox/channel:

- **Account-level OAuth** - Administrators connect the account calendar from Settings -> Integrations -> Google Calendar
- **Custom-role access** - Administrators can grant an assigned agent the “Access Calendar” permission for Calendar, ReplyBox, and ContactPanel
- **Configuration-gated availability** - The `/calendar` workspace, composer icon, and conversation-panel events appear only when the account is connected with a selected calendar; Kanban sync controls require the same account configuration
- **Calendar selection** - Import all accessible calendars by default or limit inbound import to one; MEGA keeps a concrete outbound destination and defaults new setup to bidirectional sync
- **Minimal event creation** - Use a Google Calendar-inspired two-column editor with selectable time zones, removable guest chips, writable destination selection, and Google Meet creation/copy/access without stacked cards
- **Internal event layer** - MEGA stores calendar events internally and tracks Google provider IDs separately
- **MEGA calendar workspace** - Agents manage day, week, month, and list views from `/calendar`; the month view limits visible events per day and offers `+N more` or a context menu for actions without hiding events. Events support colors, and administrator-only permanent deletion also removes the linked Google event
- **Google-like event form** - Manual events support timezone, location, guests, reminders, recurrence, Google Meet, and installation-branded context with channel icons in conversation search
- **Searchable MEGA links** - Agents search and select contact, conversation, and Kanban item while creating or editing events without typing internal IDs
- **Module controls** - Enable sync for internal calendar, Kanban, conversations, and reminders from one place
- **Sync on save** - When outbound sync is enabled, MEGA creates or updates the event in the selected Google calendar while preserving internal status
- **Automatic Google polling** - Every five minutes MEGA imports only events changed since each calendar's last successful poll; deleted Google events remove their mapped local entries, and `/calendar` offers manual sync as a fallback
- **Connection health** - View connected identity, reconnect when needed, and disconnect without removing internal events
- **Kanban scheduling bridge** - Scheduled/deadline Kanban items can create internal events and sync them to the selected calendar
- **Conversation scheduling and sharing** - Agents use the same Google-enabled event form from the conversation reply composer with contact and conversation prefilled, and the “Create and send” button shares the schedule, location, details, and generated Google Meet link
- **Conversation follow-up** - The panel shows linked events with a pulsing green (<50%), yellow (50–90%), or red (≥90%) dot based on Start-to-End progress, fades expired entries, and reopens the shared editor
- **Google import and legacy backfill** - Administrators can pull Google events into MEGA and backfill legacy Kanban event IDs into the global calendar model

### Meta Template Builder *(Mega)*

Create and manage your WhatsApp templates directly from MEGA, without needing to access Meta Business Manager:

**Template management:**

- **Centralized list** - View all templates from all your WhatsApp inboxes in one place
- **Unified cached template API** - Integrations can list cached templates for native and Twilio WhatsApp inboxes, filter by the provider's exact name, and read the last synchronization-attempt time without contacting the provider
- **Approval status** - Monitor whether each template is approved, pending, or rejected by Meta
- **Meta category changes** - Flags when Meta recategorizes a template (for example, from Utility to Marketing) or announces it will within 24 hours, with a shortcut to request a review
- **Usage metrics** - See how many times each template was delivered and its read rate
- **Advanced filters** - Filter by status, category, language, channel, and date range
- **Search** - Quickly find templates by name or content
- **Delete templates** - Delete individual or bulk templates with confirmation
- **Turn templates on or off** - Hide a template from agents (reply box, new conversation and scheduled messages) without deleting it on Meta; campaigns and automations can still use it. Useful for Meta sample templates or campaign-only templates
- **Sync templates** - Sync button to pull new templates from Meta
- **Automatic initial sync** - Runs an initial template sync right after channel creation
- **Duplicate prevention** - Insert validations to prevent duplicate templates during sync
- **Responsive table layout** - Improved template metadata table visibility on desktop and mobile

**Visual builder:**

- **Step-by-step template creation** - Guided flow: Basic Info → Builder
- **Optional header** - Text or multimedia header (image, video, document)
- **Message body** - Editor with bold *text*, italic *text*, variables {{1}}, {{2}}
- **Format toolbar** - Format buttons and variable insertion with one click
- **Optional footer** - Footer text (up to 60 characters)
- **Action buttons** - Visit website, call phone, quick reply, or copy code
- **Real-time preview** - See how the template will look before sending
- **Sample values** - Define examples for variables to ease Meta approval
- **Categories** - Marketing, Utility, Authentication
- **Multi-language** - Create templates in any language supported by WhatsApp

**Template editing:**

- **Detail view** - Inspect full template structure before entering edit mode
- **Optimized media uploads** - Improved media file upload behavior for edit/send flows

### Dashboard Apps

Embed custom applications within the conversation view:

- **Custom iFrames** - Embed external apps in conversations
- **Synchronized app context** - Embedded apps receive custom attribute definitions and the resolved light/dark theme; context refreshes when these change or the tab reopens, and refresh requests receive a response only in the requesting iframe.
- **Dynamic context** - Pass conversation and contact information to the app
- **Per-user apps** - Apps can be configured per agent
- **Multiple apps** - Add several apps to the same inbox
- **Secure** - Apps run in sandboxed iframes
- **Real-time data** - Apps receive live conversation updates
- **Administrator management** - Account-wide apps can be created, updated, and deleted only by administrators; authenticated agents retain read access
- **Dashboard scripts (Super Admin)** *(Mega)* - Publish global dashboard customizations without modifying core code. The list shows each script's load order, the external hosts it pulls code from, its size and an on/off switch, with live search and a status filter; one form creates and edits a script with line numbers, a length meter and a preview of a real account dashboard that injects unsaved code and reports errors. Phones get one card per script, with compact navigation and an editor sized for the screen
- **Agent Bots (Super Admin)** *(Mega)* - Manage the agent bots of the whole installation. The list shows who can connect each bot (global or one account), its type, the host it sends events to and how many inboxes use it, with live search by name, URL or account and a scope filter; the bot page gathers its details, the connected inboxes with their account and status, the webhook URL, the signing secret and API token masked with copy, and deletion; the form picks the account with a search (empty = global bot). On phones each bot is a card
- **Platform apps (Super Admin)** *(Mega)* - Manage the apps that use the Platform API. The list shows how many accounts each app reaches and the users and bots it created, with live search; the app page lists accounts with search, a with/without access filter and pagination to grant or revoke access one by one or grant all, and gathers the masked API token with copy, the records it manages and deletion; the form has an all-accounts switch that never revokes access. It warns that accounts created later are not added on their own. On phones each app is a card
- **Platform banners (Super Admin)** *(Mega)* - The list shows each banner in its type's color, who sees it, when and whether it is showing now, scheduled, ended or turned off, with an on/off switch per row, live search and a status filter; the banner page gathers the message, audience and dates, the chosen accounts, activity (including how many agents closed it) and the same preview as the form, with a note when it is scheduled or ended. In the form the type is picked by color and the preview follows the type, title, message and status while editing, in the real dashboard colors. On phones each banner is a card
- **Feature announcements** *(Mega)* - Super Admin announces a new feature with an image or a video and a short write-up: a YouTube, Vimeo, Loom, Arcade, Bunny, Guidejar or CodePen link, the link of a file, or a file uploaded from the same form by creating a banner of the New feature type, with the same accounts, roles and dates as other banners. Agents see it as a panel over the dashboard when they open it; with several active announcements they switch between them with the thumbnails, the dots, the arrow keys or a swipe on touch screens. Once closed it stays closed on all their devices until the announcement is edited, and a new or edited announcement shows up live without a reload. The form asks for the image or video only for this type and the preview shows the panel with the image
- **WhatsApp providers (Super Admin)** *(Mega)* - Evolution API, WAHA and Uazapi servers show as a grid of cards with their provider and slot, inbox usage against capacity, the API host, where the credentials come from (saved, environment or missing), voice calls and status, with live search and a provider filter; the server page shows usage, the inboxes it hosts with their account, the connection with the environment variables the slot reads and whether they are set, settings and deletion (blocked for the legacy slot or while it hosts inboxes). The sectioned form picks the provider as a choice and shows live which environment variables the chosen slot reads. On phones each server is a full-width card
- **Push diagnostics (Super Admin)** *(Mega)* - A three step tool to check why a user gets no notifications: find the user by name, email or #id (each result says how many devices they have), pick their subscriptions, which show the browser (Chrome, Firefox, Safari, Edge) or the mobile app, the end of the endpoint or token and the last update, or delete broken subscriptions. Next to them, the test message shows a live preview of the notification with the installation's icon and name, length counters for title and body, default text in the Super Admin language that can be restored, and a button that says how many devices it goes to. The browser test push now carries the body, not just the title. Results show per device whether the push service accepted it, failed or skipped it, with the raw response; failures open on their own. On phones each device is a card
- **Settings pages (Super Admin)** *(Mega)* - Each Settings page (General, SAML SSO, Custom branding, Billing, Captain, Email, Messenger, Instagram, TikTok, Google, Microsoft, Linear, Notion, Slack, WhatsApp embedded, Shopify, EvolutionAPI, QuepasaAPI, Mega Hub and Call ICE) shows the feature's icon, name and description, and groups its values in sections with a title and an explanation (for example App, Webhooks and Options on channels, or Images, Identity, Colors, Legal and Web on branding). Every value shows its variable name; secrets stay hidden with a reveal button, images show their preview and can be uploaded, and colors get a picker. Saving happens from the sticky bar with a translated notice. On phones the sections stack in one column with the save bar at the bottom
- **AI providers (Super Admin)** *(Mega)* - The list shows each provider as a card with its connection type and host, whether it is on, whether it is the Captain or Mega Assistant default, how many models it has and the state of each capability (verified, failing or untested), plus the provider's credit or quota warnings. The provider page gathers the models table with each capability's result, AI Actions, reasoning and prices, the failed tests with their message, the connection, where it is used (including the accounts that picked it) and deletion; models are tested from there. The form is split into Connection, Availability and Models: each model is a row with its uses as toggles and its price and reasoning folded under it. On phones cards and tables become one column
- **Plan features (Super Admin)** *(Mega)* - When creating or editing a plan, features look the same as in the account features tab: one card per category with how many the plan includes, each feature with its name, its switch and the Premium tag, All / Included / Not included filters with their totals, and search. The Use defaults, Select all and Clear selection actions are still there and take the screen width on phones.
- **Super Admin sign in** *(Mega)* - A brand panel in the installation's primary color sits beside the form: the logo, what the console covers (accounts and users, plans and billing, instance health) and, quietly at its foot, a Mega message picked at random, with the domain and version. Phones keep only the form, with the message above the language and theme pickers. The sign in page lets you pick the language and theme before signing in, and the picked language stays after signing in. It shows the installation logo (`LOGO`, or `LOGO_DARK` on the panel and in the dark theme). A wrong email or password is reported in the user's language, keeping the email and putting the cursor in the password. The show password button changes its icon, the sign in button shows it is signing in and does not submit twice, and signing in goes back to the page that was asked for or to the Dashboard.
- **Light and dark mode in Super Admin** *(Mega)* - The account menu in the sidebar has a theme picker: Light, Dark or System (follows the operating system). The choice is the same one the agent dashboard uses, so both switch together, and it applies to every page, the sign in page (with the dark logo when one is set), dialogs, charts and the script preview, without a flash on load.
- **Redesigned Super Admin console** *(Mega)* - Sidebar grouped by section (collapses to icons) and, on phones, an off-canvas menu with a top bar; forms split into sections, lists that turn into cards on mobile, a live preview of platform banners and add-on prices per currency with a single fill-from-USD action. The accounts list filters by billing state through tabs that show their share, combines that with one state or source filter (active, suspended, courtesy, manual payment, recent…), sorts by name, agents or creation date, filters as you type, also searches the emails of the account's users, and on phones shows cards with usage meters, a select mode for bulk actions and a bottom sheet for filters and sorting. On the account page, Subscription and payments is split into sub-tabs (subscription, invoices, AI usage, AI Actions movements and history), subscription actions sit in a bar at the foot of their card, and on phones invoices, users and features show as rows that fit the screen. Suspending or reactivating the account is done from the summary (Account status card) or the ⋯ menu, with the category and reason a suspension requires, without opening Edit
- **Safe preview and per-script toggle** *(Mega)* - Validate changes safely and enable/disable scripts independently

### Platform Apps

Build and connect external applications with full API access:

- **Full API access** - Complete programmatic access to the platform
- **Permissibles** - Granular control over which resources the app can access
- **Account management** - Create and manage accounts programmatically
- **User management** - Manage users via API
- **Bot integration** - Connect custom bots via Platform Apps
- **Secure tokens** - API tokens with scoped permissions
- **Scope enforced** - A platform app only gets existing users it already manages, and only creates or moves bots into accounts it has access to
- **Use cases** - CRM integrations, custom dashboards, automation systems

### Slack

Manage customer conversations directly from Slack, without switching tools:

- **Auto sync** - Conversations appear in Slack channels
- **Respond from Slack** - Reply to customers without opening MEGA
- **Alerts only** - Keep Slack threads for internal discussion without sending replies to the customer
- **Private notes** - Communicate with your team without customer seeing
- **Profile linking** - Connect Slack users with MEGA agents
- **Private channels** - Organize by team or conversation type
- **Reconnection alerts** - Notice if integration needs renewal

### Dialogflow

- **NLU Bot** - Connect with Dialogflow agents
- **Intents and entities** - Natural language processing

### OpenAI / GPT

Advanced AI features with GPT models:

- **Writing assistant** - Improve and correct your responses
- **Conversation summary** - Generate automatic summaries
- **Auto translation** - Translate messages to any language
- **Response tone** - Adjust tone (formal, friendly, etc.)
- **Text expansion** - Develop short ideas into complete responses
- **Simplification** - Simplify complex texts

### Dyte (Video Calls)

Video calls integrated directly into the conversation:

- **Create meeting** - Start a video call with one click
- **Join meeting** - Customers can join from widget
- **Reply box button** - Quick access from reply box
- **Video message type** - Calls appear in timeline

### Google Translate

Automatic message translation in conversations:

- **Automatic translation** - Translate incoming messages to your configured language
- **Language detection** - Automatically identifies the message language
- **In-context translation** - Translated messages displayed inline in the conversation
- **Multi-language support** - Compatible with all Google Translate languages
- **Verified key** - The Google service account key (`type: service_account`) is checked with Google when the integration is connected and every time it changes

### Auto translate *(Enterprise)*

Talk to every customer in their language, whatever languages your team speaks:

- **Read in your language** - Contact messages and bot replies show in each agent's dashboard language, with *View original* to read what the customer wrote
- **Reply in theirs** - Agent replies, greetings, out-of-office and CSAT messages go out in the customer's language; the agent's own text stays one click away, also for the customer in the web widget
- **Follows the customer** - The language is detected on every message, so a customer who switches language gets replies in the new one. A message of one or two words (a city name, a typo) does not change the conversation language
- **Captain or Google Translate** - Pick the translation service in Settings → Conversation workflow → Translation; Captain is the recommended service, because it reads the whole conversation and keeps short replies like "ok" in the right language; Google Translate sits under *Use other providers* and is billed by Google on the account's Google Cloud. Accounts with Google Translate connected keep it until they choose, with a *Switch to Captain* button. With Captain each translation uses AI Actions (detecting the language is free) and the model can be picked in Captain settings
- **Exactly as written when it must be** - Private notes, WhatsApp templates, Direct Send, interactive messages, campaigns and forwarded messages are never translated; a reply that cannot be translated is sent as typed and flagged for the agent. If the translation service fails, the reply is still sent
- **Turn it off for one conversation** - From the conversation menu (*Turn off auto-translate*) an agent turns it off for that conversation only: neither its messages nor the replies are translated until it is turned back on from the same menu. The conversation shows who turned it off or back on
- **Off by default** - Enabled per account (Super Admin feature *Auto Translate*) and switched on by the account admin

### Linear *(Enterprise)*

- **Ticket management** - Create issues from conversations
- **Sync** - Keep statuses updated
- **Safe unlinking** - From a conversation, only issues linked to that same conversation can be unlinked

### Shopify *(Enterprise)*

- **Customer data** - View purchase history
- **Recent orders** - E-commerce context

### WooCommerce *(Enterprise/Mega)*

Complete WooCommerce integration:

- **Store connection** - Link your WooCommerce store
- **Order history** - View customer orders in context
- **Search by email and phone** - Finds orders by email and by phone, even when the store saved the phone in a local format
- **WooCommerce webhooks** - Receive store events
- **Order panel** - Order view in conversation

### Stripe in the contact panel

Read-only view of your own Stripe billing next to every conversation (separate from the Mega subscription billing):

- **Your own Stripe account** - An administrator connects it with a restricted API key, stored encrypted
- **Customer by email** - The contact's Stripe customer is found by email; when several match, the agent picks one
- **Subscriptions** - Latest five, with status, price, quantity, renewal, trial end and scheduled cancellation
- **Recent invoices** - Number, date, amount and status of the last five invoices
- **Access control** - Only agents who can see the conversation see its billing data; managing the key is for administrators
- **Desktop and phone** - A section of the contact panel, and a page of the contact sheet on phones

### Notion *(Enterprise)*

- **Documentation** - Connect Notion pages
- **Knowledge base** - Quick access to resources

### CRM (LeadSquared)

- **Lead sync** - Send contacts to your CRM
- **Unified history** - 360 customer view

### Email Templates

Customize email communications with your branding:

- **Custom templates** - Create branded email templates
- **Per-account templates** - Different templates for each account
- **Liquid variables** - Dynamic content with variable substitution
- **Installation templates** - Default templates for the entire installation
- **Template types** - Support for different email types (notifications, transcripts, etc.)
- **Branded reply layouts** - Administrators can configure a Liquid HTML fallback per account and an override per Email inbox; layouts must include `{{ content_for_layout }}` and support up to 262,144 characters.

---

## 💎 Enterprise Features

### SLA (Service Level Agreements)

- **Configurable policies** - Define target times
- **First response** - Maximum time to respond; its live clock ends after the first agent reply while missed results remain in SLA reports
- **Next response** - Time between responses
- **Resolution** - Total service time
- **Frozen misses** - Resolving a conversation records the breach duration so it no longer increases
- **Business hours** - Backend-computed deadlines that respect inbox working hours
- **Blocked contacts** - Conversations with blocked contacts are excluded from SLA assignment, processing, reports, and indicators until unblocked
- **Alerts and notifications** - Warning before breach
- **SLA reports** - Compliance and trends
- **Create automation** - After creating an SLA, a shortcut opens a new automation rule that already applies it (accounts with automations)

### Audit Logs

- **Complete record** - Every action is logged
- **Who, what, when** - Full traceability
- **Compliance** - For regulatory requirements
- **Find events quickly** - Filter by event type and whole-day date range, search the acting user's name or email, and sort newest or oldest; filters are shareable through the page URL
- **Deletion evidence (Super Admin)** *(Mega)* - A read-only report filters retained Inbox, Conversation, Contact, and Message destruction audits by account; Message entries retain the original content for evidence while the audit-log API omits it and the message payload from list responses. The account is chosen with a search picker; a live search (name, email, phone, IP or ID) and a record-type filter with counts narrow the list, which is grouped by day and expands each audit to show and copy everything it retained; phones get one card per audit

### SAML/SSO

Enterprise Single Sign-On for centralized authentication:

**Supported providers:**

- **Okta** - Full Okta integration
- **Azure AD** - Microsoft Entra ID
- **Google Workspace** - Google as identity provider
- **OneLogin** - Full support
- **Auth0** - Integration available
- **Generic SAML 2.0** - Any compatible provider

**Features:**

- **Auto-provisioning** - Automatically create users on first login
- **Account isolation** - A user who belongs to several accounts can use SAML only when all of them trust the same identity provider; otherwise invitations and SAML sign-in are refused
- **Group mapping** - Sync groups/teams from IdP
- **Force SSO** - Require SSO for all account users
- **Multiple domains** - Configure SSO for different email domains
- **Single Logout** - SLO supported
- **IdP metadata URL** - Paste the identity provider's metadata URL instead of copying the SSO URL, entity ID and certificate by hand. Mega reads them from the URL, picks up a rotated certificate when the current one is about to expire, and a Refresh metadata button reads them again on demand. The manual form stays available

**Security:**

- **Centralized authentication** - Unified access management
- **IdP password policies** - Use corporate password rules
- **IdP MFA** - Multi-factor authentication from provider
- **Instant revocation** - Remove access by deactivating in IdP

### Advanced Assignment (V2)

- **Agent capacity** - Dynamic limits
- **Smart balancing** - Optimal load distribution
- **Complex rules** - Custom assignment logic

### Advanced Search

- **Full indexing** - Search all messages
- **Transcript-aware results** - Find transcribed audio in message results and its parent conversation
- **Combined filters** - Multiple simultaneous criteria
- **Instant results** - Optimized performance

### Required Conversation Attributes

Force agents to complete specific attributes before resolving conversations:

- **Required fields** - Define which custom attributes must be filled
- **Resolution validation** - Block resolution until required fields are completed
- **Safe macros** - Resolving macros request required attributes; if dismissed, they run the remaining actions but keep the conversation open
- **Improved data quality** - Ensure every conversation has the necessary information

### Voice Conferences

Voice conference calls between agents and customers:

- **Multi-party calls** - Connect multiple participants in one call
- **Conference management** - Full conference controls
- **Integrated in conversations** - Conferences are linked to existing conversations

### Custom Branding

Fully customize your platform's appearance:

- **Custom logo** - Your logo instead of the default platform logo
- **Dark mode logo** - Specific logo for dark mode
- **Thumbnail logo** - Square application artwork for the favicon, installable PWA icon, and splash screen, with the notification icon as fallback
- **Notification icon** - Independent square image for system Push alerts, badges, and the temporary hidden-tab indicator; defaults to `/favicon-badge-16x16.png` with the thumbnail logo as fallback
- **Brand name** - Change name shown throughout platform
- **Installation name** - Name for specific instance
- **Primary color** - Define your corporate main color
- **PWA icon background** - Configure the installable app icon background without rebuilding the image
- **Brand URL** - Your company link
- **Widget URL** - Link in chat widget
- **Terms and privacy** - Custom URLs for legal pages
- **Meta description** - Custom SEO for your installation

### Disable Branding

- **Unbranded widget** - Remove platform attribution from live chat
- **Unbranded emails** - Outgoing emails without platform branding
- **Clean portals** - Help Center without platform references

### Custom Roles

Create roles tailored to your organization with granular permission control:

**Control access to:**

- **Conversations** - Who can view and manage which conversations
- **Contacts** - Access to customer data
- **Companies** - Access to the Companies menu and company records
- **Reports** - Who sees statistics
- **Campaigns** - Permissions to create and send campaigns
- **Help Center** - Article and portal management
- **Sensitive data** - Control over visible phone numbers

**Role examples:**

- **Supervisor** - Views reports and metrics without editing configuration
- **Senior Agent** - Can take unassigned conversations
- **Basic Agent** - Only works with assigned conversations
- **Analyst** - Exclusive access to reports and statistics
- **Community Manager** - Manages campaigns and Help Center content

---

## ⭐ Mega Exclusive Features

### 🧭 Guided Onboarding

- **Dedicated initial setup** - Complete account details through a purpose-built administrative flow
- **Phone at signup** *(Mega)* - The account creation form asks for an optional phone number (WhatsApp) so the team can reach the customer during activation; Super Admin shows it in the account header with a direct WhatsApp link
- **Normalized website URL** - Store the address with its protocol for downstream integrations and automation
- **Guided Instagram connection** - Resume inbox setup after authorizing Instagram from onboarding

### 📅 Scheduled Messages

Schedule automatic message delivery in your conversations:

- **Flexible scheduling** - Choose exact date and time to send the message
- **Recurrence** - Schedule recurring messages: daily, weekly, monthly, or yearly
- **Series that keep going** - Weekly series send on the chosen weekdays in the account time zone (Settings → General). If the next send cannot be created, the sent message shows why instead of the series stopping silently; attachments carry over to every send
- **Templates** - Use predefined message templates for scheduled sends
- **Attachments** - Include images, documents, and files in scheduled messages
- **Status tracking** - Monitor status: pending, sent, failed, cancelled
- **Cancellation** - Cancel scheduled messages before they are sent
- **Recovery and send again** - Retry or reschedule a failed message, or schedule an editable copy of a sent one while retaining its recipient and attachments
- **Universal scheduling API** - Schedule a message for a phone, email, or provider identifier while automatically creating or reusing the contact
- **Multiple per conversation** - Schedule several messages in the same conversation
- **History** - View the history of scheduled messages and their status
- **Calendar and list** - Monthly calendar in local time, with the time and title of each send, and a list grouped by day that shows the upcoming sends first and the earlier ones below (or a chosen range). Search and filters by status, inbox and agent in both views, on desktop and phone
- **Attachments when editing** - Editing a pending message shows its files, which can be removed, and new ones can be added (up to 15)
- **Detail with actions** - The detail shows the provider error and offers the actions of its status: cancel or edit a pending one, retry or reschedule a failed one, send a sent one again
- **From the conversation and Kanban** - The contact panel button and the Kanban tab list that conversation's scheduled messages with the same actions, and use the same form as the page

### 🔒 Deleted Message Placeholder

Configure per inbox whether agents see the original text and attachments alongside the deletion notice:

- **Agent retention** - Can show the original text and attachments below "This message was deleted" inside the dashboard
- **Per-inbox configuration** - Each channel can have its own setting
- **Contact protection** - The public API and contact-facing realtime events deliver only the deletion notice, without attachment metadata or file URLs

### Alternative WhatsApp Providers

MEGA includes multiple WhatsApp providers beyond Meta's official API, allowing flexibility in costs, features, and use cases.

**Multi-server management (Mega):**

- **Multiple servers per provider** - Configure more than one server per channel for operational continuity
- **Configurable capacity** - Define per-server limits to distribute messaging volume
- **Partial legacy server editing** - Adjust existing server settings without recreating full connections
- **Assigned server visibility** - Quickly identify which server is linked to each inbox

---

### 📱 WhatsApp Evolution

Direct WhatsApp connection without needing the official API, ideal for companies seeking flexibility and cost savings.

**Main advantages:**

- **QR Connection** - Link your WhatsApp in seconds by scanning a code
- **No mandatory templates** - Send messages freely without approvals
- **No 24-hour window** - Start conversations whenever you want
- **No per-message costs** - Avoid Meta's official API fees

**All content types:**

- Texts, images, videos, documents
- Audio and voice notes
- Stickers
- WhatsApp group support

**Ideal for:**

- Companies looking to reduce costs
- Operations needing message flexibility
- Teams already using personal or business app WhatsApp

---

### 📱 WhatsApp WAHA

Robust, high-availability solution for demanding operations requiring maximum stability.

**Main advantages:**

- **High availability** - Designed for production with auto-reconnection
- **Multiple numbers** - Manage multiple lines in one installation
- **Very stable** - Ideal for 24/7 operations

**Full multimedia content:**

- Texts, images, videos, documents
- Audio and voice notes
- Stickers and reactions, including API-token reaction sending
- Complete group support

**Advanced features:**

- Presence status (typing, online)
- Read receipts
- Edited and deleted messages
- Passkey authorization during WhatsApp linking through the WAHA browser extension flow, with dedicated session states, a proactive notice when the extension is not installed, and manual code confirmation when WhatsApp requests it
- On-demand global and per-conversation sync for recent messages, with account-level concurrency protection and optional dedicated processing for high-volume installations
- Optional per-inbox WAHA group lazy media download: incoming group media is stored as a pending attachment with a generic placeholder and is only downloaded when an agent requests it from the conversation; direct conversations retain immediate downloads
- Per-session proxy with a `host:port` server and optional credentials, which can be removed to return to a direct connection
- Per-session WAHA apps: switches to enable or disable Phone Numbers for Brazil, Argentina and Mexico, and Voice calls when available, reflecting each app's current state
- Session settings screen shared by WAHA, Evolution and Uazapi: a clear connection status, QR or pairing-code linking without pop-ups, switches that save on their own, and a confirmation before recreating or disconnecting the session

**Ideal for:**

- High-volume operations
- Companies needing maximum stability
- Teams with multiple WhatsApp lines

---

### 📱 WhatsApp Uazapi

Economic and scalable solution for high-volume operations.

**Main advantages:**

- **Competitive pricing** - Ideal for high message volume
- **Flexible connection** - By QR or pairing code
- **Multiple lines** - Each number with its own configuration
- **Speed control** - Avoid blocks with controlled sending

**Supported content:**

- Texts, images, videos
- Audio and voice notes
- Documents
- On-demand global and per-conversation sync for recent messages, with historical media recovery

**Chat filter configuration:**

Define which conversations you want to receive in the platform:

- **Filter by type** - Receive only individual chats, groups, or both
- **Exclusion list** - Ignore specific numbers
- **Inclusion list** - Receive only from specific numbers
- **UI configuration** - Manage filters directly from channel settings

**Regional proxy:**

- **Brazilian city selection** - Save an optional managed-proxy city in channel settings
- **Applied on new connections** - The saved location is used for QR, pairing-code, and recreated sessions
- **Custom proxy or no proxy** - Switch to your own proxy URL or completely remove the active proxy

**Ideal for:**

- Companies with tight budgets
- High-volume operations
- Teams needing multiple low-cost lines

---

### 📱 WhatsApp Notificame

Brazilian provider combining the official WhatsApp Business API with ease of use.

**Main advantages:**

- **Official Meta API** - All the reliability of the official API
- **Approved templates** - Send messages outside the 24h window
- **Auto sync** - Your approved templates are imported automatically
- **Multiple lines** - Manage multiple channels from one account
- **Phone replies** - Replies sent from the phone or WhatsApp Web show up in the conversation as sent messages

**Supported content:**

- Texts and templates with custom parameters
- Images, videos, and documents
- Shared locations

**Ideal for:**

- Companies in Brazil or Latin America
- Operations requiring official templates
- Teams needing official API reliability

---

### 🎙️ WaVoIP Integration (Webphone) *(Evolution/WAHA/Uazapi)*

Make voice calls via WhatsApp directly from the platform using alternative WhatsApp providers:

**What is WaVoIP?**

WaVoIP enables voice calls through WhatsApp for providers that don't use Meta's official Cloud API (Evolution, WAHA, Uazapi). It's a third-party service that bridges voice calls to your browser.

**Main features:**

- **Inbound and outbound calls** - Full voice over WhatsApp support
- **Intuitive webphone** - Easy-to-use floating widget in your browser
- **Complete controls** - Mute, hang up, accept, reject calls
- **Real-time duration** - Timer visible during call
- **Quality indicator** - Monitor connection quality live
- **Persistent device sessions** - Preserve per-inbox authentication and status to reduce manual reconnects
- **Auto recording** - Automatic call recording with download option
- **Recording storage** - Recordings saved and attached to conversations

**How it works:**

1. Configure your WaVoIP account credentials
2. Enable WaVoIP feature on your account
3. Webphone widget appears when calls come in
4. Accept/reject calls directly from browser
5. Make outbound calls from contact profile

**Benefits:**

- Voice calls without official WhatsApp Business API
- Works with personal WhatsApp numbers
- No per-call Meta charges
- Complete call history in conversation

---

### 🔄 Inbox Migration

When you need to reorganize your channels:

- **Transfer conversations** - Move chats between channels without losing history
- **Preserve all context** - Messages, files, and notes are maintained
- **Mass operations** - Migrate multiple conversations at once
- **Visible progress** - Pick source and destination with search, get warned that the migration cannot be undone and follow migrated contacts, conversations and messages live

### Unified Conversation History

Complete context of each customer regardless of how they contacted you:

- **360° view** - All contact history in one place
- **All channels** - WhatsApp, email, social media, all together
- **Immediate context** - Understand the customer before responding
- **WhatsApp replies** - Quoted replies can reference messages from previous conversations when history is enabled and retain context in coexistence between phone-scoped and BSUID-scoped WAMIDs

### Privacy Controls

Configure what your agents can see and access:

- **My conversations only** - Agents see only their assigned chats
- **Hide contacts** - Restrict access to complete database
- **Simplified interface** - Hide options they don't need
- **Granular control** - Configure permissions per account

---

### 📝 Message Editing & Deletion *(Evolution/WAHA/Uazapi)*

Edit and delete WhatsApp messages after sending:

**Edit Messages:**

- **15-minute window** - Edit sent messages within 15 minutes
- **Sync updates** - Incoming edits sync automatically from WhatsApp Cloud and Notificame without duplicating the original message
- **Group sender context** - Incoming group edits keep the participant number and name visible below the edit indicator
- **Edit indicator** - Edited messages show "edited" label
- **All providers** - Works with Evolution, WAHA, and Uazapi

**Delete Messages:**

- **Delete for everyone** - Remove sent messages
- **Confirmation** - Safety confirmation before deletion
- **Status update** - Deleted messages show as deleted in conversation

---

### 🧩 Sales Kanban Board *(Mega)*

Manage commercial opportunities in a visual pipeline connected to omnichannel conversation context:

- **Funnels with customizable stages** - Create multiple funnels and set a default stage per funnel
- **Board and list views** - Switch between visual pipeline and operational list depending on team workflow
- **Complete list through progressive loading** - List view loads 30 opportunities per page and can fetch later pages without losing cards already shown
- **List search and filters over the whole funnel** - In list view, search and filters (including dates) look through every card of the funnel, not only the ones already loaded, and keep loading results 30 at a time
- **Advanced inbox/channel/activity filters** - Segment opportunities by origin and recent movement
- **Label-based filtering** - Filter by conversation labels in board and list views, including stage metrics
- **Per-user column visibility** - Show or hide columns and persist preferences locally
- **360 item workspace** - Includes checklist, notes, attachments, assigned agents, offers, and custom attributes
- **Global fields through the API** - Integrations can create or update funnel attributes with a structured array or a name-keyed object; the object uses only fields configured on the funnel
- **Readable long notes** - Open full formatted text and attachments in a scrollable detail view, with direct editing when permitted
- **Relationship search** - Find linked conversations with remote search while managing item relationships
- **Account default currency** - The board baseline currency is defined at account settings level (`default_currency`)
- **Account time zone** - Settings → General picks the account time zone (`settings.reporting_timezone`, UTC when blank) used by reports, tasks, Flow Builder schedules and recurring scheduled messages
- **Consistent currency across Kanban** - Cards, details, offers, activities, and history follow offer → item → account → locale precedence; each side of a historical change keeps its own currency
- **Per-currency stage totals** - Stage headers keep PYG, USD, EUR, and every other currency separate without conversion or cross-currency addition; the tooltip covers all filtered offers even when pagination has not loaded every card
- **Custom offer currency override** - In manual product/service offers, users can choose currency per offer
- **No currency on items without offers** - If an item has no offers, value is shown as a placeholder and is excluded from monetary totals
- **Faithful Kanban report downloads** - CSV reports include every authorized card matching the active funnel, date, agent, and inbox filters, preserve free text safely for spreadsheets, and use the selected language, configured stage names, and card/account currency
- **Labels at creation and from the item card** - Select existing labels while creating an item, or add and remove them directly from its card
- **Native contact and conversation relationships** - Keep sales context linked to the real customer chat thread
- **Google Calendar event bridge** - Scheduled or deadline-based items can create MEGA calendar events when account-level Kanban sync is enabled
- **Stage-based automations** - Trigger actions when entering or moving stages, including quick messages and operational rules
- **No-response stage follow-ups** - After a configured wait, send text or uploaded multimedia to the item's primary conversation only when the contact has not replied. The message editor autocompletes ReplyBox variables for contact, conversation, inbox, agent, and custom-attribute data. For configured WhatsApp Cloud inboxes, approved templates are also available and free-form sends remain blocked outside the 24-hour window
- **Group-free entry** - Each entry stage can exclude WhatsApp group conversations so no item is created and its automatic flows do not start
- **Automatic template delivery** - Automatic stage templates are sent once per item by default, preventing duplicate customer messages when an item re-enters a stage. The editor suggests variables such as `{{contact.name}}` when typing `{{` and resolves them when sent; a template can explicitly opt in to resend on every re-entry; manual quick messages remain unrestricted
- **Quick message from the card** - With the funnel's *Quick message* switch on, the card menu (⋯), the card drawer and the phone detail screen offer *Quick message*: it sends one of the stage templates that apply to the card, or a custom message, to its linked conversation without opening it
- **Kanban alerts** - Notify selected team members and assigned agents from stage automation, and the assigned agent when a checklist task reaches its due date; dismissed alerts reappear after the funnel-configured interval only while that task remains pending. Alerts are grouped in a non-blocking banner and do not send email
- **Optimized queries** - Funnel selector counts use lightweight queries; statistics preserve totals by currency and offer, while searches and reports reuse related data to reduce repeated queries.
- **Deadlines on creation or duplication** - Checklist tasks with a due date and assignee schedule their alert when saved, including when copied to another card; copied tasks notify from the destination card.
- **Real-time synchronization** - Stage and item updates propagate instantly to chat list and contact panel
- **Contact-wide open deals** - Each funnel can opt in from Advanced Configuration to show its open Kanban items across every conversation of the current contact; the option is disabled by default, keeps existing visibility rules, and identifies related conversations
- **Authorized panels** - The conversation panel Kanban block and sidebar entry are hidden when the user has no visible items and no accessible funnels to add deals
- **Kanban details from conversations** - A card displays one channel icon for each linked inbox type: it opens that channel's only conversation directly or a selector limited to that channel when several exist, without reloading the board; on mobile, item details show business information first and open the item profile in a side panel. The drawer contact panel hides previous conversations to preserve the item context
- **Unread messages on the card** - Each channel button shows how many unread incoming messages its linked conversations have, using the same rule as the conversation list and counting only conversations the user can see. When several conversations share a channel (for example two WhatsApp inboxes), the button adds up their counts and the selector shows each one, unread first. The buttons line up with the actions menu and stay visible when the card is collapsed. The count goes up in real time with each incoming message and resets when the conversation is opened from the board. Each funnel can turn it off in Advanced Configuration → Card
- **Realtime Kanban access** - Adding or removing funnel agents refreshes the sidebar, funnel list and visible items without a reload
- **Multiple linked conversations** - A single Kanban item can relate to several conversations; the first remains the primary link and additional conversations appear in the relationships tab, with the picker limited to the funnel inboxes and channel icons shown
- **Conversation link history** - Each linked or unlinked conversation gets its own event; links show the inbox from the same account and action text follows the interface language
- **One open opportunity per contact and funnel** - Automatic creation reuses the contact's open item and links new Instagram, WhatsApp, or other enabled-inbox conversations to it; each funnel is evaluated separately, and a won or lost opportunity allows a new one
- **History without broken links** - If a linked conversation is deleted, the Kanban item is kept as history and the link is cleared
- **Role- and permission-based Kanban access** - Administrators manage every funnel and item; agents and roles with `kanban_view` work with authorized items; `kanban_manage` also creates and edits assigned funnels, without deleting, setting the default, or changing visibility
- **Administrator self-assignment** - Administrators can assign or remove themselves from any item even when absent from the funnel agents or inboxes; every other user keeps the normal eligibility rules
- **Controlled item visibility** - The creator can always view an item; with a valid linked conversation, its assignee can view it only when also selected on the funnel, and manually assigned item agents can view it; a stale link is visible only to the administrator and creator. The funnel's `everyone` mode lets every funnel agent view every item, while `assigned_only` restricts visibility to authorized agents.
- **Flexible funnel agents** - Any account member with Kanban access can be added to a funnel, with or without inboxes selected; a custom role requires `kanban_view` or `kanban_manage`. With configured inboxes, manual item assignments require access to at least one. Moving an item automatically adds its assignees to the destination funnel without changing inbox permissions
- **Protected configuration and automations** - Global configuration is read-only for Kanban actors; its changes and global automations are administrator-only. `kanban_manage` administers only the funnels assigned to that user

---

### 📊 Year in Review

Annual statistics and insights for your account:

- **Annual summary** - Complete overview of your year's performance
- **Key metrics** - Conversations, messages, resolution times
- **Busiest day** - Identify your peak activity day
- **Personality type** - Fun categorization based on your work patterns
- **Interactive slides** - Engaging presentation of your stats
- **Cached results** - Fast loading for repeated views
- **Share** - Share your achievements with your team

---

### 💳 Native subscriptions (plans, add-ons and AI Actions)

Operators define and sell their own plans from Super Admin, without depending on a fixed catalog. It works the same on cloud and self-hosted installations.

**Plans you define**

- Each plan sets included agents and inboxes, enabled features, monthly AI Actions and Captain documents.
- Monthly, semiannual and yearly prices per currency (USD, BRL, EUR), entered by the operator; "Suggest from USD" fills them using today's exchange rate.
- Free trial configurable per plan (15 days by default), with no card required and reminders 7, 3 and 1 day before it ends.
- **Duplicate plan** - From a plan's menu, "Duplicate" creates an independent copy with its limits, prices, gateways, features, add-ons and AI models, so variations do not have to be set up from scratch. The copy is created inactive, named "(copy)", "(copy 2)"…, and opens for editing before it is turned on.
- After signup, the administrator sees an activation screen with the account, 3-step progress and log out, a monthly/semiannual/yearly toggle (only the intervals the plans are priced in), plan cards and a comparison table grouped by team, channels, AI, productivity and platform. The default plan comes first and highlighted, with its payment methods and 4 summarized benefits. Every public plan with trial days offers its own trial: its card shows the free days and their end date, the start-trial button before "Pay now" and the terms below the buttons. The account is suspended if the trial ends unpaid. Without a default plan the public catalog is shown; when no plan has trial days, payment is required for activation. The signup language carries through to Billing.

**Payments with Stripe and Asaas**

- Payment methods configured in Super Admin: Stripe (international) and Asaas (Brazil, with the fiscal document issued by Asaas). Asaas subscriptions can be paid by card, PIX or boleto: Super Admin picks which ones the gateway offers, the customer chooses when subscribing and can switch later, and PIX and boleto customers pay each charge, add-ons and upgrades included, on its invoice page.
- **Custom payment method** - Any provider with an HTTP API is connected from Super Admin without waiting for a native integration: fill in how to authenticate (API key or OAuth with a Connect button), the request that creates the charge with variables such as `{{amount}}` or `{{customer.tax_id}}`, where the id and payment link come back, and the webhook URL Mega gives you to paste in the provider. For providers without webhooks, Mega checks the status every 10 minutes. Every charge (subscription, renewal, proration, add-ons, AI Actions, service charges) is a payment link; the Test button sends a real charge and shows the answer to set up the fields.
- Each currency points to one gateway; the country chosen at signup sets the account currency (Brazil in BRL, the euro area in EUR, every other country in the default currency, USD), as long as a gateway charges it and plans are priced in it; no conversion at charge time.
- Upgrades are charged immediately with proration; downgrades apply at the end of the period and never delete agents or inboxes.
- **Account-exclusive plans** - Super Admin reserves a plan for one or more accounts, for example with a negotiated price: only those accounts see it in Billing and subscribe through the gateway, with add-ons and plan changes. Other accounts neither see it nor can subscribe by calling the API.

**Add-ons and AI Actions packages**

- Recurring add-ons are charged at their full price when bought, whatever is left of the period, and from the next renewal they are added to the plan in the same invoice.
- Removing an add-on keeps it until the end of the paid period, with no refund; the billing page shows "Removed on <date>" with a **Keep** button that cancels the removal until then. A removal that would leave more agents, inboxes, calls or WAHA inboxes in use than what stays is refused. An add-on the account holds stays listed even once it is no longer sold, so it can always be removed. Super Admin sees the scheduled removals on the account billing tab and can remove or keep an add-on from there.
- An add-on another held add-on depends on cannot be removed either (WAHA while WAHA calls remain): remove the dependent one first, or both together. When the account moves to a plan that already includes an add-on's feature, that add-on is removed by itself at the end of the period and is not charged again.
- Add-ons sold by units show how many are in use ("In use: 1 of 2") on the billing page and on the account page in Super Admin.
- A single add-on catalog that each plan can offer with an optional maximum, with four types: extra agent, extra inbox, **feature** (turns on the feature picked when creating it, charged with the subscription like extra agents and hidden on plans that already include it) and **custom** (free text for any service the operator sells, charged monthly with the subscription or as a one-time payment).
- A feature add-on can also be sold by units: **per inbox** (WAHA calls: each unit turns calls on in one inbox; the others show them locked with "Buy another unit") or **with its own inbox** (WhatsApp WAHA, Evolution or Uazapi: each unit adds an inbox only that provider can use, on top of the plan limit, and turns the provider on). An add-on can require another feature (calls are only offered to accounts with WAHA), and units in use cannot be removed until the inboxes are freed. Plans, the regular inbox limit and Super Admin exceptions keep working as before.
- When the account has no inboxes left, the new inbox screen shows every channel locked ("No inboxes left") with a banner to buy an extra inbox; WhatsApp stays open only for the providers whose add-on still has a free inbox.
- One-time custom add-ons are bought from the billing page choosing the quantity; once paid they show up in Super Admin under "Pending deliveries" and in the billing dashboard's attention panel until the operator marks them delivered.
- One-off AI Actions packages that add to the monthly balance, roll over and expire after 90 days.
- **One price per model** - Each AI model has a single price in AI Actions, the one the operator sets in AI Providers (or the model's default). It is what the account sees when picking a model in Captain, what the plan form shows and what is charged: every feature charges the model it really used.
- **Large jobs charge what they do** - Copilot workflows charge each step, each reviewed conversation and each screening decision; Mega Assistant conversation reviews, each reviewed conversation; call transcription, each model pass; audio notes, per started minute; voice, per 5-minute block.
- **Visible negative balance** - Work that already started finishes even when the balance runs out; if it costs more than what was left, the balance goes negative, shows on the billing page and in Super Admin, and is taken first from the next plan, package or adjustment. With a balance at zero or below no new AI work starts, including work that is not charged on its own (classifier suggestions, generated voice, FAQs, contact notes, dictation).
- Add-ons do not add AI Actions: AI Actions come from the plan, packages and Super Admin adjustments.
- On a self-hosted installation, accounts without a native plan are not charged AI Actions and see no credits when picking a model.
- Usage meter per source (plan, packages and adjustments) on the billing page.
- Payment history appears before the plan catalog, showing the four most recent matching invoices per page with combined status and concept filters.

**Administration**

- Manual plan assignment: courtesy, manual payment and trial, individually or in bulk with a per-account impact preview.
- Existing accounts stay in Legacy mode: they keep their current features and limits until a plan is assigned.
- Past due: 7 grace days with a persistent notice for administrators and, once elapsed, suspension with automatic reactivation on payment.
- **Service charges** - From the account page (or the Platform API), Super Admin creates a one-off charge for any amount, such as consulting, onboarding or a data migration, with a description, an optional due date and an internal note. The account administrators get an email, see a banner across the app and pay it from the Billing banner or the payment history through the gateway of their currency (Stripe, Asaas with card, PIX or boleto, dLocal Go or PayPal). If it is not paid it turns overdue without suspending the account; while unpaid it can be voided. The Billing page and the banners update in real time when a charge is created, paid or voided or the subscription changes.
- **AI usage** - Super Admin shows charged AI Actions, calls, tokens, and provider cost by period, provider, account, model, and feature, including a monthly forecast and cost per action.
- **AI result** - The usage dashboard, the billing summary and each account page show the same profit and loss in USD: collected from packages, estimated from plans, courtesy credits kept apart (never counted as income), usage that consumed no AI Actions, and the final result. It includes each package's profitability with its minimum price, the AI Actions suggested per model from its real cost (also next to each model in AI Providers), and Mega Assistant broken down by feature (Captain, reports, contacts, conversations, and more). The AI usage (Summary, Profitability, Accounts, Breakdown) and billing (Summary, Plans, AI) dashboards are organized in tabs. Billing explains which figures are current versus monthly, separates paying subscriptions from the installation-wide subscriber base, and shows actions alongside credits used. Its AI tab uses only the month selector because its results cover the whole installation in USD. The accounts list has search and pagination. On each account page, every invoice says what it charged for (plan and interval, add-ons and quantities, AI Actions package, or the plan a proration moved to), with filters by concept and status, and the AI Actions ledger has search, filters by movement, bucket, feature and dates, and pagination. The AI usage summary leads with result, income and total LLM cost, then separates charged actions, credits used and courtesy credits. Its tabs explain which figures follow the selected period and which use current prices or the last 30 days.
- **Revenue** - Super Admin shows MRR per currency (semiannual and yearly prices spread over 6 and 12 months), collections and receivables, the 12-month collection trend split into subscriptions, add-ons, AI Actions and services, MRR by plan, subscriptions by status, collections by gateway and invoice type, subscriber movements, and the oldest overdue invoices.

---

## 🔐 Security & Compliance

- **More complete audit trail** - Sign-ins and sign-outs show the IP location and the suspension history shows who suspended each account
- **Safe HTML content** - Markdown messages, Captain instructions, and signup terms links filter dangerous content while retaining internal tool links and trusted article embeds.
- **Impersonation notice** - When a Super Admin signs in as another user, the dashboard says so with a banner and lets them leave in one click
- **Channel connection for administrators only** - Only account administrators can connect or reconnect Facebook pages and WhatsApp numbers (embedded signup, WAHA and Evolution)
- **Names always as text** - Contact names (also when merging contacts), canned responses, macros and notification content are shown as text and never interpreted as HTML

### Authentication

- **2FA/MFA** - Two-factor authentication
- **Super Admin 2FA** - Super admins who have two-factor authentication turned on enter the code from their app after the password. The code step expires after 5 minutes and is cancelled after 5 wrong codes. The console has no password recovery, sign-up or confirmation pages of its own.
- **Expiring reset links** - Password reset links expire after 6 hours; invitation links after 7 days. If the new password is rejected, the invitation stays pending.
- **Email change needs the password** - Changing the profile email asks for the current password, just like changing the password; the field appears when the email is edited.
- **Enforce 2FA per account** - From Settings → Security (available on every installation type), administrators can require two-factor authentication for every member. Members without it set it up right on the login page (QR code, code and backup codes) at their next password sign-in; Google and SAML sign-ins are exempt, and members cannot turn their own 2FA off while it is required. API, MCP and OAuth tokens of members who have not enrolled stop working for that account until they do
- **New-device verification (Cloud)** - When enabled, password sign-ins from an unrecognized device require a six-digit email code. Verified devices can be trusted for 30 days; changing the password or email revokes that trust. SSO and existing 2FA sign-ins keep their own flows.
- **SAML/SSO** - Enterprise Single Sign-On
- **API Tokens** - Secure programmatic access
- **Suspended account support** - Suspended users see the policy notice with a direct contact support action; Cloud administrators can also open billing to settle payment and restore access. Super administrators record a category and reason for each suspension and can review or correct the latest entry from the account details.
- **Scheduled subscription cancellation** - Cloud Billing shows the date a Stripe subscription will end and keeps the plan active until that billing-period boundary.
- **Confirmation resend** - Super administrators can resend a pending user's confirmation email from their details without exposing links or tokens.

### Privacy

- **GDPR Ready** - Regulatory compliance
- **Data deletion** - Right to be forgotten
- **Account deletion from Super Admin** - Removes users who belonged only to that account; keeps shared users and Super Admins
- **Export** - Data portability

### Infrastructure

- **Encryption in transit** - Mandatory HTTPS
- **Encryption at rest** - Protected data
- **Auto backups** - Disaster recovery
- **Queue-based worker autoscaling** - Optional CloudWatch publishing of Sidekiq queue latency, depth, enqueued jobs, and worker utilization for backlog-driven worker capacity
- **Queues without a consumer** - Super Admin alert and log/Sentry error when Sidekiq jobs wait in a queue no worker reads, such as a new queue missing from a split Sidekiq setup
- **License protection** *(Mega)* - Integrity verification to strengthen deployment control
- **Release observability** - Better release-level error traceability in monitoring
- **Super Admin in your language** *(Mega)* - Each super administrator picks English, Spanish, or Portuguese (Brazil) from the sidebar; the preference is shared with their agent dashboard profile

---

## 📱 Applications

### Progressive Web App (PWA) *(Mega)*

MEGA works as a full **Progressive Web App**: install it on any device and get a native app-like experience without going through app stores.

**Installation & Native Experience:**

- **One-tap install** - Smart banner automatically appears on mobile devices inviting users to install the app
- **Desktop and mobile** - Works on Chrome, Edge, Safari (iOS/macOS) and any PWA-compatible browser
- **Full screen** - Runs in standalone mode, without the browser address bar
- **Conversation list gestures** - On phones, swiping a conversation left shows Assign (choose agent or team first), Stage when it has an open deal, Snooze when it is open, and Resolve; swiping it right shows Delete (administrators only), which asks for confirmation before deleting it; holding it selects it, as in WhatsApp, and the top bar adds Pin/Unpin and Delete (administrators only, with confirmation) next to the bottom bar actions
- **Fast custom splash screen** - Branded loading screen that clears as soon as Vue paints the interface, with a safety timeout if startup fails
- **Loading skeletons everywhere** - At any screen width, each page shows the shape of its content while it loads; the conversation screen (list, chat and contact panel) appears all at once when everything is ready, and startup remembers whether the contact panel was open
- **Quick shortcuts** - Access Conversations or Notifications directly from the app icon's context menu
- **Dynamic icon** - The app icon is generated from the configured thumbnail logo, falling back to the notification icon, in all required sizes (48px to 512px)
- **Configurable icon background** - Use a custom color for the installable icon while keeping white as the default
- **Monochrome badge** - Optimized badge icon with monochrome silhouette for system notifications

**Advanced Push Notifications:**

- **Native push notifications** - Receive instant alerts even with the app closed, directly in the operating system
- **Browser tab indicator** - If a message arrives while the tab is hidden or unfocused, the favicon switches to the notification icon and returns to normal when the user comes back
- **Inline quick reply** - Reply to messages directly from the notification without opening the app
- **Mark as read** - Mark notifications as read from the notification itself with a single tap
- **Message stacking** - Messages from the same conversation stack into a single notification (WhatsApp-style) showing up to 10 messages
- **Unread counter** - The app icon badge shows the exact number of unread notifications
- **Accurate cache timestamps** - Consistent Service Worker asset invalidation to avoid stale resources
- **Smart activation** - Automatic prompt when opening the PWA for the first time to enable notifications with pre-configured flags (assignment, mention, new message)
- **Reliable subscription lifecycle** - Per-user device opt-out survives reloads, logout revokes the browser binding, and changed VAPID keys are renewed automatically
- **Configurable sound** - Audio alerts that work even on iOS, with automatic AudioContext unlock on first touch
- **Deferred sound** - If the app is in the background and can't play audio, it automatically plays when you return to the app
- **Vibration** - Custom vibration pattern on mobile devices when receiving notifications

**Offline Support:**

- **Custom offline page** - When there's no connection, displays an elegant page with your brand logo and retry button
- **Smart caching** - Only fingerprinted Vite assets are cached, with a bounded runtime cache for fast repeat loading
- **Safe offline navigation** - Authenticated pages and APIs are never persisted; unavailable navigation uses the public offline page
- **Automatic cleanup** - The Service Worker removes outdated versions and limits retained fingerprinted assets

**Brand Customization (White-label):**

- **Dynamic manifest** - The PWA manifest is dynamically generated with your installation's name, description, colors and logo
- **SVG support** - SVG logos are converted to high-resolution PNG through librsvg or libvips before final asset composition
- **Apple icons** - Automatic generation of apple-touch-icons in all sizes required by iOS
- **iOS splash screens** - 14 pre-generated splash screen resolutions for all iPhone and iPad models
- **Brand colors** - The manifest's theme-color and background-color use your configured primary color

### Mobile Application *(In development)*

- **iOS and Android** - Serve customers from your phone
- **Push notifications** - Instant alerts for new conversations
- **Full functionality** - All tools in your pocket

---

## 📞 Support & Resources

- **Help Center** - Complete documentation and step-by-step guides
- **Active community** - Connect with other users
- **Enterprise Support** - Priority, dedicated service for enterprise customers

---

*MEGA - Transforming how businesses communicate with their customers.*

**© 2026 MEGA - All rights reserved**

- **Bot handoff alerts** - A pending conversation handed to a human triggers the sound and browser tab badge after a short delay. Existing audio assignment and visibility settings apply; Captain private notes do not trigger a second alert.
