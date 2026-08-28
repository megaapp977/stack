---
name: dashboard-script-creator
description: Create or review Mega Dashboard Scripts for developers using AI without repository access. Produces safe, SPA-aware, ready-to-paste snippets and asks only for the dashboard context it needs. Use when the user says "crear dashboard script", "script para dashboard", "customizar dashboard", "super_admin/dashboard_scripts", or "dashboard scripts".
---

# Dashboard Script Creator

## Purpose

Help a developer create a small Dashboard Script without needing access to Mega source code. The result should be easy to paste into Super Admin, safe to run on a Vue single-page dashboard, and clear about any uncertainty in its selector. It can also propose a Mega API integration when a UI-only script is not enough.

Use this for focused interface customization: a visual marker, a small button, a shortcut, or controlled show/hide behavior. For a complete module, data integration, or independent screen, recommend a Dashboard App instead.

## Classify Before Building

Classify the request before selecting a pattern:

| Extension type | Typical outcome |
| --- | --- |
| Cosmetic or navigation | Dashboard Script. |
| Local contextual action | Dashboard Script when it only changes local UI or opens an approved URL. |
| Read-only external data | Dashboard Script plus approved same-origin backend/proxy, or Dashboard App. |
| Data creation, updates, automation, or business workflow | Dashboard App plus Mega API and an approved backend boundary. |
| Full screen, multi-step UI, complex state, uploads, independent testing, or many network operations | Dashboard App. |

Also state the risk: **low** for local visual DOM changes, **medium** for dynamic lifecycle or approved same-origin reads, and **high** for writes, external systems, sensitive data, authentication, permissions, or business-critical controls. Do not implement high-risk behavior as a browser-only script.

## What the AI Can Assume

- Dashboard Scripts are trusted HTML/JavaScript snippets configured by Super Admin. They run in dashboard pages for users who can access them.
- Scripts are delivered globally. Visibility by account is enforced inside the script from the URL.
- The dashboard is a SPA: navigation can replace DOM nodes without reloading the document.
- The editor preview opens a real dashboard page in an iframe, with desktop and 375px mobile-width views. It is a useful visual smoke test, not a sandbox or full integration test.
- Script content must never contain secrets, credentials, private data, or unapproved third-party tracking/script loads.

Do not mention internal source paths, require repository searches, or say a selector was “verified in source”. The developer using this skill does not have that access.

## Account Visibility

The AI must ask for one of these visibility modes and implement it before any DOM work, listener, observer, or API call:

| Mode | Configuration | Result |
| --- | --- | --- |
| All accounts | "ALLOWED_ACCOUNT_IDS = null" | Visible on every account dashboard route. |
| One account | "ALLOWED_ACCOUNT_IDS = [123]" | Visible only for account 123. |
| Selected accounts | "ALLOWED_ACCOUNT_IDS = [123, 456, 789]" | Visible only for the listed accounts. |
| All except selected accounts | "ALLOWED_ACCOUNT_IDS = null" and "EXCLUDED_ACCOUNT_IDS = [123, 456]" | Visible on every account except those listed. |

The guard reads the account id from "/app/accounts/:id/...". It must return false outside an account route. This prevents a global Dashboard Script from changing a login, Super Admin, or other non-account page.

Do not describe this as server-side access control: the script is still delivered globally. Use a true account-scoped Dashboard App or backend authorization for data protection, permission enforcement, or secret-bearing functionality.

## Platform Visual Injection Map

These are the strategic visual surfaces that teams most often customize. They are **requested UI locations**, not pre-known CSS selectors: ask for a screenshot, copied HTML, or an existing selector before generating a concrete selector.

| Visual surface | Good customizations | Injection strategy and limits |
| --- | --- | --- |
| Primary sidebar | Link to an internal tool, indicator, compact embedded-app launcher. | Insert one named navigation item before/after a confirmed existing item. It must be idempotent; never rewrite or reorder Mega navigation. |
| Top bar / global header | Status indicator, shortcut, notifications/help launcher. | Keep it compact and global only when the feature belongs on every dashboard route. Avoid covering account controls. |
| Inbox and conversation list | Badges, filters, quick links, summary counters. | Mount in a confirmed list header or card container. Treat list rows as recycled/re-rendered; do not alter selection, assignment, or unread behavior. |
| Conversation header | Contextual action, integration launcher, read-only status. | Mount beside a confirmed existing action. Never replace the core resolve, assign, close, or search controls. |
| Reply Box / composer | Template helper, writing shortcut, approved external-tool launcher, contextual hint. | Mount beside the confirmed composer toolbar; preserve focus, keyboard shortcuts, attachments, drafts, and the Send action. Do not intercept or rewrite message content unless explicitly requested. |
| Message bubbles / conversation timeline | Small visual marker, metadata, copy helper, external record link. | Add a node-level marker to each processed bubble. Do not modify the message body, delivery state, media, reactions, or agent/customer content without explicit authorization. |
| Contact Panel / conversation side panel | CRM shortcut, customer indicator, compact external-profile link, read-only summary. | Mount inside a confirmed panel section and reapply when the selected conversation/contact changes. Do not overwrite contact fields or panel actions. |
| Kanban board | Summary, quick filter, board-specific link, visual stage helper. | Mount in a board header or confirmed column container. Do not change drag/drop, stage ordering, totals, or card workflow unless explicitly requested. |
| Contacts list and contact details | Search helper, tag/CRM link, data indicator. | Scope to contact routes and keep per-contact changes idempotent. Prefer API-backed data for anything that must persist. |
| Main dashboard page | Compact action, notice, or panel. | Scope it by the current URL so it does not appear on unrelated pages. |
| Settings / integrations | Focused helper, setup launcher, support link. | Use a specific route guard. Prefer a Dashboard App for a multi-step configuration experience. |
| Modal, drawer, popover | Small enhancement to a specific dialog. | Attach only after the named dialog opens; clean up when it closes. Do not use a modal as a permanent mount point. |
| Floating action | One high-value action when no natural container exists. | Keep it unobtrusive, mobile-aware, and removable; do not cover the Reply Box or conversation controls. |

For a primary-sidebar request, the AI should return a named button/link that it appends to a selector supplied by the developer, plus a route guard. It must not guess a sidebar selector from the name “sidebar”. The same evidence rule applies to Reply Box, Contact Panel, and every other surface.

## Choose the Right Runtime Pattern

Select the smallest pattern that matches the UI lifecycle:

| Situation | Pattern |
| --- | --- |
| A static item already exists when the page loads | Run once; no observer. |
| The target appears after dashboard navigation | Observe the narrowest confirmed container and coalesce with "requestAnimationFrame". |
| A list has repeated cards or message bubbles | Process each node once with a dedicated dataset marker. |
| A modal, drawer, or popover is temporary | Mount while it exists; remove listeners and temporary nodes when it closes. |
| The customization needs its own full screen, state, or data flow | Do not grow the script further; recommend Dashboard App. |

Never use an observer as a substitute for an unknown selector. Confirm the selector first, then observe only if that selector is rendered late or replaced.

## Lifecycle and Cleanup

Use the simple static baseline for a one-shot feature. A script that owns persistent listeners, timers, observers, subscriptions, or DOM nodes must use the SPA baseline and provide a destroy function.

- Keep script state in its unique window state object only for lifecycle resources, not business data.
- Mark initialization complete only after bootstrap succeeds. If bootstrap fails, remove the state key so a corrected script can initialize.
- Prefer AbortController for removable event listeners.
- The destroy function must disconnect owned observers, abort listeners, clear timers, remove only owned DOM nodes, and delete the state key.
- A route-dependent SPA enhancement may keep one narrow observer alive. A one-shot observer must disconnect after successful mount; do not use a universal fixed timeout as the SPA lifecycle strategy.

The handoff must say how to invoke cleanup during testing:

~~~js
window.__megaDashboardFeatureNameV1?.destroy?.()
~~~

## Minimal Discovery

Ask for only the missing context that materially changes the script:

1. What should happen, and where should it appear: sidebar, header, inbox/conversation list, conversation header, Reply Box, message bubble, Contact Panel, Kanban, contacts, settings, modal, or floating action?
2. Which accounts can see it: every account, one account id, a list of account ids, or every account except a list?
3. Is it desktop, mobile, or both?
4. A screenshot, the visible label, or a copied HTML fragment for the target control when a reliable selector is not already provided.

If this information is unavailable, create the smallest safe draft with a clearly marked selector placeholder and state exactly what must be replaced. Do not invent selectors, internal component names, or API contracts.

## Browser Evidence Packet

When the developer can open the dashboard but cannot access source code, ask for this lightweight packet:

1. A screenshot showing the desired insertion point.
2. The current account id and dashboard URL.
3. The nearest parent element's copied outer HTML from browser DevTools, with names, message content, tokens, and private values removed.
4. Whether the target stays visible during navigation or is recreated when the conversation/contact changes.

Use only the supplied structural attributes to create the selector. If copied HTML has sensitive data, the developer must redact it before sharing it with the AI.

## Interaction, Accessibility, and Language

For any UI that the script creates:

- Use a semantic "button" for actions and an "a" element only for navigation.
- Add an accessible name with visible text or "aria-label"; keep keyboard focus visible.
- Do not steal focus from Reply Box, modal inputs, or search fields.
- Configure visible labels in a small "LABELS" object when more than one language is needed; do not hardcode a selector based on translated text.
- Reuse nearby visual conventions where possible. Keep custom UI compact and avoid covering Send, navigation, or account controls.

For keyboard shortcuts, require an explicit user request and ignore keystrokes from input, textarea, select, or contenteditable elements.

## Choosing the Right Extension

Use a **Dashboard Script** when the change is a small DOM customization with no backend state or external data flow.

Recommend a **Dashboard App** when the request needs a substantial interface, a third-party tool, durable data exchange, dedicated permissions, or conversation/contact/agent context. It is a more suitable boundary than injecting a large application into the dashboard DOM.

## Mega API Integrations

When the requested behavior needs data creation, lookup, updates, or automation, propose Mega API as the integration path instead of inventing browser-only state.

Use the official project reference: [Mega API Postman collection](https://github.com/megaapp977/stack/blob/main/API-MEGA/Mega%20API.postman_collection.json).

The AI should tell the developer to:

1. Import the collection into Postman.
2. Configure "host" with the installation URL (without a trailing slash), "account_id", and "api_access_token".
3. Use the collection’s Application API folders for account-scoped operations. Platform APIs require the separate "platform_api_access_token"; public APIs do not inherit authentication.
4. Start with a read request, then use the matching create/update request only after confirming the payload and side effect.

The collection is the endpoint and payload reference. The AI must not invent endpoint paths or request bodies when the collection does not show them.

**Security boundary:** never put "api_access_token" or "platform_api_access_token" in a Dashboard Script, browser storage, URL, or HTML. For a script-driven UI, route authenticated API work through a trusted backend/proxy, or use a Dashboard App/approved integration architecture. The script may call only an explicitly approved same-origin endpoint that does not expose credentials.

## Embedded Panels and External Tools

An iframe/panel is appropriate only for a trusted tool that needs a contained interface. Before generating one, confirm:

1. The external URL is HTTPS and owned/approved by the organization.
2. The tool allows embedding from the Mega domain through its frame policy.
3. No Mega API token, session secret, or private conversation/contact payload is added to the iframe URL.
4. Any "postMessage" exchange validates the sender origin and accepts only the minimal expected message shape.

If the external tool needs conversation/contact/agent context or secure authenticated data exchange, prefer a Dashboard App or an approved backend integration.

## Selector Rules

Choose selectors from evidence supplied by the developer, in this order:

1. An id or "data-*" attribute in a copied HTML fragment.
2. A distinctive "aria-label", role, name, or short semantic class shown in the dashboard.
3. A relationship to visible text only when the dashboard language is fixed and the user accepts that dependency.

Never use a long chain of Tailwind classes, positional selectors such as ":nth-child", "querySelectorAll('*')", Vue internals, or test-only attributes unless the developer explicitly confirmed they exist in the live dashboard.

If a selector is inferred from a screenshot rather than copied HTML, label it as a hypothesis and give the developer one simple browser-console check:

~~~js
document.querySelector('YOUR_SELECTOR')
document.querySelectorAll('YOUR_SELECTOR').length
~~~

For a single mount point, one match is ideal. Zero means the target was not found; more than one means the selector is probably too broad.

Keep these selectors distinct:

- **Target selector:** identifies the platform element or repeated card to enhance.
- **Mount selector:** identifies the specific child/container where the new owned node will be inserted.
- **Owned node marker:** a unique id or data-mega-dashboard-owned="feature-name" on every node created by the script.

Use a stable record id only when the developer confirms one exists. Conversation rows, message bubbles, cards, and contact panels are ephemeral DOM nodes; never assume their position or lifetime represents a durable record. The DOM dataset is for rendering/idempotence only; durable business state belongs in Mega/backend storage.

## Safe DOM and Network Rules

- Prefer additive changes with append, prepend, or insertAdjacentElement; do not replace platform-owned nodes unless the developer explicitly accepts that compatibility risk.
- Create dynamic UI with document.createElement, textContent, and setAttribute.
- Never interpolate API data, contact data, messages, user input, or URL values into innerHTML.
- If styling is needed, scope it to the script's owned root marker. Do not style body, generic button elements, or broad platform selectors globally.
- Network access defaults to an explicitly approved same-origin endpoint. Do not send Mega account, contact, conversation, message, or agent data to a third-party origin without explicit approval.
- For a link opened in a new tab, use rel="noopener noreferrer".

## Do Not Do

Do not:

- invent selectors, API endpoints, request payloads, or permission behavior;
- patch or intercept fetch, XMLHttpRequest, WebSocket, EventSource, browser prototypes, history navigation, router internals, Vue internals, stores, or private event buses;
- use long Tailwind selector chains, positional selectors for core targets, global DOM scans, or indefinite polling;
- replace Send, Resolve, Assign, search, attachment, navigation, timeline, or Kanban workflow controls unless explicitly requested and risk-assessed;
- keep business state only in DOM, localStorage, or sessionStorage;
- insert untrusted dynamic values with innerHTML;
- place secrets or credentials in any browser-visible value;
- send private Mega data to an unapproved third party.

## Required Script Shape

Every generated script must:

- use a unique "<script data-name=...>" wrapper;
- use a unique global key to initialize once per document;
- mark each changed node with a "dataset" flag;
- return early for an out-of-scope account before adding listeners, observers, DOM changes, or API calls;
- use a narrow, coalesced MutationObserver only when Vue rendering requires it;
- avoid permanent polling and global DOM scans.

Prefer stable semantic selectors, account/route/device guards, additive DOM changes, owned-node markers, textContent, AbortController, narrow observers, requestAnimationFrame coalescing, and approved same-origin backend endpoints.

## Release, Debugging, and Rollback

Every delivery must support a safe rollout:

1. Start with one account allowlist.
2. Enable a "DEBUG" flag only while testing; it may log lifecycle messages but never private data.
3. Test desktop, mobile when relevant, navigation, changing conversations/contacts, and the target account boundaries.
4. Expand the allowlist only after the script is stable.
5. Roll back by disabling or deleting the named Dashboard Script in Super Admin, then reload the dashboard.

Use the unique "data-name" and element id/data marker in the handoff so the developer can identify exactly which customization to disable.

## Baseline A — Static or One-Shot Customization

Use this when the confirmed target exists at initial load and does not need to be recreated after later SPA navigation. It deliberately does not create persistent lifecycle resources.

~~~html
<script data-name="feature-name">
  (() => {
    const SCRIPT_KEY = '__megaDashboardFeatureNameV1';
    if (window[SCRIPT_KEY]?.initialized) return;

    const state = { initialized: false };
    window[SCRIPT_KEY] = state;

    // null means every account dashboard route. Add one or more account ids to limit visibility.
    const ALLOWED_ACCOUNT_IDS = null; // Example: [123] or [123, 456]
    const EXCLUDED_ACCOUNT_IDS = []; // Example: [789]
    const REQUIRED_PATH_PARTS = []; // Empty = any account route. Example: ['/conversations']
    const DEVICE_MODE = 'all'; // 'all', 'desktop', or 'mobile'
    const DEBUG = false;
    const TARGET_SELECTOR = '[data-replace-with-confirmed-anchor]';
    let scheduled = false;

    const debug = (...message) => {
      if (DEBUG) console.debug('[feature-name]', ...message);
    };

    const currentAccountId = () => {
      const match = window.location.pathname.match(/^\/app\/accounts\/(\d+)(?:\/|$)/);
      return match ? Number(match[1]) : null;
    };

    const isInScope = () => {
      const accountId = currentAccountId();
      if (accountId === null) return false;
      if (EXCLUDED_ACCOUNT_IDS.includes(accountId)) return false;
      return ALLOWED_ACCOUNT_IDS === null || ALLOWED_ACCOUNT_IDS.includes(accountId);
    };

    const isRouteAllowed = () =>
      REQUIRED_PATH_PARTS.every(part => window.location.pathname.includes(part));

    const isDeviceAllowed = () => {
      if (DEVICE_MODE === 'mobile') return window.innerWidth <= 768;
      if (DEVICE_MODE === 'desktop') return window.innerWidth > 768;
      return true;
    };

    function applyFeature() {
      if (!isInScope() || !isRouteAllowed() || !isDeviceAllowed()) return;

      const target = document.querySelector(TARGET_SELECTOR);
      if (!target || target.dataset.featureNameApplied === 'true') return;

      target.dataset.featureNameApplied = 'true';
      debug('Applied to target');
      // Add the smallest local DOM change here.
    }

    function scheduleApply() {
      if (scheduled) return;
      scheduled = true;
      requestAnimationFrame(() => {
        scheduled = false;
        applyFeature();
      });
    }

    function bootstrap() {
      scheduleApply();
    }

    function start() {
      try {
        bootstrap();
        state.initialized = true;
      } catch (error) {
        console.error('[Mega Dashboard Script: feature-name]', error);
        delete window[SCRIPT_KEY];
      }
    }

    if (document.readyState === 'loading') {
      document.addEventListener('DOMContentLoaded', start, { once: true });
    } else {
      start();
    }
  })();
</script>
~~~

Replace "feature-name", the global key, "TARGET_SELECTOR", account visibility arrays, required route parts, and device mode.

## Baseline B — SPA Lifecycle Customization

Use this for Reply Box, Conversation Header, Contact Panel, repeated cards, or another confirmed target that Vue replaces during navigation. Replace all placeholders before use.

~~~html
<script data-name="feature-name">
  (() => {
    const SCRIPT_KEY = '__megaDashboardFeatureNameV1';
    if (window[SCRIPT_KEY]?.initialized) return;

    const state = {
      initialized: false,
      controller: new AbortController(),
      observer: null,
      scheduled: false,
      destroy: null,
    };
    window[SCRIPT_KEY] = state;

    const ALLOWED_ACCOUNT_IDS = null;
    const EXCLUDED_ACCOUNT_IDS = [];
    const REQUIRED_PATH_PARTS = ['/conversations'];
    const MOUNT_SELECTOR = '[data-replace-with-confirmed-mount]';
    const OBSERVER_ROOT_SELECTOR = '#app';
    const OWNED_SELECTOR = '[data-mega-dashboard-owned="feature-name"]';
    const DEBUG = false;

    const debug = (...message) => {
      if (DEBUG) console.debug('[feature-name]', ...message);
    };

    const currentAccountId = () => {
      const match = window.location.pathname.match(/^\/app\/accounts\/(\d+)(?:\/|$)/);
      return match ? Number(match[1]) : null;
    };

    const isInScope = () => {
      const accountId = currentAccountId();
      return accountId !== null &&
        !EXCLUDED_ACCOUNT_IDS.includes(accountId) &&
        (ALLOWED_ACCOUNT_IDS === null || ALLOWED_ACCOUNT_IDS.includes(accountId)) &&
        REQUIRED_PATH_PARTS.every(part => window.location.pathname.includes(part));
    };

    function mountFeature() {
      if (!isInScope() || document.querySelector(OWNED_SELECTOR)) return;

      const mount = document.querySelector(MOUNT_SELECTOR);
      if (!mount) return;

      const button = document.createElement('button');
      button.type = 'button';
      button.textContent = 'Feature action';
      button.setAttribute('aria-label', 'Feature action');
      button.dataset.megaDashboardOwned = 'feature-name';
      button.addEventListener('click', () => {
        // Add the approved local action here.
      }, { signal: state.controller.signal });
      mount.append(button);
      debug('Mounted feature');
    }

    function scheduleMount() {
      if (state.scheduled) return;
      state.scheduled = true;
      requestAnimationFrame(() => {
        state.scheduled = false;
        mountFeature();
      });
    }

    function destroy() {
      state.observer?.disconnect();
      state.controller.abort();
      document.querySelectorAll(OWNED_SELECTOR).forEach(node => node.remove());
      delete window[SCRIPT_KEY];
    }

    function bootstrap() {
      const root = document.querySelector(OBSERVER_ROOT_SELECTOR);
      if (!root) return;

      state.observer = new MutationObserver(scheduleMount);
      state.observer.observe(root, { childList: true, subtree: true });
      state.destroy = destroy;
      scheduleMount();
    }

    try {
      bootstrap();
      state.initialized = true;
    } catch (error) {
      console.error('[Mega Dashboard Script: feature-name]', error);
      destroy();
    }
  })();
</script>
~~~

The SPA baseline keeps one narrow observer alive because the target lifecycle requires it. During testing, run "window.__megaDashboardFeatureNameV1?.destroy?.()" to remove only this script's resources and owned nodes.

## Delivery Format

Deliver:

1. Extension type: Dashboard Script or Dashboard App recommended.
2. Risk level: low, medium, or high, with one-sentence rationale.
3. Scope: injection location, accounts, routes, and devices.
4. Selector evidence: target selector, mount selector, source of evidence, uniqueness check, and confidence.
5. A ready-to-paste snippet using Baseline A or Baseline B.
6. A short preview checklist: desktop, mobile if applicable, navigate away/back, no duplicates, correct account/route, and core controls still work.
7. The lifecycle and cleanup strategy, including the destroy command when Baseline B is used.
8. When data is needed: the recommended Mega API collection folder/request, required variables, and whether a trusted backend/proxy is required.
9. The rollout plan: initial account allowlist, validation, and rollback by "data-name".
10. The reason to choose Dashboard App instead, if the request outgrows a local customization.

## Final Checklist

- [ ] No secret, token, private data, remote script, or unapproved external data flow.
- [ ] Dynamic or untrusted values never reach innerHTML.
- [ ] Visibility mode is explicit: all accounts, one account, allowlist, or exclusion list.
- [ ] The account guard runs before side effects and returns false outside an account route.
- [ ] Route and device scope are explicit when the customization is not global.
- [ ] Script is idempotent for SPA navigation.
- [ ] Selector is confirmed or visibly labelled as needing confirmation.
- [ ] Target selector and mount selector are distinct where the component has multiple DOM regions.
- [ ] Owned nodes have a unique marker and platform-owned core nodes are changed additively.
- [ ] Created UI is semantic, keyboard-accessible, and does not steal focus.
- [ ] API tokens remain outside browser-delivered code.
- [ ] Iframe or external-tool use is trusted, HTTPS, and does not leak data through URLs.
- [ ] Baseline B resources have a destroy function and removable event listeners.
- [ ] A one-account rollout and rollback by "data-name" are included.
- [ ] The script is small enough to be maintained as a customization.
