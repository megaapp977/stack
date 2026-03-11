# Configuração do Canal TikTok no MEGA

Configure a integração do TikTok Business Messaging para gerenciar conversas do TikTok diretamente do MEGA.

A integração do canal TikTok permite gerenciar conversas do TikTok Business Messaging diretamente do MEGA. Os agentes podem receber e responder mensagens de usuários do TikTok, visualizar publicações compartilhadas e manipular anexos de imagens, tudo dentro do painel do MEGA.

A configuração do canal TikTok consiste em **7 etapas principais**.

## Pré-requisitos

Antes de começar, certifique-se de ter:

1. **Instância MEGA auto-hospedada** acessível através de uma URL pública com HTTPS
2. **Conta TikTok Business** registrada em uma região elegível
3. **Configurações de mensagem direta**: Sua conta TikTok Business deve estar configurada para aceitar mensagens diretas de todos. Caso contrário, você precisará aceitar manualmente as mensagens no aplicativo TikTok. [Saiba como atualizar suas configurações de mensagem](https://ads.tiktok.com/help/article/how-to-update-your-tiktok-direct-message-permission-for-tiktok-messaging-ads?lang=en)
4. **Conta de desenvolvedor do TikTok** em [developers.tiktok.com](https://developers.tiktok.com/)
5. **Acesso à API Business Messaging do TikTok** - [solicitar permissões especiais](https://business-api.tiktok.com/portal/docs?id=1832183871604753) (requer aprovação manual)
6. **Acesso de Super Admin** à sua instância do MEGA

> **⚠️ Aviso Importante**  
> A API Business Messaging do TikTok tem restrições regionais. **Atualmente NÃO está disponível** para contas registradas no Espaço Econômico Europeu (EEA), Suíça ou Reino Unido. Apenas contas TikTok Business são suportadas — contas pessoais não são compatíveis.

## Passo 1 — Criar Conta de Desenvolvedor do TikTok

1. Acesse [developers.tiktok.com](https://developers.tiktok.com/) e cadastre-se
2. Verifique seu endereço de e-mail
3. Aceite os Termos de Serviço

## Passo 2 — Registrar Sua Aplicação

![Criar aplicativo TikTok](images/tiktok-create-app.png)

1. Vá para [business-api.tiktok.com/portal/apps](https://business-api.tiktok.com/portal/apps) e crie um novo aplicativo
2. Preencha os campos obrigatórios:
   - **App Name**: ex. "Sua Empresa - MEGA"
   - **App Description**: Descrição breve do seu caso de uso de mensagens
   - **App Icon**: Faça upload do logo da sua empresa
   - **Terms of Service URL**: URL dos termos de serviço da sua empresa
   - **Privacy Policy URL**: URL da política de privacidade da sua empresa
3. Após criado, anote seu **App ID** (client key) e **App Secret** (client secret)

## Passo 3 — Solicitar Acesso à API Business Messaging

O acesso à **API Business Messaging do TikTok** exige aprovação manual. Para instruções detalhadas, consulte o [guia oficial de acesso à Business Messaging API](https://business-api.tiktok.com/portal/docs?id=1832184145137922).

1. Abra seu aplicativo no Portal de Desenvolvedores do TikTok
2. Navegue até o produto Business Messaging API
3. Envie uma solicitação incluindo:
   - Seu caso de uso (ex. suporte ao cliente via MEGA)
   - Como você lidará com os dados do usuário
   - Detalhes da sua organização
4. Aguarde a revisão e aprovação do TikTok

> **📌 Nota:** A aprovação geralmente leva alguns dias, mas pode demorar mais para acessos especializados. Você não pode prosseguir com a integração até que sua solicitação seja aprovada.

## Passo 4 — Configurar Permissões e URLs do Aplicativo

Após a aprovação, configure o seguinte no Portal de Desenvolvedores do TikTok:

### Permissões Necessárias

Depois que seu aplicativo for aprovado, certifique-se de que a permissão **TikTok Accounts** esteja habilitada em **Scope of permission** nas configurações do seu aplicativo.

![Permissão TikTok Accounts](images/tiktok-accounts-permission.png)

### URL de Redirecionamento de Autorização

Defina a URL de redirecionamento de autorização para:

```text
https://<FRONTEND_URL>/tiktok/callback
```

Substitua `<FRONTEND_URL>` pela URL da sua instalação do MEGA.

## Passo 5 — Configurar o MEGA

### Configuração do Super Admin

1. Faça login na sua instância do MEGA como Super Admin
2. Navegue até a configuração do aplicativo para TikTok
3. Insira seu **TikTok App ID** e **TikTok App Secret**
4. Clique em Enviar

**Alternativamente**, você pode definir estas variáveis de ambiente:

```bash
TIKTOK_APP_ID=seu_tiktok_app_id
TIKTOK_APP_SECRET=seu_tiktok_app_secret
TIKTOK_API_VERSION=v1.3
```

> **📌 Nota:** A versão padrão da API do TikTok é `v1.3`. Configure isso se você quiser usar uma versão diferente da API do TikTok. Certifique-se de que esteja prefixada com 'v'.

**Reinicie o servidor MEGA** após fazer as alterações.

### Habilitar o Recurso TikTok

1. No Super Admin, navegue até Contas
2. Selecione a conta onde você deseja habilitar o TikTok
3. Em Recursos, habilite o canal TikTok
4. Salve as alterações

> **📌 Nota:** O TikTok só aparecerá nas opções de canal da caixa de entrada depois que você configurar o App ID e App Secret e habilitar o recurso para a conta.

## Passo 6 — Configurar Webhook

Configure o webhook do TikTok para receber mensagens recebidas. Abra um console Rails no seu servidor MEGA:

```bash
bundle exec rails console
```

Execute o seguinte comando para registrar a URL de callback do webhook:

```ruby
Tiktok::AuthClient.update_webhook_callback
```

Isso define a URL do webhook para `https://<FRONTEND_URL>/webhooks/tiktok`.

Você pode verificar a configuração do webhook executando:

```ruby
Tiktok::AuthClient.webhook_callback
```

> **⚠️ Aviso:** O webhook deve ser configurado depois de definir o TikTok App ID e App Secret no Super Admin. Se você alterar seu domínio do MEGA, precisará executar este comando novamente.

## Passo 7 — Conectar o MEGA com Sua Conta TikTok

1. Inicie a conexão do MEGA (Settings → Inboxes → Add Inbox → TikTok)
2. Você será redirecionado ao TikTok para autorizar
3. Aprove as permissões solicitadas

Após a autorização:

- O MEGA valida o acesso
- O canal TikTok é criado ou atualizado
- A caixa de entrada associada é habilitada
- As mensagens recebidas aparecem automaticamente no MEGA

## Solução de Problemas

### Canal TikTok não aparece nas opções de caixa de entrada

- Verifique se o recurso TikTok está habilitado para a conta no Super Admin
- Confirme se `TIKTOK_APP_ID` e `TIKTOK_APP_SECRET` estão configurados corretamente
- Reinicie o servidor MEGA após as alterações de configuração

### Falha na autorização OAuth

- Certifique-se de que a URL de redirecionamento no Portal de Desenvolvedores do TikTok corresponda exatamente a `https://<FRONTEND_URL>/tiktok/callback`
- Verifique se seu aplicativo TikTok tem todos os scopes necessários habilitados
- Confirme se seu aplicativo TikTok está aprovado para a Business Messaging API

### Não está recebendo mensagens recebidas

- Verifique se o webhook está configurado executando `Tiktok::AuthClient.webhook_callback` no console Rails
- Certifique-se de que a URL do webhook seja publicamente acessível via HTTPS
- Confirme se sua conta TikTok Business está em uma região elegível
- Revise os logs do Sidekiq para erros de `Webhooks::TiktokEventsJob`

### Falha no envio de mensagens

- Verifique se a janela de resposta de 48 horas expirou
- Confirme se o token de acesso é válido — o MEGA renova automaticamente os tokens, mas se o token de atualização expirar (30 dias), o canal precisará de reautorização
- Certifique-se de estar enviando um tipo de mensagem suportado (apenas texto ou uma única imagem)
- Verifique os logs do Sidekiq para erros de `SendReplyJob`

### Canal mostra "Reautorização Necessária"

Isso acontece quando tanto o token de acesso (cerca de 24 horas) quanto o token de atualização (cerca de 30 dias) expiraram, normalmente devido à inatividade.

1. Vá para Settings → Inboxes → selecione a caixa de entrada do TikTok
2. Clique em Reauthorize
3. Complete o fluxo OAuth do TikTok novamente

### Falha na verificação de assinatura do webhook

- Certifique-se de que `TIKTOK_APP_SECRET` corresponda ao secret no seu Portal de Desenvolvedores do TikTok
- Verifique a sincronização do relógio do servidor — a verificação de assinatura do TikTok requer timestamps dentro de 5 segundos

## Limitações

- Apenas contas Business (contas pessoais não suportadas)
- Apenas mensagens iniciadas por usuários
- Janela de resposta de 48 horas
- Tipos de mensagem suportados: texto, imagem, publicação compartilhada
- Não disponível no EEA, Suíça ou Reino Unido
- Tokens de acesso expiram (~24 horas, renovação automática)
- Tokens de atualização expiram (~30 dias, requer reautorização manual)
