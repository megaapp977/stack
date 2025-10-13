# 🧭 Mega Dashboard Script — Add Custom Sidebar Item with Embedded App

This guide explains how to add a **custom link in Mega’s sidebar** that opens your own embedded application inside the main dashboard area — without leaving the Mega interface.

---

## 🔐 Accessing Dashboard Scripts

To add the script, you must first log in to your Mega **Super Admin panel**:

1. Visit the following URL (replace `your-domain.com` with your own):
   ```
   https://your-domain.com/super_admin/app_config?config=internal
   ```
2. Scroll down to find **Dashboard Scripts**.
3. Paste the JavaScript code provided in this guide.
4. Click **Save** and reload your dashboard.

---

## ⚙️ Features

- Keeps the **sidebar visible** at all times.  
- Supports both **Dark and Light themes** automatically.  
- Allows full **position control** (before or after any built-in menu item).  
- Embeds your app in an **iframe** inside the Mega dashboard.

---

## 🧩 Configuration (`CFG` block)

Inside the script, edit the `CFG` constant to customize your app:

```js
const CFG = {
  // Sidebar label and icon
  LINK_TEXT: 'My Application',
  LINK_ICON: '🧭',

  // The app or web tool to embed
  IFRAME_URL: 'https://www.google.com',

  // Sidebar item position options
  POSITION: {
    mode: 'afterLabel', // 'start' | 'end' | 'index' | 'afterLabel' | 'beforeLabel'
    label: 'Conversations', // The text of the reference menu item (exactly as shown in your sidebar)
    index: 0 // Used only when mode = 'index'
  },

  // Visual options for the embedded panel
  PADDING: 0,            // Internal padding (px)
  SHOW_BORDER: true,     // Adds subtle border matching current theme
};
```

---

## 🎯 Positioning Modes

| `mode` | Description | Example |
|--------|-------------|----------|
| `start` | Places your item at the **top** of the sidebar. | `{ mode: 'start' }` |
| `end` | Places your item at the **bottom** of the sidebar (default). | `{ mode: 'end' }` |
| `index` | Places your item at an **exact numeric position** (starting from 0). | `{ mode: 'index', index: 3 }` |
| `afterLabel` | Inserts **after** a sidebar item by its visible label text. | `{ mode: 'afterLabel', label: 'Conversations' }` |
| `beforeLabel` | Inserts **before** a sidebar item by label text. | `{ mode: 'beforeLabel', label: 'Campaigns' }` |

### 💡 Examples

#### Place before “Conversations”
```js
POSITION: { mode: 'beforeLabel', label: 'Conversations' }
```

#### Place after “Conversations”
```js
POSITION: { mode: 'afterLabel', label: 'Conversations' }
```

#### Place after “Campaigns”
```js
POSITION: { mode: 'afterLabel', label: 'Campaigns' }
```

#### Place at the top of the sidebar
```js
POSITION: { mode: 'start' }
```

#### Place at position index 4
```js
POSITION: { mode: 'index', index: 4 }
```

---

## 🌓 Theme Support (Dark / Light)

This script automatically adapts to Mega’s **dark/light mode**:

- Background color  
- Text color  
- Border color  

It dynamically updates when the user toggles between themes — no reload required.

---

## 🧱 Full JavaScript Code

Paste this entire script into the **Dashboard Scripts** section:

```html
<script>
(function () {
  /** CONFIGURATION — customize this section **/
  const CFG = {
    LINK_TEXT: 'My Application',
    LINK_ICON: '🧭',
    IFRAME_URL: 'https://www.google.com',
    POSITION: { mode: 'afterLabel', label: 'Conversations', index: 0 },
    PADDING: 0,
    SHOW_BORDER: true,
  };

  const $ = (s, r=document) => { try { return r.querySelector(s); } catch { return null; } };
  const $$ = (s, r=document) => { try { return Array.from(r.querySelectorAll(s)); } catch { return []; } };
  const on = (el, ev, fn, opts) => el && el.addEventListener(ev, fn, opts || { passive: true });
  const normalize = s => (s || '').toLowerCase().replace(/\s+/g, ' ').trim();

  function findSidebar() {
    return $('[data-testid="sidebar-primary"]') || $('aside');
  }
  function findAnyList() {
    const sb = findSidebar(); if (!sb) return null;
    return $('ul', sb);
  }
  function findListAndRefByLabel(labelWanted) {
    const sb = findSidebar(); if (!sb) return { list: null, ref: null };
    const wanted = normalize(labelWanted);
    const uls = $$('ul', sb);
    for (const ul of uls) {
      const lis = $$(':scope > li', ul);
      for (const li of lis) {
        const txt = normalize(li.textContent);
        if (txt === wanted || txt.includes(wanted)) {
          return { list: ul, ref: li };
        }
      }
    }
    return { list: null, ref: null };
  }

  function ensurePanel() {
    if ($('#cw-embed-panel')) return $('#cw-embed-panel');
    const panel = document.createElement('div');
    panel.id = 'cw-embed-panel';
    panel.style.cssText = 'position:fixed;inset:auto 0 0 0;top:0;z-index:9;display:none;';
    panel.innerHTML = `<iframe id="cw-embed-iframe" style="width:100%;height:100%;border:0;"></iframe>`;
    document.body.appendChild(panel);

    function layout() {
      const sb = findSidebar(); if (!sb) return;
      const r = sb.getBoundingClientRect();
      panel.style.left = r.right + 'px';
      panel.style.width = (window.innerWidth - r.right) + 'px';
      panel.style.background = getComputedStyle(document.body).backgroundColor;
    }
    layout();
    on(window, 'resize', layout);

    window.__cwShowEmbedPanel = () => {
      $('#cw-embed-iframe').src = CFG.IFRAME_URL;
      layout();
      panel.style.display = 'block';
    };
    window.__cwHideEmbedPanel = () => {
      panel.style.display = 'none';
      $('#cw-embed-iframe').src = 'about:blank';
    };
    return panel;
  }

  function ensureSidebarLink() {
    if ($('#cw-embed-link')) return;

    const li = document.createElement('li');
    li.id = 'cw-embed-link';
    li.style.listStyle = 'none';
    li.innerHTML = `
      <a href="javascript:void(0)" style="display:flex;align-items:center;gap:10px;
        padding:8px 12px;border-radius:8px;text-decoration:none;color:inherit;">
        <span>${CFG.LINK_ICON}</span><span>${CFG.LINK_TEXT}</span>
      </a>`;
    const link = li.querySelector('a');

    let parentList = null;
    let ref = null;

    if (CFG.POSITION.mode === 'afterLabel' || CFG.POSITION.mode === 'beforeLabel') {
      const found = findListAndRefByLabel(CFG.POSITION.label);
      parentList = found.list;
      ref = found.ref;
    }
    if (!parentList) parentList = findAnyList();
    if (!parentList) return;

    const items = $$(':scope > li', parentList);
    switch (CFG.POSITION.mode) {
      case 'start':
        parentList.insertBefore(li, items[0] || null);
        break;
      case 'index':
        parentList.insertBefore(li, items[Math.max(0, Math.min(CFG.POSITION.index, items.length))] || null);
        break;
      case 'afterLabel':
        if (ref && ref.nextSibling) parentList.insertBefore(li, ref.nextSibling);
        else parentList.appendChild(li);
        break;
      case 'beforeLabel':
        if (ref) parentList.insertBefore(li, ref);
        else parentList.insertBefore(li, items[0] || null);
        break;
      case 'end':
      default:
        parentList.appendChild(li);
    }
    on(link, 'click', () => {
      if (typeof window.__cwShowEmbedPanel === 'function') window.__cwShowEmbedPanel();
    });
  }

  function boot() { ensurePanel(); ensureSidebarLink(); }
  if (document.readyState === 'loading') document.addEventListener('DOMContentLoaded', boot);
  else boot();
  new MutationObserver(() => ensureSidebarLink())
    .observe(document.body, { childList: true, subtree: true });
})();
</script>
```

---

## ✅ Notes

- Your embedded app **must allow iframe embedding**.  
  Ensure your app’s headers **do not include** `X-Frame-Options: DENY` or `SAMEORIGIN`.  
  Add the following CSP header if needed:
  ```http
  Content-Security-Policy: frame-ancestors https://your-Mega-domain.com;
  ```

- To exit the embedded app view, simply click any other sidebar item.

- The embedded iframe automatically adjusts to the sidebar width and respects the active theme.

---

**Author:**  
Mega Dashboard Script Guide (v1.1)  
Maintained by **@nestordavalos**
