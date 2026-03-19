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
- Agentes: `agents_json` (array JSON con id, name, availability_status), `agents_formatted` (lista numerada con emoji de disponibilidad, ej: `1. 🟢 Juan`)
- Equipos: `teams_json` (array JSON con id y name), `teams_formatted` (lista numerada, ej: `1. Ventas`)

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

## MEGA_CMD — Intercepción local de comandos

Dado que un servidor Typebot externo generalmente no puede hacer llamadas HTTP de vuelta a la instancia de Mega (firewalls, aislamiento de red Docker, etc.), MEGA_CMD proporciona una forma de ejecutar acciones localmente sin webhooks.

### Cómo funciona

1. En tu flujo de Typebot, incluye una **burbuja de texto** con un marcador de comando: `[MEGA_CMD:acción:valor]`
2. Cuando Mega recibe la respuesta de Typebot, intercepta el marcador **antes** de enviar el mensaje a la conversación.
3. El comando se ejecuta del lado del servidor (ej: asignar un agente o equipo).
4. El marcador se elimina del texto — el usuario final nunca lo ve.

### Acciones soportadas

| Acción | Valor | Ejemplo | Descripción |
|--------|-------|---------|-------------|
| `assign_agent` | ID del agente | `[MEGA_CMD:assign_agent:5]` | Asigna el agente con id 5 a la conversación |
| `assign_team` | ID del equipo | `[MEGA_CMD:assign_team:3]` | Asigna el equipo con id 3 a la conversación |

### Ejemplo en un flujo de Typebot

Una burbuja de texto en Typebot puede contener:

```text
¡Gracias! Serás conectado con nuestro equipo de soporte en breve.
[MEGA_CMD:assign_team:3]
```

El usuario ve solo: *"¡Gracias! Serás conectado con nuestro equipo de soporte en breve."*

El comando puede combinarse con texto regular. También se soportan múltiples comandos en el mismo mensaje.

## Placeholders de listas — Menús numerados dinámicos

La interpolación de variables de Typebot puede ser poco confiable al construir listas numeradas para WhatsApp (no soporta botones). Mega provee **placeholders de listas** del lado del servidor que se reemplazan con listas numeradas generadas dinámicamente antes de entregar el mensaje.

### Placeholders disponibles

| Placeholder | Se reemplaza con |
|-------------|-----------------|
| `[TEAMS_LIST]` | Lista numerada de todos los equipos de la cuenta, ordenados por nombre. Ejemplo: `1. Ventas\n2. Soporte` |
| `[AGENTS_LIST]` | Lista numerada de agentes en línea con emoji de disponibilidad. Ejemplo: `1. 🟢 Juan\n2. 🟢 María` |

### Cómo usar en un flujo de Typebot

En una burbuja de texto, incluye el placeholder:

```text
Por favor selecciona un equipo:

[TEAMS_LIST]

0. ⬅️ Volver al menú
```

Mega reemplaza `[TEAMS_LIST]` con la lista numerada real antes de entregar el mensaje.

### Escape de listas Markdown

Las listas numeradas (ej: `1. Ventas`) normalmente serían parseadas como listas ordenadas por el renderizador Markdown del dashboard, lo que renumera los ítems (ej: convirtiendo `0.` en `3.`). Mega inserta un espacio de ancho cero (U+200B) entre el dígito-punto y el espacio para evitar esto, manteniendo la numeración original tanto en WhatsApp como en el dashboard.

## Acceso API con token de bot

Para soportar las variables prellenadas con datos de agentes y equipos, los siguientes endpoints de la API son accesibles con tokens de bot:

- `GET /api/v1/accounts/:id/agents` — Listar agentes
- `GET /api/v1/accounts/:id/teams` — Listar equipos
- `GET /api/v1/accounts/:id/contacts` — Listar/crear/actualizar contactos
