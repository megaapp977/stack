# Configuración de Webhooks WaVoIP para Grabaciones

## Descripción

Esta guía explica cómo configurar los webhooks de WaVoIP para recibir notificaciones automáticas cuando las grabaciones de llamadas están listas para descargar.

## Por qué es necesario

WaVoIP procesa las grabaciones de forma asíncrona. Después de que termina una llamada, la grabación pasa por varios estados:

- `RECORDING` - Grabación en progreso
- `MIXING` - Procesando/mezclando audio
- `READY` - ¡Grabación lista para descargar!
- `DISABLED` - Grabaciones deshabilitadas
- `EMPTY_RECORDING` - Llamada muy corta, sin grabación

Sin el webhook configurado, el sistema hace polling (reintentos cada vez más espaciados) esperando que la grabación esté lista, lo cual puede fallar si tarda mucho tiempo.

**Con el webhook configurado**, WaVoIP notifica automáticamente cuando la grabación está lista, y se descarga inmediatamente.

## Configuración

### 1. Obtener la URL del Webhook

Tu URL de webhook es:

```
https://TU-DOMINIO.com/webhooks/wavoip
```

Por ejemplo:

- Producción: `https://app.tuempresa.com/webhooks/wavoip`
- Desarrollo: `https://staging.tuempresa.com/webhooks/wavoip`

### 2. Configurar en WaVoIP

1. Accede al panel de WaVoIP: <https://app.wavoip.com/devices>
2. Selecciona el dispositivo que deseas configurar
3. En el menú lateral, ve a **Integraciones > Webhook**
4. Ingresa la URL del webhook (del paso 1)
5. Haz clic en **Guardar**
6. **Importante**: Habilita el evento `RECORD`

### 3. Verificar la configuración

Después de configurar, realiza una llamada de prueba corta. Deberías ver en los logs:

```
[WaVoIP Webhook] Received event: RECORD
[WaVoIP Webhook] Recording READY for call 123456
[WaVoIP Recording Webhook] ✅ Recording attached successfully
```

## Formato del Webhook

WaVoIP envía webhooks con estos eventos:

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

## Troubleshooting

### Las grabaciones no se descargan

1. **Verifica la URL del webhook** - Asegúrate de que sea accesible públicamente
2. **Revisa los logs** - Busca `[WaVoIP Webhook]` para ver si llegan los eventos
3. **Prueba manualmente** - Haz una solicitud POST de prueba:

   ```bash
   curl -X POST https://tu-dominio.com/webhooks/wavoip \
     -H "Content-Type: application/json" \
     -d '{"type":"RECORD","whatsapp_call_id":"test123","record_status":"READY"}'
   ```

### El webhook no llega

1. Verifica que el dispositivo tenga el webhook habilitado en WaVoIP
2. Confirma que el evento `RECORD` está seleccionado
3. Revisa si hay firewalls bloqueando las solicitudes de WaVoIP

### La grabación se descarga pero está vacía

Esto puede ocurrir si la llamada fue muy corta. WaVoIP envía `record_status: "EMPTY_RECORDING"` para estas llamadas.

## Sistema de respaldo (Polling)

Si el webhook no está configurado o falla, el sistema automáticamente:

1. Intenta descargar la grabación con reintentos exponenciales
2. Espera hasta 4 horas con reintentos cada vez más espaciados
3. Marca el mensaje como "fallido" si no puede descargar después de todos los intentos

**Recomendación**: Siempre configura el webhook para mayor confiabilidad.

## Referencias

- [Documentación oficial de WaVoIP - Grabación](https://wavoip.gitbook.io/api/gravacao)
- [Documentación oficial de WaVoIP - Webhook](https://wavoip.gitbook.io/api/webhook-beta)
