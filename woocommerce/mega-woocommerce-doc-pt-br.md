# Configuração da Integração WooCommerce no MEGA

Conecte sua loja WooCommerce ao MEGA para ver os pedidos de cada cliente direto na conversa.

Com a integração ativa, os agentes veem na barra lateral da conversa os pedidos recentes do contato: número do pedido, status, data e total. Cada número de pedido abre o pedido no painel de administração do WordPress. Opcionalmente, o MEGA também pode avisar na conversa sempre que o status de um pedido mudar.

A configuração tem **3 passos** (o terceiro é opcional).

## Pré-requisitos

Antes de começar, verifique se você tem:

1. **Loja WooCommerce publicada com HTTPS** e acessível pela internet (o MEGA consulta a loja a partir dos servidores dele, não do seu navegador)
2. **Links permanentes ativados** no WordPress: em **Configurações → Links permanentes**, qualquer opção diferente de **Simples** deve estar selecionada. Sem isso, a API do WooCommerce (`/wp-json/...`) não responde
3. **Acesso de administrador** no WordPress / WooCommerce
4. **Acesso de administrador** na sua conta do MEGA
5. **A integração WooCommerce habilitada no seu plano**

> **📌 Nota:** WooCommerce é um recurso premium. Se você não vê o cartão **WooCommerce** em **Configurações → Integrações**, seu plano ainda não o inclui. Peça ao seu provedor do MEGA para habilitá-lo na sua conta.

## Passo 1 — Criar as chaves da API no WooCommerce

1. No WordPress, vá em **WooCommerce → Configurações → Avançado → API REST**
2. Clique em **Adicionar chave**
3. Preencha os campos:
   - **Descrição**: ex. "MEGA"
   - **Usuário**: um usuário administrador ou gerente da loja
   - **Permissões**: **Ler**
4. Clique em **Gerar chave de API**
5. Copie e guarde em um lugar seguro:
   - **Chave do consumidor** (Consumer key), começa com `ck_`
   - **Segredo do consumidor** (Consumer secret), começa com `cs_`

> **⚠️ Importante**
> O WooCommerce mostra o segredo do consumidor **uma única vez**. Se você perdê-lo, revogue a chave e gere uma nova.

> **🔒 Segurança:** O MEGA apenas lê pedidos, nunca os altera. A permissão **Ler** é suficiente; não conceda **Ler/Escrever**.

## Passo 2 — Conectar a loja no MEGA

1. No MEGA, vá em **Configurações → Integrações**
2. Encontre **WooCommerce** e clique em **Conectar**
3. Preencha o formulário:
   - **Store URL**: o endereço da sua loja, ex. `https://www.minhaloja.com.br`
   - **Consumer Key**: a chave `ck_...` do Passo 1
   - **Consumer Secret**: a chave `cs_...` do Passo 1
4. Salve

### Como preencher a Store URL

- Use **exatamente** o **Endereço do site (URL)** que aparece no WordPress em **Configurações → Geral**
- Mantenha o `https://` e o `www` como aparecem lá: `https://minhaloja.com.br` e `https://www.minhaloja.com.br` contam como lojas diferentes
- Não adicione `/wp-admin`, `/loja` nem outros caminhos. A barra final não faz diferença
- Se o WordPress estiver instalado em uma subpasta (ex. `https://minhaloja.com.br/loja`), inclua a subpasta

> **📌 Nota:** O MEGA não testa as chaves ao salvar. A forma de confirmar que tudo funciona é abrir uma conversa (veja abaixo).

### Verificar a conexão

1. Abra a conversa de um cliente que já comprou na loja
2. Na barra lateral direita, expanda a seção **Pedidos do WooCommerce**
3. Você deve ver os pedidos recentes, cada um com:
   - **Pedido nº** (clique para abri-lo no WordPress)
   - **Status**: Pendente, Processando, Em espera, Concluído, Cancelado, Reembolsado ou Falhou
   - **Data** e **total** com a moeda

### Como o MEGA encontra os pedidos de um contato

- O MEGA busca os pedidos pelo **e-mail** e pelo **telefone** do contato, e mostra os resultados juntos, sem repetir pedidos
- **Por e-mail**: o e-mail do contato precisa ser igual ao e-mail de cobrança do pedido
- **Por telefone**: o MEGA reconhece o telefone de cobrança mesmo quando o cliente digitou com espaços, traços ou sem código do país (ex. `(11) 91234-5678`), usando o país de cobrança do pedido. Assim ele bate com o formato internacional do contato (ex. `+5511912345678`)
- São exibidos os **10 pedidos mais recentes**
- Se o contato não tiver e-mail nem telefone, a seção mostra **Nenhum pedido encontrado**

> **💡 Dica:** Você pode reordenar ou recolher a seção **Pedidos do WooCommerce** na barra lateral, como as demais seções.

## Passo 3 — Avisos de mudança de status (opcional)

Com este passo, sempre que o status de um pedido mudar, o MEGA adiciona uma nota na conversa do cliente, por exemplo:

> Status do pedido 1234 atualizado para completed

O status aparece exatamente como o WooCommerce envia (`pending`, `processing`, `on-hold`, `completed`, `cancelled`, `refunded`, `failed`).

### Criar o webhook no WooCommerce

1. No WordPress, vá em **WooCommerce → Configurações → Avançado → Webhooks**
2. Clique em **Adicionar webhook**
3. Preencha os campos:
   - **Nome**: ex. "MEGA - pedidos"
   - **Status**: **Ativo**
   - **Tópico**: **Pedido atualizado**
   - **URL de entrega**: `https://SEU-DOMINIO-MEGA/woocommerce/callback` (substitua `SEU-DOMINIO-MEGA` pelo endereço que você usa para acessar o MEGA, ex. `https://app.minhaempresa.com.br/woocommerce/callback`)
   - **Segredo**: pode manter o valor sugerido pelo WooCommerce
   - **Versão da API**: **WP REST API Integration v3**
4. Clique em **Salvar webhook**

> **💡 Dica:** Se também quiser um aviso quando um pedido for criado, repita os passos com o tópico **Pedido criado**.

### Como os avisos funcionam

- O MEGA identifica a loja pelo endereço, por isso a **Store URL** do Passo 2 precisa ser igual ao endereço do site no WordPress
- O cliente é encontrado pelo **e-mail de cobrança** do pedido e, se não houver correspondência, pelo **telefone de cobrança**, em qualquer formato (lido com o país de cobrança)
- A nota é adicionada na **conversa mais recente** do cliente. Se o cliente não tiver nenhuma conversa no MEGA, nada é adicionado
- A seção **Pedidos do WooCommerce** carrega ao abrir a conversa. Se ela já estiver aberta quando o aviso chegar, abra a conversa de novo para ver o novo status

## Solução de problemas

| Problema | Causa provável | Solução |
|---|---|---|
| **WooCommerce** não aparece em **Configurações → Integrações** | Seu plano não inclui a integração | Peça ao seu provedor do MEGA para habilitá-la |
| A seção **Pedidos do WooCommerce** não aparece na conversa | A integração não está conectada, ou a seção está oculta | Revise o Passo 2 e as seções da barra lateral |
| A seção mostra um erro ao carregar os pedidos | Chaves erradas ou revogadas, Store URL digitada errado, links permanentes em **Simples**, ou um firewall / plugin de segurança bloqueando `/wp-json/` | Revise as chaves e a Store URL; ative os links permanentes; libere o acesso a `/wp-json/wc/v3/` no firewall, Cloudflare ou plugin de segurança |
| **Nenhum pedido encontrado** para um cliente que comprou | Nem o e-mail nem o telefone do contato batem com os dados de cobrança do pedido | Corrija ou adicione o e-mail ou o telefone no contato |
| Os avisos de mudança de status não chegam | Webhook inativo, URL de entrega errada, Store URL diferente do endereço do site, ou o cliente não tem conversa no MEGA | Revise o Passo 3. Em **WooCommerce → Status → Logs**, procure os logs `webhooks-delivery` para ver as respostas |
| O webhook aparece como **Desativado** | O WooCommerce o desativa sozinho após várias entregas com falha | Corrija a URL de entrega e volte o status para **Ativo** |

## Desconectar a integração

1. No MEGA, vá em **Configurações → Integrações → WooCommerce** e exclua a integração
2. No WordPress, vá em **WooCommerce → Configurações → Avançado → API REST** e **revogue** a chave criada para o MEGA
3. Se você criou webhooks, exclua-os em **WooCommerce → Configurações → Avançado → Webhooks**
