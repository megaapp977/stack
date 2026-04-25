# 🧭 Mega Dashboard Scripts — Guía del Creador y Patrones Seguros

Esta guía es la referencia oficial para crear Dashboard Scripts en Mega con:

- Anchors de DOM seguros.
- Comportamiento idempotente.
- Estrategias de ejecución de baja fragilidad.
- Criterios claros para decidir entre Dashboard Script y Dashboard App.

También complementa la skill reutilizable de IA disponible en `skills/skills.md`.

---

## 🌐 Idiomas

- English: `README.md`
- Português (Brasil): `README-PT-BR.md`
- Español: `README-ES.md`

---

## 🔐 Acceso a Dashboard Scripts

Para agregar un script, entra al panel Super Admin de Mega:

- Visita (reemplaza `tu-dominio.com`):

  ```text
  https://tu-dominio.com/super_admin/app_config?config=internal
  ```

- Busca **Dashboard Scripts**.
- Pega tu script.
- Haz clic en **Guardar** y recarga el dashboard.

---

## 🧠 Ubicación de la Skill de IA

La especificación de la skill para agentes de IA está en:

- `skills/skills.md`

Usa esta skill cuando la solicitud incluya:

- `crear dashboard script`
- `script para dashboard`
- `customizar dashboard`
- `super_admin/dashboard_scripts`
- `dashboard scripts`

---

## 🏗️ Hechos del Codebase que Debes Respetar

### Pipeline de inyección

- Los scripts de dashboard se ensamblan en `DashboardController#set_dashboard_scripts` desde:
  - Registros activos en BD (`DashboardScript.active.ordered.pluck(:content)`).
  - Configuración global (`DASHBOARD_SCRIPTS`).
- El contenido final se inyecta en `app/views/layouts/vueapp.html.erb` mediante `@dashboard_scripts.html_safe`.
- Los scripts se omiten en rutas sensibles mediante `DashboardController#sensitive_path?`.

### Modo de alcance: global o cuenta única

- Modo global:
  - Mantén el script activo en Super Admin o usa `DASHBOARD_SCRIPTS`.
  - El comportamiento corre para todas las cuentas en rutas de dashboard.
- Modo cuenta única:
  - La inyección sigue siendo global, así que debes aplicar guard de cuenta en runtime dentro del script.
  - Lee la cuenta desde la URL (`/app/accounts/:id/...`) y corta la ejecución si no coincide.
  - Para integraciones estrictas por cuenta, prefiere `DashboardApp`.

### Reglas del modelo Dashboard Script

- Modelo: `app/models/dashboard_script.rb`.
- Campos requeridos: `name`, `content`.
- Largo máximo de `content`: `Limits::DASHBOARD_SCRIPT_CONTENT_MAX_LENGTH`.
- Solo se cargan scripts con `active: true`.

### Comportamiento del editor y preview en Super Admin

- Editor principal: `app/views/super_admin/dashboard_scripts/show.html.erb`.
- Formulario nuevo: `app/views/super_admin/dashboard_scripts/new.html.erb`.
- El preview usa iframe con URL `/app/accounts/1/dashboard` y soporta desktop/mobile.
- Los scripts combinados agregan `data-name` automáticamente en la primera etiqueta `<script` del payload.

### Arquitectura alternativa cuando script no es ideal

- Modelo `DashboardApp`: `app/models/dashboard_app.rb`.
- El schema de contenido requiere items como `{ type: "frame", url: "https://..." }`.
- El puente frontend en `DashboardApp/Frame.vue` publica `appContext` (conversation/contact/agent).
- Usa Dashboard App para módulos externos grandes embebidos.

---

## 🧭 Matriz de Decisión: Script vs App

Usa **Dashboard Script** cuando:

- Necesitas personalización ligera de DOM.
- El alcance es pequeño/local (texto de botón, marcadores visuales, ocultar un control).
- Puedes implementar con idempotencia y selectores estables.

Usa **Dashboard App** cuando:

- Necesitas un módulo/UI externo completo.
- Necesitas mayor aislamiento frente a cambios del DOM del dashboard.
- Necesitas contexto estructurado (conversation/contact/agent) en integración embebida.
- Integras un tercero con ciclo de releases independiente.

---

## ✅ Flujo Obligatorio

### 1) Aclarar el comportamiento objetivo

Captura:

- En qué ruta/página debe correr.
- Qué acción o estado de UI lo dispara.
- Si aplica para desktop, mobile o ambos.
- Modo de alcance (global o cuenta única).

### 2) Mapear anchors estables primero

Prioridad de selectores:

1. IDs semánticos o atributos de datos estables.
2. Clases cortas con intención clara.
3. Selectores estructurales solo como último recurso.

Evita cadenas largas y frágiles de DOM.

### 3) Construir script idempotente

- Agrega una llave global para inicializar una sola vez.
- Usa `<script data-name="feature-name">`.
- Marca nodos procesados con flags en `dataset`.
- Mantén efectos colaterales locales.
- Si es cuenta única, agrega guard por URL antes de mutar.

### 4) Manejar render dinámico de forma segura

- Usa `MutationObserver` solo en el subtree necesario.
- Desconecta el observer cuando sea posible.
- Si necesitas fallback por intervalo, usa baja frecuencia y condiciones de corte.

### 5) Agregar guardas de seguridad

- Verifica elementos requeridos antes de mutar.
- Limita comportamiento mobile-only por viewport.
- Evita sobrescribir acciones críticas si no fue solicitado explícitamente.
- Evita inyectar scripts remotos salvo requisito explícito y de confianza.

### 6) Validar con preview del dashboard

- Verifica en preview desktop y mobile.
- Valida que no exista inserción duplicada en re-render.
- Valida que no existan errores en consola.

### 7) Entregar salida completa

Incluye:

- Snippet final del script.
- Razón de selección de selectores.
- Estrategia de runtime (observer/guards).
- Riesgos conocidos y plan de fallback.
- Recomendación de Dashboard App si conviene más.

---

## 🧱 Plantilla de Implementación (Baseline Preferido)

```html
<script data-name="feature-name">
  (function () {
    const SCRIPT_KEY = 'mega_dashboard_feature_name_v1';
    if (window[SCRIPT_KEY]) return;
    window[SCRIPT_KEY] = true;

    const TARGET_ACCOUNT_ID = null; // Ejemplo: 1 para cuenta única, null para global

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
      // Aplica aquí el cambio de DOM de forma local.
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

      // Guarda opcional para evitar observers permanentes cuando no hagan falta.
      setTimeout(() => observer.disconnect(), 20000);

      window.addEventListener('resize', () => {
        // Mantener liviano; ejecutar solo si la feature depende del viewport.
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

---

## 🎯 Ejemplo de Referencia: Item en Sidebar con App Embebida

Usa este ejemplo listo para producción para agregar un item en la sidebar que abre un iframe embebido dentro de Mega.

### Configuración (bloque `CFG`)

```js
const CFG = {
  LINK_TEXT: 'Mi Aplicación',
  LINK_ICON: '🧭',
  IFRAME_URL: 'https://www.google.com',
  TARGET_ACCOUNT_ID: null, // Define un número para modo cuenta única
  POSITION: {
    mode: 'afterLabel', // 'start' | 'end' | 'index' | 'afterLabel' | 'beforeLabel'
    label: 'Conversaciones',
    index: 0,
  },
  PADDING: 0,
  SHOW_BORDER: true,
  MOBILE_MAX_WIDTH: 768,
};
```

### Modos de posición

| `mode` | Descripción | Ejemplo |
| --- | --- | --- |
| `start` | Coloca el item al inicio de la sidebar. | `{ mode: 'start' }` |
| `end` | Coloca el item al final (por defecto). | `{ mode: 'end' }` |
| `index` | Coloca en un índice exacto (base 0). | `{ mode: 'index', index: 3 }` |
| `afterLabel` | Inserta después de un item por texto visible. | `{ mode: 'afterLabel', label: 'Conversaciones' }` |
| `beforeLabel` | Inserta antes de un item por texto visible. | `{ mode: 'beforeLabel', label: 'Campañas' }` |

### Código JavaScript completo

```html
<script data-name="sidebar-embed-app">
  (function () {
    const SCRIPT_KEY = 'mega_sidebar_embed_app_v2';
    if (window[SCRIPT_KEY]) return;
    window[SCRIPT_KEY] = true;

    const CFG = {
      LINK_TEXT: 'My Application',
      LINK_ICON: '🧭',
      IFRAME_URL: 'https://www.google.com',
      TARGET_ACCOUNT_ID: null,
      POSITION: { mode: 'afterLabel', label: 'Conversations', index: 0 },
      PADDING: 0,
      SHOW_BORDER: true,
      MOBILE_MAX_WIDTH: 768,
    };

    const $ = (s, r = document) => {
      try {
        return r.querySelector(s);
      } catch {
        return null;
      }
    };
    const $$ = (s, r = document) => {
      try {
        return Array.from(r.querySelectorAll(s));
      } catch {
        return [];
      }
    };
    const on = (el, ev, fn, opts) => {
      if (el) el.addEventListener(ev, fn, opts);
    };
    const normalize = value => (value || '').toLowerCase().replace(/\s+/g, ' ').trim();

    let panel = null;

    function getAccountIdFromPath() {
      const match = window.location.pathname.match(/\/app\/accounts\/(\d+)/);
      return match ? Number(match[1]) : null;
    }

    function isScopeAllowed() {
      if (CFG.TARGET_ACCOUNT_ID === null) return true;
      return getAccountIdFromPath() === CFG.TARGET_ACCOUNT_ID;
    }

    function findSidebar() {
      return $('[data-testid="sidebar-primary"]') || $('aside');
    }

    function findAnyList() {
      const sb = findSidebar();
      if (!sb) return null;
      return $('ul', sb);
    }

    function findListAndRefByLabel(labelWanted) {
      const sb = findSidebar();
      if (!sb) return { list: null, ref: null };

      const wanted = normalize(labelWanted);
      const uls = $$('ul', sb);
      for (const ul of uls) {
        const lis = $$(':scope > li', ul);
        for (const li of lis) {
          const text = normalize(li.textContent);
          if (text === wanted || text.includes(wanted)) {
            return { list: ul, ref: li };
          }
        }
      }
      return { list: null, ref: null };
    }

    function getThemeTokens() {
      const rootStyle = getComputedStyle(document.documentElement);
      const bodyStyle = getComputedStyle(document.body);

      return {
        background: rootStyle.getPropertyValue('--w-bg-color').trim() || bodyStyle.backgroundColor,
        text: rootStyle.getPropertyValue('--w-text-color').trim() || bodyStyle.color,
        border: rootStyle.getPropertyValue('--w-border-color').trim() || 'rgba(148, 163, 184, 0.35)',
      };
    }

    function applyPanelTheme() {
      if (!panel) return;
      const tokens = getThemeTokens();
      panel.style.background = tokens.background;
      panel.style.color = tokens.text;
      panel.style.padding = `${CFG.PADDING}px`;
      panel.style.borderLeft = CFG.SHOW_BORDER ? `1px solid ${tokens.border}` : '0';
    }

    function layoutPanel() {
      if (!panel || panel.dataset.visible !== 'true') return;
      const sb = findSidebar();
      if (!sb) return;

      const rect = sb.getBoundingClientRect();
      panel.style.left = `${Math.max(0, rect.right)}px`;
      panel.style.width = `${Math.max(320, window.innerWidth - rect.right)}px`;
    }

    function ensurePanel() {
      if (panel && document.body.contains(panel)) return panel;

      panel = document.createElement('section');
      panel.id = 'mega-embed-panel';
      panel.dataset.visible = 'false';
      panel.style.cssText = [
        'position:fixed',
        'top:0',
        'right:0',
        'bottom:0',
        'z-index:9',
        'display:none',
        'overflow:hidden',
      ].join(';');

      panel.innerHTML = '<iframe id="mega-embed-iframe" title="Embedded dashboard app" style="width:100%;height:100%;border:0;"></iframe>';
      document.body.appendChild(panel);

      applyPanelTheme();
      layoutPanel();
      return panel;
    }

    function hidePanel() {
      if (!panel) return;
      panel.dataset.visible = 'false';
      panel.style.display = 'none';

      const iframe = $('#mega-embed-iframe');
      if (iframe) iframe.src = 'about:blank';
    }

    function showPanel() {
      ensurePanel();
      const iframe = $('#mega-embed-iframe');
      if (iframe && iframe.src !== CFG.IFRAME_URL) iframe.src = CFG.IFRAME_URL;

      panel.dataset.visible = 'true';
      panel.style.display = 'block';
      applyPanelTheme();
      layoutPanel();
    }

    function ensureSidebarLink() {
      if ($('#mega-embed-link')) return;

      const li = document.createElement('li');
      li.id = 'mega-embed-link';
      li.style.listStyle = 'none';
      li.innerHTML = `
        <a href="#" data-mega-embed-link="true" style="display:flex;align-items:center;gap:10px;padding:8px 12px;border-radius:8px;text-decoration:none;color:inherit;">
          <span aria-hidden="true">${CFG.LINK_ICON}</span><span>${CFG.LINK_TEXT}</span>
        </a>
      `;

      const link = $('a', li);
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

      on(link, 'click', event => {
        event.preventDefault();
        showPanel();
      });
    }

    function bindSidebarCloseHandler() {
      const sb = findSidebar();
      if (!sb || sb.dataset.embedCloseBound === 'true') return;
      sb.dataset.embedCloseBound = 'true';

      on(
        sb,
        'click',
        event => {
          const customLink = event.target && event.target.closest('[data-mega-embed-link="true"]');
          if (!customLink) hidePanel();
        },
        { capture: true, passive: true }
      );
    }

    function applyFeature() {
      if (!isScopeAllowed()) return;
      ensurePanel();
      ensureSidebarLink();
      bindSidebarCloseHandler();
      applyPanelTheme();
    }

    function bootstrap() {
      applyFeature();

      const observer = new MutationObserver(() => applyFeature());
      observer.observe(document.body, { childList: true, subtree: true });

      const themeObserver = new MutationObserver(() => applyPanelTheme());
      themeObserver.observe(document.documentElement, { attributes: true, attributeFilter: ['class', 'data-theme'] });
      themeObserver.observe(document.body, { attributes: true, attributeFilter: ['class', 'data-theme'] });

      on(window, 'resize', () => {
        if (window.innerWidth <= CFG.MOBILE_MAX_WIDTH) {
          hidePanel();
        } else {
          applyPanelTheme();
          layoutPanel();
        }
      });

      setTimeout(() => observer.disconnect(), 20000);
    }

    if (document.readyState === 'loading') {
      document.addEventListener('DOMContentLoaded', bootstrap, { once: true });
    } else {
      bootstrap();
    }
  })();
</script>
```

---

## ✅ Checklist de Calidad de Salida

Antes de finalizar cualquier script:

- El script está envuelto en `<script>` y tiene `data-name`.
- La inicialización es idempotente (llave global + guardas por nodo).
- No hay hot loops sin límite.
- La estrategia de selectores es lo más estable posible.
- La lógica mobile-only está correctamente condicionada.
- El modo de alcance es explícito (global o cuenta única).
- El comportamiento es mínimamente invasivo y entendible.
- Si el caso es complejo, incluye recomendación de Dashboard App.

---

## 📌 Notas

- Las apps embebidas deben permitir uso en iframe.
- Evita `X-Frame-Options: DENY` y `X-Frame-Options: SAMEORIGIN` en la app objetivo.
- Agrega CSP si es necesario:

  ```http
  Content-Security-Policy: frame-ancestors https://tu-dominio-mega.com;
  ```

---

**Autor:**
Guía de Dashboard Scripts de Mega (v2.0)
Mantenido por **@nestordavalos**
