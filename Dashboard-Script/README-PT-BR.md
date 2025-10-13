# 🧭 Script de Dashboard do Mega — Adicione um Item Personalizado na Barra Lateral com um Aplicativo Embutido

Este guia explica como adicionar um **link personalizado na barra lateral do Mega** que abre seu próprio aplicativo embutido dentro da área principal do painel — sem sair da interface do Mega.

---

## 🔐 Acessando os Scripts do Dashboard

Para adicionar o script, primeiro acesse o painel **Super Admin** do seu Mega:

1. Acesse a seguinte URL (substitua `seu-dominio.com` pelo seu domínio real):
   ```
   https://seu-dominio.com/super_admin/app_config?config=internal
   ```
2. Role a página até encontrar **Dashboard Scripts**.
3. Cole o código JavaScript fornecido neste guia.
4. Clique em **Salvar** e recarregue o painel.

---

## ⚙️ Funcionalidades

- Mantém a **barra lateral visível** o tempo todo.  
- Suporta automaticamente os modos **Claro e Escuro**.  
- Permite **controle total de posição** (antes ou depois de qualquer item do menu).  
- Embute seu aplicativo em um **iframe** dentro do painel do Mega.

---

## 🧩 Configuração (bloco `CFG`)

Dentro do script, edite a constante `CFG` para personalizar seu aplicativo:

```js
const CFG = {
  // Rótulo e ícone do link na barra lateral
  LINK_TEXT: 'Meu Aplicativo',
  LINK_ICON: '🧭',

  // O aplicativo ou site a ser embutido
  IFRAME_URL: 'https://www.google.com',

  // Opções de posicionamento na barra lateral
  POSITION: {
    mode: 'afterLabel', // 'start' | 'end' | 'index' | 'afterLabel' | 'beforeLabel'
    label: 'Conversas', // Texto do item de referência (exatamente como aparece na sua barra lateral)
    index: 0 // Usado apenas quando mode = 'index'
  },

  // Opções visuais do painel embutido
  PADDING: 0,            // Espaçamento interno (px)
  SHOW_BORDER: true,     // Adiciona uma borda sutil de acordo com o tema
};
```

---

## 🎯 Modos de Posição

| `mode` | Descrição | Exemplo |
|--------|------------|----------|
| `start` | Coloca seu item **no topo** da barra lateral. | `{ mode: 'start' }` |
| `end` | Coloca seu item **no final** da barra lateral (padrão). | `{ mode: 'end' }` |
| `index` | Coloca seu item em uma **posição numérica específica** (começando em 0). | `{ mode: 'index', index: 3 }` |
| `afterLabel` | Insere **após** um item existente da barra lateral, identificado pelo texto visível. | `{ mode: 'afterLabel', label: 'Conversas' }` |
| `beforeLabel` | Insere **antes** de um item existente da barra lateral. | `{ mode: 'beforeLabel', label: 'Campanhas' }` |

### 💡 Exemplos

#### Colocar antes de “Conversas”
```js
POSITION: { mode: 'beforeLabel', label: 'Conversas' }
```

#### Colocar depois de “Conversas”
```js
POSITION: { mode: 'afterLabel', label: 'Conversas' }
```

#### Colocar depois de “Campanhas”
```js
POSITION: { mode: 'afterLabel', label: 'Campanhas' }
```

#### Colocar no topo da barra lateral
```js
POSITION: { mode: 'start' }
```

#### Colocar na posição de índice 4
```js
POSITION: { mode: 'index', index: 4 }
```

---

## 🌓 Suporte a Tema (Claro / Escuro)

Este script se adapta automaticamente ao modo **claro/escuro** do Mega:

- Cor de fundo  
- Cor do texto  
- Cor da borda  

A atualização é automática quando o usuário alterna entre os modos — sem recarregar a página.

---

## 🧱 Código JavaScript Completo

Cole este script inteiro na seção **Dashboard Scripts**:

```html
<script>
(function () {
  /** CONFIGURAÇÃO — personalize esta seção **/
  const CFG = {
    LINK_TEXT: 'Meu Aplicativo',
    LINK_ICON: '🧭',
    IFRAME_URL: 'https://www.google.com',
    POSITION: { mode: 'afterLabel', label: 'Conversas', index: 0 },
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

## ✅ Observações

- Seu aplicativo embutido **deve permitir o uso dentro de iframe**.  
  Certifique-se de que os cabeçalhos da sua aplicação **não incluam** `X-Frame-Options: DENY` ou `SAMEORIGIN`.  
  Adicione o seguinte cabeçalho CSP se necessário:
  ```http
  Content-Security-Policy: frame-ancestors https://seu-dominio-Mega.com;
  ```

- Para sair da visualização do aplicativo embutido, basta clicar em outro item da barra lateral.

- O iframe embutido ajusta-se automaticamente à largura da barra lateral e respeita o tema ativo.

---

**Autor:**  
Guia do Script de Dashboard do Mega (v1.1)  
Mantido por **@nestordavalos**
