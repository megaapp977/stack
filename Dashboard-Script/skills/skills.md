---
name: dashboard-script-creator
description: Create Dashboard Scripts for Mega using AI agents based on our source code, with safe DOM hooks and idempotent behavior. Use when the user says "crear dashboard script", "script para dashboard", "customizar dashboard", "super_admin/dashboard_scripts", or "dashboard scripts".
---

# Dashboard Script Creator

## Goal

Create Dashboard Scripts that are safe, maintainable, and compatible with the Mega codebase.

This skill is intended for users who want AI agents to generate scripts according to our source code patterns.

Use this workflow for:

- New dashboard customizations (UI tweaks, buttons, shortcuts, hide/show behavior).
- Script creation and adaptation from existing Mega patterns.
- Refactors of existing scripts to reduce fragility and side effects.

## Codebase Facts You Must Respect

### Injection Pipeline

- Dashboard scripts are assembled in `DashboardController#set_dashboard_scripts` from:
  - Active DB records (`DashboardScript.active.ordered.pluck(:content)`).
  - Global config (`DASHBOARD_SCRIPTS`).
- Final content is injected in `app/views/layouts/vueapp.html.erb` with `@dashboard_scripts.html_safe`.
- Scripts are intentionally skipped on sensitive paths via `DashboardController#sensitive_path?`.

### Scope Mode: Single Account or Global

- Global mode:
  - Keep the script active in Super Admin, or use `DASHBOARD_SCRIPTS` global config.
  - The behavior is expected to run for all accounts in dashboard routes.
- Single-account mode:
  - Injection remains global, so enforce account scope inside the script at runtime.
  - Read account id from URL (`/app/accounts/:id/...`) and return early when it does not match target account.
  - For strict per-account integrations, prefer `DashboardApp` records because they are account-scoped.

### Dashboard Script Model Rules

- Model: `app/models/dashboard_script.rb`.
- Required: `name`, `content`.
- `content` has max length enforced by `Limits::DASHBOARD_SCRIPT_CONTENT_MAX_LENGTH`.
- Only `active: true` scripts are loaded into dashboard pages.

### Super Admin Editor/Preview Behavior

- Main editor: `app/views/super_admin/dashboard_scripts/show.html.erb`.
- New form: `app/views/super_admin/dashboard_scripts/new.html.erb`.
- Preview runs against iframe URL `/app/accounts/1/dashboard` and supports desktop/mobile toggles.
- Combined scripts add `data-name` automatically to the first `<script` tag when building payload.

### Alternative Architecture (When Script Is Not Ideal)

- `DashboardApp` (`app/models/dashboard_app.rb`) supports URL-based framed apps.
- `DashboardApp` content schema requires array of `{ type: "frame", url: "https://..." }`.
- Frontend frame bridge (`DashboardApp/Frame.vue`) posts `appContext` with conversation/contact/agent.
- Use Dashboard App when embedding larger third-party modules.

## Decision Matrix: Dashboard Script vs Dashboard App

Use **Dashboard Script** when:

- You need lightweight DOM customization.
- Change scope is small and local (button text, visual markers, hide one control).
- You can implement idempotently with stable selectors and low runtime cost.

Use **Dashboard App** when:

- You need a full external UI/module.
- You need strong isolation from Mega dashboard DOM changes.
- You need structured conversation/contact/agent context in a framed integration.
- You are integrating a third-party product with independent release cycle.

## Pattern Guidance from Our Source Code

Patterns worth reusing:

- `DOMContentLoaded` bootstrap.
- Duplicate guards (`if (element exists) return`, `dataset.customized`, unique keys).
- `data-name` script labeling for traceability.
- Targeted `MutationObserver` for dynamic UI regions.

Patterns to avoid or tame:

- Very deep Tailwind selector chains (extremely brittle).
- Infinite or frequent `setInterval` loops as primary strategy.
- Global mutation of all elements (`querySelectorAll('*')`) unless absolutely required.
- Blind dependence on `window.__vue__` internals without fallback guards.

## Required Workflow

### 1) Clarify the target behavior

Capture:

- Where it should run (which dashboard page/route).
- What user action or UI state should trigger it.
- Whether it is desktop, mobile, or both.
- Scope mode: global or single-account.

### 2) Map stable anchors first

Prefer selectors with this priority:

1. Semantic ids or stable data attributes.
2. Short class selectors tied to component intent.
3. Structural selectors only if no better option.

Never start with long full-DOM chains unless there is no alternative.

### 3) Build idempotent script

- Add a global guard key so script initializes once.
- Wrap in `<script data-name="your-feature-name">...</script>`.
- Mark processed nodes with `dataset` flags.
- Keep side effects local to required nodes.
- If single-account mode is requested, add a URL account guard before any mutation.

### 4) Handle dynamic rendering safely

- Use `MutationObserver` only on needed subtree.
- Disconnect observer when done if possible.
- If you need interval fallback, use low frequency and stop conditions.

### 5) Add safety guards

- Check required elements before mutating.
- Gate mobile-only behavior by viewport.
- Avoid overriding critical actions unless explicitly requested.
- Avoid new remote script injection unless requirement is explicit and trusted.

### 6) Validate with dashboard preview

- Verify desktop preview and mobile preview.
- Validate no duplicate UI insertion on re-render.
- Validate no console errors in injected script path.

### 7) Deliver output in this format

Provide:

- Final script snippet.
- Why selectors were chosen.
- Runtime strategy (observer/guards).
- Known risks and fallback plan.
- Recommendation if Dashboard App would be better.

## Implementation Template (Preferred Baseline)

```html
<script data-name="feature-name">
  (function () {
    const SCRIPT_KEY = 'mega_dashboard_feature_name_v1';
    if (window[SCRIPT_KEY]) return;
    window[SCRIPT_KEY] = true;

    const TARGET_ACCOUNT_ID = null; // Example: 1 for single-account mode, null for global mode

    function getAccountIdFromPath() {
      const match = window.location.pathname.match(/\/app\/accounts\/(\d+)/);
      return match ? Number(match[1]) : null;
    }

    function isScopeAllowed() {
      if (TARGET_ACCOUNT_ID === null) return true;
      return getAccountIdFromPath() === TARGET_ACCOUNT_ID;
    }

    const isMobile = () => window.innerWidth <= 768;

    function applyFeature() {
      if (!isScopeAllowed()) return;

      const target = document.querySelector('[data-your-anchor]');
      if (!target) return;
      if (target.dataset.featureApplied === 'true') return;

      target.dataset.featureApplied = 'true';
      // Apply your scoped DOM change here.
    }

    function bootstrap() {
      applyFeature();

      const observer = new MutationObserver(() => {
        applyFeature();
      });

      observer.observe(document.body, {
        childList: true,
        subtree: true,
      });

      // Optional guard to avoid permanent observers when not needed.
      setTimeout(() => observer.disconnect(), 20000);

      window.addEventListener('resize', () => {
        // Keep lightweight; only run if feature depends on viewport.
        if (isMobile()) applyFeature();
      });
    }

    if (document.readyState === 'loading') {
      document.addEventListener('DOMContentLoaded', bootstrap, { once: true });
    } else {
      bootstrap();
    }
  })();
</script>
```

## Output Quality Checklist

Before finalizing, verify all items:

- Script is wrapped in `<script>` tag and has `data-name`.
- Initialization is idempotent (global key + node-level guard).
- No unbounded hot loop.
- Selector strategy is as stable as possible.
- Mobile-only logic is gated.
- Scope mode is explicit (global or single-account) and implemented correctly.
- Behavior is understandable and minimally invasive.
- If request is complex, include Dashboard App recommendation.
