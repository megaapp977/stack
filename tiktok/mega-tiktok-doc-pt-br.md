# Criação do canal TikTok no MEGA

## Passo 1 — Conta TikTok Business
É necessário possuir uma **TikTok Business Account**. Contas pessoais não são suportadas.

## Passo 2 — Solicitar permissões especiais
O acesso à **TikTok Business Messaging API** exige aprovação manual.

1. Acesse a documentação oficial:
   https://business-api.tiktok.com/portal/docs?id=1832183871604753
2. Solicite acesso à *Business Messaging API*.
3. Informe:
   - Caso de uso (suporte, atendimento ao cliente, etc.).
   - Plataforma: MEGA.
4. Aguarde a aprovação do TikTok.

## Passo 3 — Criar aplicativo no TikTok Developers
1. Crie um aplicativo no TikTok Developers.
2. Obtenha:
   - App ID
   - App Secret
3. Configure:
   - Redirect URL: `https://<FRONTEND_URL>/tiktok/callback`
   - Webhook URL: `https://<FRONTEND_URL>/webhooks/tiktok`

## Passo 4 — Configurar o MEGA
1. Defina as variáveis de ambiente:
   - `TIKTOK_APP_ID`
   - `TIKTOK_APP_SECRET`
2. Ative a integração TikTok no painel administrativo.

## Passo 5 — Autorizar a conta
1. Inicie a conexão pelo MEGA.
2. Você será redirecionado ao TikTok.
3. Autorize os acessos solicitados.

## Passo 6 — Criação automática do canal
Após a autorização:
- O MEGA valida o acesso.
- O canal TikTok é criado ou atualizado.
- O inbox associado é habilitado.

## Passo 7 — Recebimento de mensagens
O TikTok envia eventos para o webhook configurado.
As mensagens entram automaticamente no MEGA.

## Limitações
- Apenas contas Business.
- Apenas mensagens iniciadas pelo usuário.
- Tipos suportados: texto, imagem, post compartilhado.
- Restrições regionais conforme o TikTok.
