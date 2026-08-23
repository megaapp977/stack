# Wame API — provedor de canal

[Wame](https://wame.api.br) é uma API de mensageria que entrega **WhatsApp, Instagram Direct e Messenger** por um único contrato. Este documento descreve o que é necessário para expor o Wame como provedor de caixa de entrada, no mesmo modelo dos provedores Evolution, Waha e Uazapi.

Referência completa da API: <https://us.api-wa.me/docs/swagger.json>

---

## Por que integrar

**Três canais, uma integração.** WhatsApp (Cloud API oficial e não-oficial), Instagram Direct e Messenger usam os mesmos endpoints. O canal é escolhido por um campo no corpo da requisição:

```json
{ "to": "5566999999999", "text": "Olá", "provider": "instagram" }
```

`provider` aceita `whatsapp` (padrão), `instagram` e `messenger`.

**Um parser, não quatro.** Instagram e Messenger já entregam num envelope unificado (`object: "wame"`). Configurando `webhookFormat: "meta"`, o WhatsApp — tanto Baileys quanto Cloud API — passa a entregar no mesmo envelope. Quem consome escreve um parser só, e o campo `provider` do envelope diz de qual canal o evento veio: simétrico ao `provider` usado no envio.

**Configuração sem sair do painel.** O Wame expõe endpoint para configurar os webhooks por API. O usuário informa servidor e key na tela de criação da caixa de entrada, e a integração se auto-configura — sem precisar abrir o painel do Wame.

---

## Credenciais

A conexão precisa de **dois campos**:

| Campo | Exemplo | Observação |
|---|---|---|
| Servidor | `https://us.api-wa.me` | Varia por instância. Também existe `https://server.api-wa.me`, e clientes self-host têm domínio próprio |
| Key | `a1b2c3d4...` | Identifica **e** autentica a instância |

A key é o primeiro segmento do path — não há header de autenticação separado:

```
POST https://us.api-wa.me/{key}/message/text
```

> Por ser credencial, a key nunca deve aparecer em log, URL pública ou mensagem de erro exibida ao agente.

---

## Fluxo de conexão sugerido

### 1. Validar a key e descobrir os canais

```bash
curl "https://us.api-wa.me/{key}/instance"
```

```json
{
  "instance": {
    "connected": true,
    "phoneConnected": true,
    "channels": ["whatsapp", "instagram"],
    "user": { "id": "5566999999999", "name": "Loja Exemplo", "imageProfile": "https://..." },
    "status": "connected"
  }
}
```

Serve para três coisas ao mesmo tempo:

- **valida** o par servidor + key (erro aqui = credencial inválida, mostre na tela)
- **`channels`** diz quais canais aquela key realmente tem — permite criar só as caixas cabíveis, sem oferecer um canal que a instância não possui
- **`connected` / `phoneConnected`** alimentam o indicador de conexão da caixa

### 2. Configurar os webhooks automaticamente

```bash
curl -X PUT "https://us.api-wa.me/{key}/instance" \
  -H "Content-Type: application/json" \
  -d '{
    "allowWebhook": true,
    "allowNumber": "all",
    "webhookFormat": "meta",
    "webhookMessage": "https://SEU-PAINEL/webhooks/wame/{inbox}",
    "webhookMessageFromMe": "https://SEU-PAINEL/webhooks/wame/{inbox}",
    "webhookConnection": "https://SEU-PAINEL/webhooks/wame/{inbox}"
  }'
```

> **Uma URL para tudo.** A instância dispara os eventos das três redes para o
> mesmo endereço — não há URL por canal. Quem recebe descobre a rede pelo campo
> `provider` no topo do envelope (`whatsapp`, `instagram` ou `messenger`) e
> roteia para a caixa certa. Por isso a URL deve identificar a **instância**, e
> não o canal.

Cada tipo de evento tem sua própria URL — podem ser iguais ou separadas:

| Campo | Evento | |
|---|---|---|
| `webhookMessage` | mensagens recebidas | recomendado |
| `webhookMessageFromMe` | mensagens enviadas pelo próprio número (eco do celular) | recomendado |
| `webhookConnection` | mudanças de estado da conexão | recomendado |
| `webhookGroup` | eventos de grupo | opcional |
| `webhookHistory` | histórico importado | opcional |
| `webhookQrCode` | QR code para parear | dispensável |

**Sobre conexão:** parear o número é feito no painel do Wame, que já tem o fluxo completo — QR code, código de pareamento, passkey, proxy. O painel de atendimento não precisa reimplementar nada disso, e por isso `webhookQrCode` normalmente fica de fora.

O que vale assinar é o `webhookConnection`, e só para **exibir estado**: quando o número cai, a caixa de entrada marca desconectado em vez de aceitar respostas que vão falhar em silêncio. É leitura, não fluxo de conexão.

`allowNumber` aceita `"all"` ou uma lista de números separados por vírgula, para filtrar quais conversas geram evento.

### 3. Receber mensagens

> **Catálogo de exemplos reais:** <https://us.api-wa.me/assets/examples/webhooks/meta/index.json>
>
> São 45 payloads capturados e versionados — 34 de WhatsApp, 7 de Instagram e 4 de Messenger — incluindo os casos difíceis: resposta a story, menção em story, reel, mensagem editada, reação removida, tipo não suportado, referral de anúncio. Cada item do índice traz `name`, `file`, `field` e `provider`, e o arquivo fica em `.../meta/{file}`. Dá para escrever os testes da integração inteira em cima deles, sem precisar de número conectado.

O payload chega no envelope unificado, com o canal e a instância identificados. `provider` assume `whatsapp`, `instagram` ou `messenger`:

```json
{
  "object": "wame",
  "provider": "whatsapp",
  "instance": "your-instance-id",
  "official": false,
  "entry": [{
    "id": "wame.eW91ci1pbnN0YW5jZS1pZA",
    "changes": [{
      "field": "messages",
      "value": {
        "messaging_product": "whatsapp",
        "metadata": { "display_phone_number": "5566996852025", "phone_number_id": "your-instance-id" },
        "contacts": [{ "profile": { "name": "Fulano" }, "wa_id": "5511999998888" }],
        "messages": [{
          "from": "5511999998888",
          "chat_type": "individual",
          "id": "WAMID_TEXT",
          "timestamp": "1700000000",
          "type": "text",
          "text": { "body": "Olá!" }
        }]
      }
    }]
  }]
}
```

`official` distingue WhatsApp Cloud API (`true`) de não-oficial (`false`). `chat_type` vale `individual` ou `group` — útil para descartar grupo sem inspecionar o JID.

No Instagram e no Messenger a estrutura é a mesma; muda só a identidade do contato:

```json
{
  "object": "wame",
  "provider": "instagram",
  "official": true,
  "entry": [{
    "changes": [{
      "field": "messages",
      "value": {
        "messaging_product": "instagram",
        "contacts": [{
          "wa_id": "",
          "user_id": "1700000000000000",
          "profile": { "name": "Fulano", "username": "fulano", "picture": "https://cdn.instagram.com/pic.jpg" }
        }],
        "messages": [{
          "from": "1700000000000000",
          "from_user_id": "1700000000000000",
          "id": "aWdfEXAMPLEMID",
          "timestamp": "1700000000",
          "type": "text",
          "text": { "body": "Olá!" }
        }]
      }
    }]
  }]
}
```

`wa_id` vem vazio e a identidade está em `user_id` / `from_user_id` — é esse valor que volta como `to` no envio. `profile` traz `username` e `picture`, prontos para preencher o contato.

Eventos que não têm equivalente no formato Meta — QR code, health — chegam no formato nativo do Wame. É híbrido de propósito: nada é descartado.

Os formatos disponíveis em `webhookFormat` são `native` (padrão, payload próprio do Wame), `meta` (recomendado para esta integração) e `both`.

**Mídia recebida.** Não é preciso resolver `media_id` na Meta nem guardar token: o envelope já traz a URL pronta dentro do objeto da mensagem (`image.url`, `audio.url`, `document.url`), apontando para:

```
GET https://us.api-wa.me/{key}/message/{messageId}/media
```

**Atenção — esse endpoint não devolve o binário.** Devolve JSON com o arquivo embutido em base64:

```json
{
  "messageId": "wamid...",
  "mimetype": "audio/ogg",
  "base64": "data:audio/ogg;base64,T2dnUwACAAAA..."
}
```

Quem baixar e salvar a resposta direto acaba com o JSON gravado no lugar da mídia — o player abre em `00:00` e a imagem não carrega. É preciso extrair o campo `base64`, remover o prefixo `data:<mime>;base64,` e decodificar, usando o `mimetype` para definir o content-type e a extensão.

Um detalhe de áudio: notas de voz vêm como `audio/ogg`. Bibliotecas de detecção de tipo costumam reclassificar o arquivo como `audio/opus` ao persistir, e nesse content-type o player do navegador não reproduz — vale normalizar de volta para `audio/ogg`.

**Confirmações de entrega e leitura.** Chegam em `statuses[]`, no mesmo envelope, normalizadas para o formato do WhatsApp nos três canais:

```json
"statuses": [
  { "id": "aWdfEXAMPLEMID", "status": "read", "timestamp": "1700000000", "recipient_id": "1700000000000000" }
]
```

`status` vale `sent`, `delivered`, `read`, `played` ou `failed`. O `read`/`delivery` do Instagram e do Messenger é convertido para esse mesmo shape antes de sair — um tratamento só acende os tiques nos três canais. O `id` é o mesmo devolvido no envio.

### 4. Enviar mensagens

Todos os endpoints aceitam o campo `provider` para escolher o canal, e respondem no mesmo formato:

```json
{ "code": "SENDING", "status": 200, "id": "3EB03800A147DDFB637177", "message": "Message sending" }
```

Guarde o `id`: é ele que volta em `statuses[]` quando a mensagem for entregue e lida. `SENDING` confirma que o Wame aceitou o envio, não que o destinatário recebeu — a entrega é confirmada pelo status.

**Texto**

```bash
curl -X POST "https://us.api-wa.me/{key}/message/text" \
  -H "Content-Type: application/json" \
  -d '{ "to": "5566999999999", "text": "Olá", "provider": "whatsapp" }'
```

**Imagem**

```bash
curl -X POST "https://us.api-wa.me/{key}/message/image" \
  -H "Content-Type: application/json" \
  -d '{ "to": "5566999999999", "url": "https://.../foto.jpg", "caption": "Legenda", "provider": "instagram" }'
```

**Áudio**

```bash
curl -X POST "https://us.api-wa.me/{key}/message/audio" \
  -H "Content-Type: application/json" \
  -d '{ "to": "5566999999999", "url": "https://.../audio.ogg", "provider": "whatsapp" }'
```

**Documento**

```bash
curl -X POST "https://us.api-wa.me/{key}/message/document" \
  -H "Content-Type: application/json" \
  -d '{
    "to": "5566999999999",
    "url": "https://.../arquivo.pdf",
    "mimetype": "application/pdf",
    "fileName": "arquivo.pdf",
    "caption": "Segue em anexo",
    "provider": "whatsapp"
  }'
```

Há também vídeo, localização, contato, template, botões, lista e outros — 43 endpoints de mensagem no total, todos no swagger.

Nos canais sociais, métodos sem equivalente (botões, listas, templates) respondem **HTTP 422** com mensagem explícita, em vez de cair silenciosamente no WhatsApp.

---

## Notas de implementação

**Identidade do contato varia por canal.** No WhatsApp o `to` é o telefone; no Instagram é o IGSID e no Messenger é o PSID. Ao mapear contato para conversa, a chave precisa incluir o canal — um PSID e um telefone podem colidir se guardados no mesmo espaço.

**Áudio.** WhatsApp aceita `ogg/opus` em nota de voz; Instagram e Messenger aceitam `m4a/aac`. Enviar o formato errado falha na entrega.

**Uma key pode ter mais de um canal.** WhatsApp é exclusivo entre oficial e não-oficial, mas Instagram e Messenger convivem com ele na mesma key. Por isso `channels` no `GET /{key}/instance` é uma lista, e uma key pode originar mais de uma caixa de entrada.

---

## Contato

Dúvidas de integração, ambiente de homologação e credencial de teste: <https://wame.api.br>
