# Configuração de Webhooks WaVoIP para Gravações

## Descrição

Este guia explica como configurar os webhooks do WaVoIP para receber notificações automáticas quando as gravações de chamadas estiverem prontas para download.

## Por que é necessário

O WaVoIP processa as gravações de forma assíncrona. Depois que uma chamada termina, a gravação passa por vários estados:

- `RECORDING` - Gravação em andamento
- `MIXING` - Processando/mixando áudio
- `READY` - Gravação pronta para download!
- `DISABLED` - Gravações desabilitadas
- `EMPTY_RECORDING` - Chamada muito curta, sem gravação

Sem o webhook configurado, o sistema faz polling (tentativas cada vez mais espaçadas) esperando que a gravação esteja pronta, o que pode falhar se demorar muito tempo.

**Com o webhook configurado**, o WaVoIP notifica automaticamente quando a gravação está pronta, e ela é baixada imediatamente.

## Configuração

### 1. Obter a URL do Webhook

Sua URL de webhook é:

```
https://SEU-DOMINIO.com/webhooks/wavoip
```

Por exemplo:

- Produção: `https://app.suaempresa.com/webhooks/wavoip`
- Desenvolvimento: `https://staging.suaempresa.com/webhooks/wavoip`

### 2. Configurar no WaVoIP

1. Acesse o painel do WaVoIP: <https://app.wavoip.com/devices>
2. Selecione o dispositivo que deseja configurar
3. No menu lateral, vá em **Integrações > Webhook**
4. Insira a URL do webhook (do passo 1)
5. Clique em **Salvar**
6. **Importante**: Habilite o evento `RECORD`

### 3. Verificar a configuração

Após configurar, faça uma chamada de teste curta. Você deverá ver nos logs:

```
[WaVoIP Webhook] Received event: RECORD
[WaVoIP Webhook] Recording READY for call 123456
[WaVoIP Recording Webhook] ✅ Recording attached successfully
```

## Formato do Webhook

O WaVoIP envia webhooks com estes eventos:

### Evento RECORD

```json
{
    "type": "RECORD",
    "action": "UPDATE",
    "whatsapp_call_id": 123456,
    "id_session": 789,
    "record_status": "READY",
    "record_url": "https://storage.wavoip.com/123456"
}
```

### Evento CALL

```json
{
    "type": "CALL",
    "action": "CREATE",
    "whatsapp_call_id": 123456,
    "status": "ACTIVE",
    "direction": "INCOMING",
    "duration": 45,
    "record_status": "RECORDING"
}
```

## Solução de Problemas

### As gravações não são baixadas

1. **Verifique a URL do webhook** - Certifique-se de que seja acessível publicamente
2. **Revise os logs** - Procure por `[WaVoIP Webhook]` para ver se os eventos estão chegando
3. **Teste manualmente** - Faça uma requisição POST de teste:

   ```bash
   curl -X POST https://seu-dominio.com/webhooks/wavoip \
     -H "Content-Type: application/json" \
     -d '{"type":"RECORD","whatsapp_call_id":"test123","record_status":"READY"}'
   ```

### O webhook não chega

1. Verifique se o dispositivo tem o webhook habilitado no WaVoIP
2. Confirme que o evento `RECORD` está selecionado
3. Verifique se há firewalls bloqueando as requisições do WaVoIP

### A gravação é baixada mas está vazia

Isso pode ocorrer se a chamada foi muito curta. O WaVoIP envia `record_status: "EMPTY_RECORDING"` para essas chamadas.

## Sistema de backup (Polling)

Se o webhook não estiver configurado ou falhar, o sistema automaticamente:

1. Tenta baixar a gravação com tentativas exponenciais
2. Aguarda até 4 horas com tentativas cada vez mais espaçadas
3. Marca a mensagem como "falhou" se não conseguir baixar depois de todas as tentativas

**Recomendação**: Sempre configure o webhook para maior confiabilidade.

## Referências

- [Documentação oficial do WaVoIP - Gravação](https://wavoip.gitbook.io/api/gravacao)
- [Documentação oficial do WaVoIP - Webhook](https://wavoip.gitbook.io/api/webhook-beta)
