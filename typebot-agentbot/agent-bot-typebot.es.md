# Typebot Agent Bot

Este documento describe cómo Mega se integra con Typebot cuando una bandeja de entrada está conectada a un **agente bot de Typebot**.

## Descripción general

- Los mensajes públicos entrantes en una conversación pendiente se reenvían a Typebot. Si no existe sesión, se inicia una sesión Typebot; de lo contrario, el chat continúa utilizando el id de sesión almacenado.
- Las respuestas de Typebot se colocan en cola como mensajes del bot en la conversación. Cuando el flujo finaliza, Mega devuelve la conversación a la cola humana.
- Un subconjunto de los datos de contacto, conversación y cuenta se envía como **variables prellenadas** a Typebot en la primera solicitud.

## Configuración (Agent Bot → Typebot)

Configure estos campos en el agente bot:

- `api_url` (obligatorio): URL base de Typebot. Por defecto `https://typebot.io`.
- `api_token` (opcional): token Bearer; requerido para Typebots privados.
- `public_name` (obligatorio): nombre/slug público del Typebot.
- `trigger_type` (obligatorio): `all` (cualquier mensaje entrante) o `keyword`.
- `trigger_operator` (disparador por palabra clave): uno de `contains` (predeterminado), `equals`, `starts_with`, `ends_with`, `regex`.
- `trigger_value` (disparador por palabra clave): palabra clave o patrón regex que debe coincidir.
- `finish_keyword` (opcional): contenido del mensaje entrante que fuerza la transferencia y el reinicio de la sesión.
- `debounce_time` (opcional): segundos para retrasar el envío de la solicitud a Typebot (útil cuando llegan varios mensajes seguidos).
- `default_delay_message` (opcional): segundos de espera entre múltiples respuestas de Typebot cuando llegan en lote.
- `expire_in_minutes` (opcional): si se establece, el id de sesión se borra tras este tiempo y la conversación se vuelve a abrir.
- Reglas de ignorar (opcional):
  - `ignore_groups` (booleano): omite Typebot para conversaciones grupales (por ejemplo, grupos de WhatsApp).
  - `ignored_targets` (array): identificadores de correo/telefono que se omiten en Typebot (coincidencia exacta; los teléfonos se normalizan a dígitos).

## Variables prellenadas enviadas a Typebot

Se envían solo en la primera solicitud de una sesión:

- Contacto: `contact_name`, `contact_email`, `contact_phone`, `contact_id`, `contact_labels`, `contact_attributes`, `contact_custom_attribute_<key>`
- Conversación: `conversation_labels`, `conversation_id`, `conversation_display_id`, `conversation_attributes`, `custom_attribute_<key>`
- Cuenta: `account_id`

Los valores de `<key>` se sanitizan a snake_case en minúsculas.

## Flujo de mensajes

- Mega agrega los últimos mensajes públicos entrantes (texto + URLs de adjuntos) en una única carga útil de solicitud. El último id de mensaje se envía como `metadata.replyId`.
- Si hay un id de sesión en el estado, las solicitudes van a `/api/v1/sessions/:sessionId/continueChat`; de lo contrario, a `/api/v1/typebots/:publicName/startChat`.
- Las respuestas de Typebot se secuencian y entregan en la conversación. `default_delay_message` controla el espaciado entre múltiples mensajes.
- Los adjuntos de Typebot se mapean a los tipos de archivo de Mega (imagen, video, audio, archivo, embed/documento). Los videos se convierten en enlaces cuando no se soporta la descarga.
- El texto enriquecido se convierte a texto tipo Markdown (negrita/cursiva/subrayado) manteniendo la separación de bloques.

## Ciclo de vida de la sesión y transferencia

- El estado de la conversación se almacena en `conversation.additional_attributes['typebot']` (id de sesión, id de resultado, marcadores de mensajes pendientes, contadores de secuencia de salida).
- La transferencia ocurre cuando:
  - Typebot marca el flujo como finalizado (estado/palabras clave) **y** se han enviado todos los mensajes pendientes de salida, o
  - Se recibe la `finish_keyword`, o
  - Las reglas de ignorar coinciden con el contacto/número.
- Cerrar o volver a abrir una conversación desencadena el reinicio de la sesión. `expire_in_minutes` también borra el id de sesión y vuelve a abrir la conversación cuando expira el temporizador.

## Consejos para resolver problemas

- Asegúrese de que `public_name` coincida con el slug público publicado en Typebot y que `api_token` esté configurado para bots privados.
- Para los disparadores por palabra clave, confirme que tanto `trigger_operator` como `trigger_value` están configurados.
- Si las respuestas se detienen a mitad del flujo, revise `additional_attributes.typebot` en la conversación en busca de un `session_id` obsoleto y considere usar la palabra clave de finalización o volver a abrir/cerrar la conversación para reiniciarla.
