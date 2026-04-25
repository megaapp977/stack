# 🧭 Mega Dashboard Scripts — Guia do Criador e Padrões Seguros

Este guia é a referência oficial para criar Dashboard Scripts no Mega com:

- Anchors de DOM seguros.
- Comportamento idempotente.
- Estratégias de execução com baixa fragilidade.
- Critérios claros para decidir entre Dashboard Script e Dashboard App.

Também complementa a skill reutilizável de IA disponível em `skills/skills.md`.

---

## 🌐 Idiomas

- English: `README.md`
- Português (Brasil): `README-PT-BR.md`
- Español: `README-ES.md`

---

## 🔐 Acesso aos Dashboard Scripts

Para adicionar um script, acesse o painel Super Admin do Mega:

- Acesse (substitua `seu-dominio.com`):

  ```text
  https://seu-dominio.com/super_admin/app_config?config=internal
  ```

- Localize **Dashboard Scripts**.
- Cole seu script.
- Clique em **Salvar** e recarregue o dashboard.

---

## 🧠 Local da Skill de IA

A especificação da skill para agentes de IA está em:

- `skills/skills.md`

Use essa skill quando o pedido envolver:

- `crear dashboard script`
- `script para dashboard`
- `customizar dashboard`
- `super_admin/dashboard_scripts`
- `dashboard scripts`

---

## 🏗️ Fatos do Codebase que Você Deve Respeitar

### Pipeline de injeção

- Os scripts de dashboard são montados em `DashboardController#set_dashboard_scripts` a partir de:
  - Registros ativos no banco (`DashboardScript.active.ordered.pluck(:content)`).
  - Configuração global (`DASHBOARD_SCRIPTS`).
- O conteúdo final é injetado em `app/views/layouts/vueapp.html.erb` por `@dashboard_scripts.html_safe`.
- Scripts são ignorados em rotas sensíveis por `DashboardController#sensitive_path?`.

### Modo de escopo: global ou conta única

- Modo global:
  - Mantenha o script ativo no Super Admin ou use `DASHBOARD_SCRIPTS`.
  - O comportamento roda para todas as contas nas rotas de dashboard.
- Modo conta única:
  - A injeção continua global, então aplique guarda de conta no runtime do script.
  - Leia a conta na URL (`/app/accounts/:id/...`) e retorne cedo quando não corresponder.
  - Para integrações estritas por conta, prefira `DashboardApp`.

### Regras do modelo Dashboard Script

- Modelo: `app/models/dashboard_script.rb`.
- Campos obrigatórios: `name`, `content`.
- Tamanho máximo de `content`: `Limits::DASHBOARD_SCRIPT_CONTENT_MAX_LENGTH`.
- Apenas scripts com `active: true` são carregados.

### Comportamento do editor e preview no Super Admin

- Editor principal: `app/views/super_admin/dashboard_scripts/show.html.erb`.
- Formulário novo: `app/views/super_admin/dashboard_scripts/new.html.erb`.
- Preview usa iframe com URL `/app/accounts/1/dashboard` e alternância desktop/mobile.
- Scripts combinados adicionam `data-name` automaticamente à primeira tag `<script` no payload.

### Arquitetura alternativa quando script não é ideal

- Modelo `DashboardApp`: `app/models/dashboard_app.rb`.
- O schema de conteúdo usa itens como `{ type: "frame", url: "https://..." }`.
- A ponte frontend em `DashboardApp/Frame.vue` envia `appContext` (conversation/contact/agent).
- Use Dashboard App para módulos terceiros maiores embutidos.

---

## 🧭 Matriz de Decisão: Script vs App

Use **Dashboard Script** quando:

- Você precisa de customização leve de DOM.
- O escopo é pequeno/local (texto de botão, marcadores visuais, ocultar um controle).
- É possível implementar com idempotência e seletores estáveis.

Use **Dashboard App** quando:

- Você precisa de um módulo/UI externo completo.
- Você quer isolamento mais forte contra mudanças de DOM do dashboard.
- Você precisa de contexto estruturado (conversation/contact/agent) na integração via frame.
- Você integra produto terceiro com ciclo de release próprio.

---

## ✅ Fluxo Obrigatório

### 1) Clarificar comportamento alvo

Capturar:

- Em qual rota/página deve rodar.
- Qual ação ou estado de UI dispara o comportamento.
- Se aplica a desktop, mobile ou ambos.
- Modo de escopo (global ou conta única).

### 2) Mapear anchors estáveis primeiro

Prioridade de seletores:

1. IDs semânticos ou atributos de dados estáveis.
2. Classes curtas com intenção clara.
3. Seletores estruturais apenas como último recurso.

Evite cadeias longas e frágeis no DOM.

### 3) Construir script idempotente

- Adicione chave global de inicialização única.
- Use `<script data-name="feature-name">`.
- Marque nós processados com flags em `dataset`.
- Mantenha efeitos colaterais locais.
- Para conta única, aplique guarda por URL antes de mutações.

### 4) Lidar com renderização dinâmica com segurança

- Use `MutationObserver` apenas no subtree necessário.
- Desconecte observer quando possível.
- Se precisar de fallback com intervalo, use baixa frequência e condição de parada.

### 5) Adicionar guardas de segurança

- Verifique elementos necessários antes de mutar.
- Gate de comportamento mobile-only por viewport.
- Evite sobrescrever ações críticas sem pedido explícito.
- Evite injetar scripts remotos sem requisito explícito e confiável.

### 6) Validar no preview do dashboard

- Validar em preview desktop e mobile.
- Confirmar que não há UI duplicada em re-render.
- Confirmar ausência de erros no console.

### 7) Entregar saída completa

Fornecer:

- Snippet final do script.
- Justificativa dos seletores escolhidos.
- Estratégia de runtime (observer/guards).
- Riscos conhecidos e plano de fallback.
- Recomendação de Dashboard App quando for mais adequado.

---

## 🧱 Template de Implementação (Baseline Preferida)

```html
<script data-name="feature-name">
  (function () {
    const SCRIPT_KEY = 'mega_dashboard_feature_name_v1';
    if (window[SCRIPT_KEY]) return;
    window[SCRIPT_KEY] = true;

    const TARGET_ACCOUNT_ID = null; // Exemplo: 1 para conta única, null para global

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
      // Aplique aqui a mudança de DOM de forma local.
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

      // Guarda opcional para evitar observer permanente quando não necessário.
      setTimeout(() => observer.disconnect(), 20000);

      window.addEventListener('resize', () => {
        // Mantenha leve; só rode se a feature depender de viewport.
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

## 🎯 Exemplo de Referência: Item na Sidebar com App Embutido

Use este exemplo pronto para produção para adicionar um item na sidebar que abre um iframe embutido dentro do Mega.

### Configuração (bloco `CFG`)

```js
const CFG = {
  LINK_TEXT: 'Meu Aplicativo',
  LINK_ICON: '🧭',
  IFRAME_URL: 'https://www.google.com',
  TARGET_ACCOUNT_ID: null, // Defina um número para modo conta única
  POSITION: {
    mode: 'afterLabel', // 'start' | 'end' | 'index' | 'afterLabel' | 'beforeLabel'
    label: 'Conversas',
    index: 0,
  },
  PADDING: 0,
  SHOW_BORDER: true,
  MOBILE_MAX_WIDTH: 768,
};
```

### Modos de posição

| `mode` | Descrição | Exemplo |
| --- | --- | --- |
| `start` | Coloca no topo da sidebar. | `{ mode: 'start' }` |
| `end` | Coloca no final (padrão). | `{ mode: 'end' }` |
| `index` | Coloca em um índice exato (base 0). | `{ mode: 'index', index: 3 }` |
| `afterLabel` | Insere depois de um item pelo texto visível. | `{ mode: 'afterLabel', label: 'Conversas' }` |
| `beforeLabel` | Insere antes de um item pelo texto visível. | `{ mode: 'beforeLabel', label: 'Campanhas' }` |

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

## ✅ Checklist de Qualidade de Saída

Antes de finalizar qualquer script:

- O script está encapsulado em `<script>` e possui `data-name`.
- A inicialização é idempotente (chave global + guardas por nó).
- Não há loops quentes sem limite.
- A estratégia de seletores é a mais estável possível.
- A lógica mobile-only está corretamente condicionada.
- O modo de escopo está explícito (global ou conta única).
- O comportamento é minimamente invasivo e compreensível.
- Para cenários complexos, há recomendação de Dashboard App.

---

## 📌 Observações

- Apps embutidos devem permitir uso em iframe.
- Evite `X-Frame-Options: DENY` e `X-Frame-Options: SAMEORIGIN` no app alvo.
- Adicione CSP se necessário:

  ```http
  Content-Security-Policy: frame-ancestors https://seu-dominio-mega.com;
  ```

---

**Autor:**
Guia de Dashboard Scripts do Mega (v2.0)
Mantido por **@nestordavalos**
