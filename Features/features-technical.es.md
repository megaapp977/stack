# MEGA - Detalle Tecnico de Funcionalidades (ES)

Version: Enterprise
Ultima actualizacion: 10 de agosto de 2026
Idioma: Espanol

## 1. Objetivo

Este documento describe como estan implementadas las funcionalidades principales de MEGA a nivel tecnico.
Se complementa con [features.es.md](features.es.md), que esta orientado a presentacion comercial.

## 2. Stack base y arquitectura

- Backend principal: Ruby on Rails.
- Frontend dashboard: Vue 3.
- Overlay Enterprise: extensiones y overrides en carpeta enterprise.
- Jobs asincronos: Sidekiq para procesos en background.
- Tiempo real: Action Cable para eventos de conversaciones, salas y tableros.
- Persistencia: PostgreSQL como base principal.
- Seguridad API: politicas de permisos y control por rol.

## 3. Dominios funcionales

### 3.1 Canales de mensajeria y voz

- WhatsApp Cloud API: canal oficial, templates y eventos de entrega; fuera de la ventana de atención de 24 horas, el servicio rechaza localmente mensajes libres de automatizaciones sin parámetros de plantilla antes de contactar al proveedor.
- Mega Hub para Meta: modo opcional por Super Admin para conectar WhatsApp, Messenger e Instagram usando apps compartidas del Hub; el bloque de credenciales del Hub se configura en Super Admin → Mega Hub, y los inboxes creados siguen enviando por los servicios nativos y reciben eventos reenviados por webhook.
- Salud de conexión de WhatsApp Cloud: los fallos de token manual se muestran sin bloquear el procesamiento de webhooks entrantes, mientras el registro integrado conserva el flujo de reautorización.
- La salud del número de WhatsApp Cloud persiste los datos disponibles del número cuando falla el enriquecimiento opcional del negocio WABA, conserva los últimos metadatos empresariales y registra el error de enriquecimiento por separado.
- Las bandejas de WhatsApp Cloud con registro integrado pueden usar una migración manual guiada y controlada por feature flag hacia una aplicación Meta propia; el flujo valida las credenciales de WABA, número y token antes de actualizar la conexión, mientras la alerta de reautorización sigue visible cuando corresponde.
- En Cloud, `whatsapp_embedded_signup_inbox_creation` es el control único para crear bandejas mediante registro integrado, reconfigurarlas de forma proactiva y reautorizarlas. Las instalaciones propias conservan `whatsapp_reconfigure` para la reconfiguración proactiva; el endpoint exige un administrador y conserva la recuperación cuando se requiere reautorización.
- WhatsApp Evolution, WAHA y Uazapi: proveedores alternativos con soporte multimedia y grupos.
- Los placeholders no soportados de WhatsApp conservan `unsupported_reason`, código y subtipo cuando Meta los entrega. Solo `131060` se clasifica como indisponibilidad por coexistencia; `131051`, otros tipos y registros antiguos usan una explicación neutral. Los mensajes salientes sin contenido enviable o sin respuesta de WAHA se marcan como fallidos y no como contenido entrante no soportado.
- Estado de conexión por proveedor: WAHA, Evolution y Uazapi consultan sus propias APIs y webhooks; la validación de firma de Meta se reserva para WhatsApp Cloud.
- Vinculación WAHA con passkey: detección proactiva de extensión vía `WAHA_PASSKEY_CHROME_EXTENSION_ID`, estados `PASSKEY_REQUIRED` y `PASSKEY_CONFIRMATION_REQUIRED` dentro de `session.status`, challenge por `/auth/passkey/challenge`, flujo temporal por token para aserción, firma con extensión de navegador en `web.whatsapp.com` y confirmación manual por código; los GET sin datos pendientes responden `422`.
- Sincronización global bajo demanda para WAHA y Uazapi: jobs Sidekiq con progreso en Redis, ventanas de 24h/7d, deduplicación por ids del proveedor, reutilización de conversaciones abiertas, descarga asincrónica de multimedia histórica, bloqueo de concurrencia por cuenta y worker dedicado opcional `whatsapp_history_sync` para instalaciones de alto volumen.
- Sincronización por conversación para WAHA y Uazapi: acción manual desde el menú de la conversación, con ventanas de 24h/7d y deduplicación por ids del proveedor.
- Reacciones de WhatsApp: actores del dashboard y tokens de API pueden agregar, reemplazar y remover una reaccion por mensaje sin romper los ecos de WhatsApp Device.
- Notificame: variante oficial orientada a operaciones LATAM.
- Instagram, Facebook, TikTok, Telegram, X, SMS y Email integrados como inboxes.
- Email IMAP con timeout dedicado de procesamiento para evitar jobs colgados en bandejas de correo.
- Diagnóstico de conexión para bandejas Gmail con autenticación IMAP/SMTP XOAUTH2 en vivo, categorías de error seguras, fechas de actividad entrante/saliente reciente y reconexión OAuth exclusiva para administradores.
- Al borrar mensajes o conversaciones de bandejas Gmail, un job asíncrono busca el RFC `Message-ID` guardado, resuelve los IDs opacos de Gmail y elimina permanentemente el mensaje o hilo sin bloquear el borrado local.
- Inferencia del proveedor de email desde registros MX del dominio de registro para sugerir integraciones Gmail u Outlook durante el onboarding.
- Subida de adjuntos con reconocimiento explicito de archivos `.pfx` junto a formatos multimedia y documentales habituales.
- API Channel: canal generico para integrar sistemas propietarios via API/webhooks.
- Formulario pre-chat del widget: las casillas marcadas como obligatorias usan la regla de aceptacion del formulario, por lo que el envio queda bloqueado hasta que se seleccionen; el mensaje localizado de campo obligatorio se conserva.
- Voz Twilio y llamadas WhatsApp Cloud: flujo WebRTC con historial unificado en conversacion; las llamadas Cloud desde perfiles sin conversacion resuelven o crean de forma segura el hilo del contacto respetando la continuidad del inbox y la visibilidad del agente. Los permisos de llamada pueden usar un template aprobado seleccionado desde ReplyBox o configurado como predeterminado por inbox, conservan el WAMID para correlacionar la respuesta y registran el mensaje saliente en la conversacion sin reenviarlo al proveedor. Las consultas a Meta son la fuente de verdad: normalizan y almacenan los estados sin permiso, temporal y permanente, y respetan la acción `start_call` antes de iniciar; cada cambio se registra como actividad, con la fecha de vencimiento recibida para permisos temporales. El cliente y el servidor impiden una segunda llamada activa por agente, incluso entre pestañas. Los candidatos del inbox se determinan con las reglas estándar de asignación —capacidad, equipo y overflow— y se excluyen quienes ya están en llamada; un administrador online que activó notificaciones solo entra como respaldo cuando no queda un agente elegible. Cuando una llamada Cloud está aceptándose, conectándose o activa, la interfaz y el modelo rechazan cambiar agente o equipo; una llamada que solo timbra todavía se puede reasignar y el cambio vuelve a estar disponible al finalizar. Los controles, solicitudes de permiso, inicio y webhooks de llamadas se deshabilitan para canales Cloud marcados como coexistencia con WhatsApp Business App, porque las llamadas continúan en la aplicación WhatsApp Business. Los reportes Twilio normalizan datos desde el modelo Call, las grabaciones nativas opcionales requieren aceptacion del costo de storage y las grabaciones se exponen en conversaciones y reportes de llamadas.
- Control de transcripcion de audio: GPT-4o Mini Transcribe por defecto para notas de voz con Whisper disponible como override por cuenta; las grabaciones mantienen flags por cuenta para habilitacion general y comportamiento por proveedor (WhatsApp Cloud y WaVoIP), normalizacion de audio, diarizacion por turno, transcripcion fiel con GPT-4o Transcribe, etiquetas basadas en el nombre del contacto/agente asignado y reintento manual desde el menu contextual de mensajes de audio sin texto. Las transcripciones almacenadas participan en OpenSearch, el fallback GIN/SQL, los resultados globales de conversaciones y la busqueda de mensajes dentro de una conversacion, conservando los permisos y filtros existentes.
- WaVoIP con persistencia de sesion por inbox y recuperacion segura de credenciales segun rol.

### 3.2 Nucleo de conversaciones

- Las solicitudes de transcripcion por email desde el widget deshabilitan su boton durante el envio y por 15 segundos despues de un envio exitoso, evitando solicitudes repetidas y manteniendo el reintento inmediato despues de un error.
- La visibilidad del feedback CSAT se almacena por inbox en `csat_config.hide_feedback_from_agents`. Los serializadores de mensajes del dashboard y Action Cable eliminan solo `feedback_message` para usuarios de cuenta no administradores, mientras las calificaciones, los datos persistidos y los payloads de administradores y clientes permanecen sin cambios.
- Los mensajes eliminados pueden conservar el texto original y los adjuntos para agentes según `inboxes.show_deleted_message_placeholder`; la API pública, los payloads del widget y los broadcasts Action Cable dirigidos al contacto reemplazan `content` y `processed_message_content` por el aviso de eliminación, omiten `content_attributes.original_content` y `translations`, y exponen una lista vacía de adjuntos sin alterar el registro persistido.
- Estados: open, pending, resolved, snoozed.
- Prioridad: urgencia operativa por conversacion.
- Participantes: colaboracion multiagente en una misma conversacion.
- API de atributos personalizados: `POST .../custom_attributes` conserva el reemplazo como predeterminado y acepta `merge=true` para actualizar solo las claves recibidas; `POST .../destroy_custom_attributes` elimina claves específicas y devuelve los atributos restantes.
- Atributos requeridos Enterprise en macros: el dashboard detecta `resolve_conversation` y `change_status` a resuelta, solicita y persiste los valores faltantes antes de ejecutar, y permite continuar sin resolver al cerrar el diálogo. El overlay de `Macros::ExecutionService` también bloquea la resolución directa cuando faltan valores de definiciones requeridas vigentes; una casilla `false` cuenta como completa y los valores nulos como faltantes.
- Borradores y pinned: continuidad de trabajo por agente.
- Filtros avanzados y vistas personalizadas: segmentacion operativa de alto volumen.
- Orden dedicado por unread en la lista de conversaciones.
- Filtros laterales dedicados: unread, mentions, participating, groups y unattended en sidebar de conversaciones.
- Contadores reactivos en sidebar: unread por tipo de conversacion y mentions por notification_type=conversation_mention.
- Assignment V2: distribucion inteligente con capacidad y reglas.
- Los inboxes exponen `auto_assign_on_agent_reply` para conservar sin responsable las conversaciones no asignadas cuando un agente envia un mensaje saliente.
- Los usuarios multicuenta mantienen un solo selector de avatar, pero sus operaciones de carga y eliminación actúan sobre la membresía `AccountUser` activa. Los payloads de agentes y mensajes priorizan ese avatar y usan como fallback el avatar global de `User`; el comportamiento de usuarios con una sola cuenta sigue siendo global y no se agrega ningún permiso ni toggle de política.
- Equipos: `icon` e `icon_color` se persisten en `teams`, se exponen por API/model JSON y viajan en payloads realtime para listas y selectores de asignacion.
- SLA Enterprise: `AppliedSla` expone deadlines FRT/NRT/RT calculados en backend; cuando la politica usa horarios de negocio, `Sla::BusinessHoursService` consume la configuracion de working hours del inbox y la respuesta JSON entrega `sla_*_due_at` al dashboard. Al resolver una conversación se registra `sla_completed_at`, que congela la duración mostrada de los incumplimientos FRT/NRT/RT; los SLA históricos sin esa marca siguen visibles como incumplidos estáticos. Las conversaciones con contacto bloqueado no aceptan nueva asignacion SLA, se excluyen de procesamiento/reportes y limpian `sla_policy_id`, `applied_sla` y `sla_events` en payloads mientras sigan bloqueadas.
- Drilldown de reportes V2: `/api/v2/accounts/:account_id/reports/drilldown` entrega conversaciones, mensajes o eventos que componen una barra del grafico; `V2::Reports::DrilldownBuilder` valida metrica, bucket, permisos de administrador, paginacion, filtros por cuenta/inbox/agente/equipo/etiqueta, horarios de negocio y serializacion de ultimo mensaje, con rate limit dedicado en Rack::Attack.
- Respuestas predefinidas con adjuntos reutilizables tambien en flujos de nueva conversacion.
- Editor de respuesta con subida de imagenes inline en Email y Widget Web, redimensionado por ProseMirror y render seguro de `cw_image_width`/`cw_image_height`.
- La resolucion de `reply_to` en WhatsApp respeta `conversation_history` buscando identificadores citados en conversaciones anteriores del mismo contact inbox, sin ampliar la busqueda a todos los mensajes de la cuenta. En coexistencia, tambien vincula WAMID de ambito telefono y BSUID que comparten un unico token decodificado; los identificadores malformados o ambiguos permanecen sin vincular.
- Baja de agentes con revision previa de conversaciones asignadas y opcion de desasignar o reasignar en lote respetando acceso por inbox/equipo.
- Las invitaciones de agentes reservan atómicamente capacidad diaria de correo en Redis antes de encolar el email; el límite agotado revierte solo esa invitación y responde HTTP 429, mientras las altas masivas continúan incorporando usuarios existentes.

### 3.3 Comunicacion interna y salas

- Chat Rooms se mantiene como dominio propio sobre la base existente: `chat_rooms`, `chat_room_members` y `chat_room_messages`.
- Los nombres de sala preservan las mayúsculas ingresadas; `chat_rooms` aplica unicidad por cuenta sin distinguir mayúsculas mediante un índice único `account_id, LOWER(name)`.
- Paridad interna extendida con `chat_room_categories`, `chat_room_drafts`, `chat_room_reactions`, `chat_room_polls`, `chat_room_poll_options`, `chat_room_poll_votes` y `chat_room_teams`.
- Tipos de sala: `public_channel`, `private_channel` y `direct_message`, con nombres opcionales para DMs y reutilizacion de DMs existentes por combinacion de miembros.
- API account-scoped para salas, miembros, categorias, borradores, reacciones, encuestas, busqueda, lectura/unread, archivo y estado de escritura.
- Busqueda con `f_unaccent` para canales, DMs y mensajes accesibles por usuario.
- Frontend Vuex `chatRooms` centraliza salas, mensajes, replies de hilo, categorias, borradores y resultados de busqueda; la UI expone filtros, secciones, creacion rapida, DMs, borradores, encuestas, panel lateral de hilo y la edicion de canales desde el menu de acciones del encabezado.
- Realtime via Action Cable y eventos `CHAT_ROOM_*` para creacion/actualizacion/eliminacion de mensajes, salas, reacciones, encuestas, lectura y typing.
- Llamadas de audio/video WebRTC con ciclo de vida en `chat_room_calls`, participantes en `chat_room_call_participants`, senalizacion SDP/ICE efimera mediante `RoomChannel` y tonos reutilizados `ring.mp3`/`calling.mp3`.
- Las cuentas con `chat_room_calls` reciben únicamente `DEFAULT_STUN_URL` de Google; al habilitar `premium_call_connectivity`, `Mega::Calls::IceConfig` obtiene `MEGA_CALL_STUN_URLS`, `MEGA_CALL_TURN_URLS`, `MEGA_CALL_TURN_USERNAME` y `MEGA_CALL_TURN_CREDENTIAL` mediante `GlobalConfigService`. Los valores guardados en Super Admin > Call ICE tienen prioridad, las variables de entorno existentes se migran y TURN solo se publica cuando sus tres campos están completos.
- El video nativo normaliza cámara y pantalla como streams independientes, renegocia un sender de pantalla adicional sin interrumpir la cámara y renderiza un espacio acotado o flotante con escenario de presentación y rail de participantes; Rails autoriza el mute grupal contra el iniciador y la topología P2P sigue orientada a grupos pequeños controlados.
- Las llamadas en vivo requieren ambas features de cuenta, `chat_rooms` y `chat_room_calls`, esta última deshabilitada por defecto; `premium_call_connectivity` solo selecciona el transporte ICE. La API responde `403 feature_disabled` y `RoomChannel` no retransmite SDP/ICE si alguna de las dos features requeridas está apagada, mientras los mensajes históricos siguen visibles.
- En llamadas con tres o mas miembros, cada invitado conserva estado `pending`/`joined`/`declined`; la llamada sigue sonando hasta que todos rechazan o el iniciador la finaliza.
- La audiencia se toma de `OnlineStatusTracker`: una llamada 1:1 no se crea si el destinatario esta offline, y en grupos solo se invitan miembros con presencia `online`.
- Cada llamada crea un unico `chat_room_message` de tipo `voice_call`; el mismo registro cambia entre `ringing`, `in-progress`, `no-answer` y `completed`, alimentando el historial y la vista previa de la sala en tiempo real.
- El flujo de audio reutiliza el patrón visual de `FloatingCallWidget`: posición lógica RTL/LTR, ancho responsive, tokens `n-call-widget-*`, jerarquía de estado e identidad y controles circulares; conserva su estado WebRTC propio y mantiene video aislado.
- Webhooks pueden emitir eventos de chat rooms sin mezclar el contrato de conversaciones con clientes.

### 3.4 Automatizacion y bots

Eventos soportados:

- Conversacion creada y actualizada.
- Mensaje recibido y creado.

- Las reglas diferidas persisten una ejecución pendiente reclamada por regla, conversación y episodio de estado. Un worker programado vuelve a validar la feature flag, la regla y las condiciones antes de ejecutarla; los cambios de estado y las respuestas invalidan el episodio correspondiente.

Condiciones:

- Estado, inbox, etiquetas, idioma, atributos y contenido.
- Nota privada como condicion para reglas internas.

Acciones:

- Asignar agente o equipo.
- Asignar al ultimo agente que respondio.
- Remover asignacion de agente o equipo.
- Etiquetar, cambiar estado/prioridad, enviar webhook, silenciar.

Flow Builder MVP:

- Persistencia: `flow_builder_flows` para borradores editables, `flow_builder_flow_versions` para snapshots publicados y `flow_builder_flow_inboxes` para vincular un flow publicado a un inbox como bot nativo.
- API account-scoped: `/api/v1/accounts/:account_id/flow_builder/flows` con CRUD, `validate`, `publish` y `pause`.
- Ejecuciones account-scoped: `flow_builder_executions` guarda estado, duracion, contexto, snapshot de definicion, pasos parciales/completos, entrada y salida por nodo, incluyendo snapshots de conversacion, mensaje y contacto; API anidada `/flows/:flow_id/executions` lista y muestra detalle.
- Permisos: Pundit admin-only y feature flag `flow_builder`.
- Frontend: ruta `flow_builder_index`, Vuex module `flowBuilder`, canvas con `@vue-flow/core`, nodo Action reutilizando `AutomationActionInput`/`useAutomationValues` para inputs dinamicos, y pestaña de ejecuciones con replay visual readonly, checks verdes por nodo ejecutado, ruta recorrida verde/roja, inspector de payloads por nodo y actualizacion en vivo via ActionCable.
- Estado operativo: switch en listado y editor que publica para activar o llama `pause` para desactivar, reutilizando el estado `published`/`paused` del backend.
- Catalogo inicial: trigger, message, question, condition, switch, set, loop, code, action, handoff, wait, webhook y end.
- Configuracion Wait: el inspector normaliza `duration/unit` legado a `mode/amount/unit/run_at` y soporta espera por intervalo o por fecha/hora especifica; la reanudacion real sigue fuera del runtime inicial.
- Validacion: un solo trigger, edges existentes, sin ciclos, sin self-edge y configuracion minima por tipo de nodo.
- Runtime inicial: flows publicados pueden dispararse desde eventos internos compatibles con Automation (`message_created`, `conversation_created`, `conversation_updated`, `conversation_opened`, `conversation_resolved`) o desde inicio tipo AgentBot por inbox para `message_created`; ejecutan nodos basicos de mensaje, pregunta, condicion, switch, acciones reutilizadas de `ActionService`, handoff y fin; las condiciones y casos switch soportan mensaje, conversacion y datos del contacto.
- Vinculacion AgentBot: al publicar, el inicio tipo AgentBot valida inbox obligatorio y evita conflictos con AgentBot, Dialogflow u otro Flow Builder activo en el mismo inbox; al pausar o cambiar de modo se remueve la vinculacion.
- Limite actual: estado conversacional multi-turn, webhook externo, wait/code/set/loop en runtime y acciones con adjuntos de regla, SLA/Kanban o envio de mensaje duplicado quedan para las siguientes fases.

Bots:

- Agent Bots por inbox con handover inteligente; los selectores de asignación manual solo exponen bots activos configurados en todos los inboxes solicitados.
- Las conversaciones nuevas y campañas sin remitente de un Agent Bot activo quedan pendientes con el bot como propietario; las asignaciones humanas explícitas se preservan y el handover, la apertura humana o la desconexión del bot limpian su propiedad. Dialogflow, Captain y los destinos ignorados no reciben propietario Agent Bot.
- El scope compartido `Conversation.unassigned` exige que tanto `assignee_id` como `assignee_agent_bot_id` sean nulos, por lo que las conversaciones de bot no afectan la lista ni el contador de la cola humana sin asignar.
- El vencimiento de una sesión Webhook usa el handover canónico: abre la conversación, limpia la propiedad del bot y habilita la autoasignación humana solo durante esa transición. Sin agente elegible, conserva la conversación abierta y sin asignar con los reintentos acotados existentes.
- El ReplyBox detecta la propiedad `AgentBot` en conversaciones pendientes, fuerza el modo efectivo `NOTE` sin sobrescribir borradores de respuesta y el banner de takeover reabre y reasigna al agente actual, actualizando también el tipo de asignado local.
- Typebot extendido con comandos MEGA_CMD para asignacion de agente/equipo.
- Typebot ignora reacciones de WhatsApp para evitar inicios o mensajes artificiales.
- Firmas de webhook por canal para validar autenticidad de eventos salientes.

### 3.5 IA Captain

- Proveedores soportados: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: configuracion por inbox con instrucciones y contexto.
- Exclusividad de bots: `InboxBotStatus` identifica Agent Bots activos y Dialogflow como bots externos; Captain no programa respuestas ni resoluciones automáticas para esos inboxes.
- Resumen del asistente: endpoints Enterprise de estadisticas, drilldown y resumen cacheado basados en `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder` y `Captain::OverviewSummaryService`; el cliente reutiliza las estadisticas cargadas para el resumen, cancela solicitudes de estadisticas reemplazadas, reintenta una vez un fallo transitorio y muestra esqueletos de metricas durante la carga. Los resúmenes usan el idioma de la cuenta; el tiempo ahorrado estimado se deriva de las respuestas publicas del asistente usando una suposicion fija de 2 minutos de esfuerzo de agente por respuesta.
- Routing de modelos Captain por feature (`assistant`, `copilot`, `document_faq_generation`, `conversation_faq_matching`, `pdf_faq_generation`, `audio_transcription`, etc.) con override por cuenta y fallback a configuracion global.
- Sugerencias de FAQ desde conversaciones: un trabajo de baja prioridad con mutex extrae solo mensajes públicos de clientes y agentes humanos junto con el contexto del negocio, rechaza conversaciones no aptas y agrupa observaciones semánticamente equivalentes por asistente e idioma; la API Enterprise de revisión lista y previsualiza solo fuentes disponibles para el agente actual, permite editar, aprobar o descartar mientras estén abiertas y bloquea las revisiones ante aprobaciones simultáneas. La aprobación crea una FAQ aprobada y conserva sus observaciones fuente; las FAQ aprobadas y sugerencias descartadas evitan duplicados nuevos.
- Detalles de generación: `GET /api/v1/accounts/:account_id/captain/agent_sessions/:message_id` en Enterprise autoriza la conversación del mensaje, hidrata citas y títulos de escenarios y alimenta el popover de mensajes Captain. Las sesiones se almacenan por mensaje; una sesión de transferencia se asocia a su nota privada no vacía. El modelo y los créditos solo se muestran a superadministradores o en desarrollo.
- Citas confiables de Captain V2: `faq_lookup` entrega índices locales tipados sin URLs; el agente principal permanece sin `response_schema` y emite marcadores `[[citation:N]]` que el servidor convierte en partes persistibles, filtra contra el mapa de la ejecución y renderiza solo documentos HTTP(S) públicos del asistente. Se rechazan credenciales, destinos privados, PDFs y parámetros firmados; `faq_ids` conserva resultados recuperados, mientras `used_faq_ids` y `cited_document_ids` guardan solo selecciones válidas. El historial reutiliza texto limpio y las sesiones legacy con columnas nulas siguen hidratándose desde `faq_ids`.
- Captain Documents: carga, indexacion y auto-sincronizacion por plan con jitter, cola purgable, limites configurables por cuenta y globales, y una vista de detalles con contenido rastreado, metadatos de origen y recuento de preguntas frecuentes generadas.
- Captain Scenarios: reglas de activación y prioridad; la API conserva `tools` enviados explícitamente, normaliza IDs escalares o metadata `{ id }`, valida contra `assistant.available_tool_ids` y mantiene referencias `tool://` cuando se omite el campo. Account MCP publica schemas específicos para crear y actualizar escenarios.
- Captain Custom Tools: integraciones HTTP con GET, POST, PUT, PATCH y DELETE; admiten fragmentos JSON Schema para parámetros complejos y Account MCP publica contratos directos para listar, crear, consultar, actualizar, eliminar y probar tools personalizadas.
- Runtime de tools Captain: conserva íntegro el `inputSchema` de cada servidor MCP, reenvía objetos y arrays sin convertirlos a texto, excluye servidores deshabilitados o desconectados, refresca cada 10 minutos los catálogos conectados que quedaron obsoletos y limita cada solicitud a 128 tools incluyendo handoffs. Un error transitorio de conexión conserva el último catálogo utilizable y mantiene el servidor elegible para reintento; errores permanentes no anuncian un catálogo obsoleto como conectado. En Playground V1 y V2 no existe selección directa mediante `@` o `tool://`. V1 prueba el asistente legacy base sin MCP directas; V2 conserva las tools normales del asistente principal, ejecuta los handoffs y carga en cada agente de escenario únicamente sus tools asignadas, igual que en una conversación real. Las referencias `tool://` dentro de la configuración de escenarios permanecen soportadas. El proxy acepta objetos JSON y cadenas que contienen objetos JSON, pero rechaza JSON inválido o valores no-objeto en vez de vaciarlos silenciosamente.
- MCP Servers nativo por cuenta: endpoints dedicados por slug en /mcp/:account_id/:slug. Las ejecuciones Captain hacia un MCP nativo llevan una prueba firmada, de un solo uso y ligada a cuenta, asistente, servidor, endpoint, tool y argumentos; el handshake permanece neutral y las llamadas MCP externas conservan su identidad normal.
- Los diagnósticos del cliente MCP usan nivel INFO para que el logger DEBUG del transporte no exponga cabeceras de autorización ni pruebas de ejecución.
- Las conexiones nativas a la propia instancia pueden usar `MCP_INTERNAL_BASE_URL`; desarrollo usa por defecto `MCP_INTERNAL_PORT`/3000 y nunca el `PORT` asignado por proceso al worker. Solo se reemplaza el origen, conservando la ruta de cuenta y la firma de la solicitud mientras se evitan timeouts de hairpin por DNS público.
- Un `conversation_message_send` nativo cierra el turno Captain únicamente con un resultado estructurado exitoso que confirma conversación activa, mensaje público saliente y remitente Captain. Su marcador de ciclo de vida, consumo y evento de finalización son idempotentes; los turnos obsoletos se descartan antes del efecto MCP.
- El POST MCP conserva JSON-RPC por `application/json` y admite una extensión `multipart/form-data`: `payload` contiene la solicitud JSON-RPC completa y `attachments[]` los archivos locales.
- Los uploads multipart se limitan a `conversation_message_send`, su alias legado y `outbound_messages_create`; respetan `MAXIMUM_FILE_UPLOAD_SIZE`, con 15 adjuntos combinados para conversaciones y exactamente uno para outbound.
- Multipart es una extensión HTTP de Mega y requiere soporte explícito del cliente; los clientes MCP JSON estándar no la utilizan automáticamente.
- El handshake JSON de carga directa de conversaciones acepta el token API del usuario efectivo del MCP, valida cuenta y conversación mediante el stack API/Pundit y devuelve el destino firmado de Active Storage sin requerir CSRF de navegador.
- `outbound_messages_create` expone en MCP el contrato universal completo: `body` conserva inbox, una identidad de destinatario, texto/media/plantilla y un signed blob; `idempotency_key` se reenvía únicamente como `Idempotency-Key`. Para multimedia admite exactamente una fuente entre signed ID, multipart, `file` con URL HTTPS temporal y `file_base64`; si el mensaje es una plantilla, esa fuente se asigna a `template.parameters.header.media_file` en vez de un adjunto normal.
- El descriptor `_meta["openai/fileParams"]` permite que ChatGPT entregue `file.download_url` y `file.file_id`; Claude y otros clientes pueden usar el mismo descriptor, multipart o el fallback JSON base64. Las URLs pasan por `SafeFetch` con protección SSRF y límite de tamaño; los blobs temporales se purgan si falla la API.
- El servicio outbound verifica que todo signed ID multimedia resuelva a un blob persistido, con tamaño positivo y objeto existente en el almacenamiento. Una referencia inválida, expirada o sin bytes responde `422 invalid_attachment` antes de crear el mensaje o invocar al proveedor.
- OAuth MCP: metadata .well-known, register, authorize, token, refresh token y PKCE.
- Autenticacion dual: Bearer OAuth o Api-Access-Token estatico.
- Catalogo MCP curado para uso cotidiano: herramientas con nombres estables por dominio (conversations, contacts, inboxes, help center, reports, kanban, etc.).
- Tools MCP publicadas: base (account_context, account_actions_list, account_action_call) + catalogo curado; incluye programacion de mensajes, tareas, plantillas, campanas, SLA, politicas, calendario, reportes, Captain, notificaciones y chat interno, ademas del ciclo completo de Help Center; no publica tools de importacion ni exportacion de datos; dinamicas explicitas via allowed_tools.
- Auto-resolve mode: evaluated, legacy o disabled por cuenta. El modo evaluado envía al evaluador el estado de la conversación y el contenido etiquetado de los mensajes no privados; las transferencias y seguimientos pendientes se mantienen abiertas.

### 3.6 CRM y gestion de contactos

- Atributos personalizados por tipo y uso en automatizaciones.
- Control de visibilidad de atributos por rol en Enterprise.
- Etiquetas para contactos y conversaciones.
- El submenu de etiquetas del menu contextual de conversaciones usa busqueda difusa con `picoSearch`, muestra primero las etiquetas asignadas sin alterar el orden fuente de cada grupo y permite seleccionar repetidamente sin quitar el foco de la busqueda. Las consultas en blanco muestran todas las etiquetas y el menu contextual solo se cierra cuando el foco sale de el.
- Empresas con agrupacion por dominio y vista unificada.
- Los payloads de contacto exponen `company_id` cuando Companies esta habilitado; las actualizaciones de contacto pueden asignar o limpiar la empresa y mantienen sincronizado `additional_attributes.company_name`.
- Importacion y exportacion de contactos disponibles para administradores y roles Enterprise con permiso `contact_manage`.
- La importación de Intercom está restringida a administradores y protegida por la funcionalidad `data_import`; las credenciales y mapeos persistentes se almacenan por cuenta.
- Las páginas de contactos y conversaciones se procesan con jobs de Sidekiq, registros idempotentes de elementos/mapeos, logs de omisiones/errores, ejecuciones reanudables y bandejas API por origen.
- Las importaciones inactivas durante 15 minutos pueden reintentarse mediante un endpoint autorizado de cuenta; el reintento bloquea la cuenta y la importación, rota el identificador de ejecución y conserva cursor, estadísticas y errores registrados.
- Bloqueo activo en WhatsApp para descartar mensajes entrantes de contactos bloqueados.

### 3.7 Campanas

- Ongoing campaigns para widget/live chat.
- One-off campaigns para WhatsApp, SMS y API Channel.
- Constructor de templates Meta con ciclo de aprobacion y sincronizacion.
- El endpoint cache-only del inbox lista templates de WhatsApp nativo y Twilio, aplica la clave de nombre exacto de cada proveedor y expone el último intento de sincronización sin consultar a Meta ni Twilio.
- Control de velocidad, rotacion multi-inbox y metricas de ejecucion.

### 3.8 Help Center

- Articulos multi-idioma con estado por idioma.
- Las ediciones de titulo y contenido de articulos publicados se guardan en columnas de borrador, con flujos de revision, publicacion y descarte que preservan la version visible hasta publicar.
- Layouts de portal seleccionables: landing clasica o documentacion con sidebar.
- La analítica del portal se guarda en `portal.config.analytics`; solo los administradores pueden actualizar los identificadores permitidos, que el modelo valida antes de renderizar los scripts de seguimiento públicos.
- Contenido recomendado por locale persistido en `portal.config.popular_content`, con listas ordenadas y límites de 3 categorías y 6 artículos; se omiten registros eliminados o artículos no publicados y se conserva el fallback por popularidad.
- Editor con menu slash, tablas nativas e insercion de enlaces de video compatibles mediante un campo validado; el enlace se convierte en el embed existente para mostrar su vista previa en el editor y el portal publico.
- El menu slash del editor de articulos expone `horizontalRule`, que inserta el nodo horizontal existente de ProseMirror y mueve el cursor al parrafo siguiente.
- Cuando la selección de ProseMirror está dentro de una tabla, el menú slash filtra los comandos de bloque que las celdas Markdown no pueden persistir y conserva solo formatos inline; las flechas y Ctrl+N/P quedan a cargo del menú mientras tenga opciones.
- Creacion de articulos desde la vista de categoria.
- Redimensionado de imagenes dentro del editor de articulos.
- Insercion de articulos en conversacion con busqueda y popover estable.
- Embedding search en Enterprise para busqueda semantica.
- Generacion asistida de FAQs desde PDF con contexto adicional y publicacion selectiva (Enterprise).

### 3.9 Kanban comercial (Mega)

- Embudos con etapas configurables y etapa predeterminada.
- Vista board y list para distintos flujos de trabajo.
- Filtros por inbox, canal, etapa y actividad.
- Filtro por etiquetas de conversacion en board/list y en estadisticas por etapa.
- El formulario compartido de creación carga las etiquetas de la cuenta y envía los títulos seleccionados mediante `kanban_item.labels`; el endpoint de creación las asigna al nuevo ítem antes de su única persistencia, sin modificar las etiquetas de la conversación vinculada. La tarjeta mantiene el endpoint de gestión de etiquetas por ítem.
- Item 360: checklist, notas, adjuntos, ofertas, agentes y atributos.
- Las notas extensas de Kanban usan un diálogo de detalles con Markdown renderizado, scroll limitado al viewport, corte forzado para texto sin separadores, adjuntos y una acción de edición directa sujeta a permisos.
- Busqueda remota de conversaciones/contactos en selectores de relaciones del item.
- Moneda base configurable por cuenta via `accounts.update` (`settings.default_currency`).
- Los consumidores monetarios activos resuelven la moneda con prioridad oferta → item → cuenta → locale mediante el helper/composable compartido; los valores historicos anterior/nuevo se formatean por separado y los importes cero permanecen visibles.
- `funnels/:id/stage_stats` conserva `count` y `total_value` y agrega `value_totals` por etapa (`currency` o `label`, código, total y conteo único de ítems) sobre todo el policy scope filtrado; `KanbanColumn` prioriza ese agregado completo, usa agrupación local solo como compatibilidad y muestra un tooltip accesible con tokens semánticos.
- Ofertas custom monetarias con moneda por oferta (`item_details.offers[].currency`) y override sobre la moneda base.
- Items sin ofertas: se muestran sin moneda y no se agregan a totales monetarios para evitar mezcla por fallback.
- Relacion nativa con contacto y conversacion.
- La sincronizacion Google Calendar a nivel de cuenta puede convertir items con fecha programada/deadline en `CalendarEvent` sin sobrescribir campos Google legacy en `item_details`.
- Los recordatorios se evalúan cada minuto, crean una sola `Notification` idempotente con actor `CalendarEvent` para `created_by_user_id` y reutilizan ActionCable dirigido, Web Push y snooze; los emails invitados nunca determinan el destinatario interno.
- Los controles de calendario del item Kanban solo se montan cuando la cuenta tiene `GoogleCalendarIntegration.connected?` y un `CalendarConnection#calendar_id`; entonces leen `CalendarEvent`/`ExternalCalendarEvent`, exponen link a Google cuando existe y mantienen IDs Google legacy solo como fallback.
- Automatizaciones por etapa y mensajes rapidos.
- Las reglas temporizadas `send_message` capturan al programarse el ID de la conversación principal y el ID del último mensaje entrante. `StageTimeAutomationJob` vuelve a validar la entrada en la etapa y la regla, mientras `KanbanItems::StageFollowUpService` bloquea el ítem, cancela ante una respuesta posterior del contacto y deduplica mediante una clave de ítem/regla/entrada guardada en los atributos del mensaje. El texto y la multimedia persistida en el funnel usan `Messages::MessageBuilder`; el editor Woot compartido expone las variables Liquid del ReplyBox y el concern `Liquidable` del mensaje las resuelve contra la conversación objetivo. Los templates aprobados se muestran y aceptan solo para inboxes configurados `whatsapp_cloud`, conservando sus `template_params` por inbox y la restricción existente de 24 horas.
- Las etapas de entrada guardan `ignore_group_conversations`; al activarlo, `AutoCreateItemJob` no crea ítems para conversaciones cuyo `contact_inbox.source_id` termina en `@g.us`, sin modificar las etapas legacy basadas en condiciones.
- La entrega automática de plantillas de etapa se identifica con `kanban_item_id` y el ID estable de la plantilla en los atributos de contenido del mensaje saliente. El editor de plantillas habilita el selector estándar de variables al escribir `{{`; `Liquidable` resuelve, por ejemplo, `{{contact.name}}` al crear el mensaje saliente. Las plantillas existentes envían una vez por ítem de forma predeterminada; `resend_on_entry` habilita el envío en cada entrada que cumpla las condiciones, mientras que los mensajes rápidos manuales no consultan este historial.
- Las reglas de etapa `notify_team` resuelven miembros de equipos seleccionados y asignados actuales del item al ejecutarse, excluyen al usuario que realizó el movimiento, deduplican usuarios y crean notificaciones en tiempo real `kanban_stage_automation` por usuario. Un banner Kanban no bloqueante muestra una alerta directamente o agrupa varias en una lista expandible con descarte individual o masivo; el envío por email queda excluido intencionalmente.
- Una tarea pendiente de checklist con fecha límite programa una alerta interna para su agente asignado. El job verifica que tarea, responsable y fecha sigan vigentes antes de entregarla, bloquea el ítem Kanban para evitar alertas concurrentes duplicadas y solo recrea una alerta descartada después del intervalo configurado en el funnel mientras la tarea siga pendiente.
- Sincronizacion en tiempo real con lista de chats y panel de contacto.
- `GET /kanban_items?contact_id=<id>` conserva el scope autoritativo de la policy Kanban, resuelve la pertenencia mediante todos los display IDs de conversaciones vinculadas y filtra los ítems abiertos antes de paginar solo para funnels con `settings.contact_panel_contact_wide_items` habilitado. La opción es falsa por defecto; ContactPanel une el resultado ampliado con `currentChat.kanban_items` y lo actualiza con los eventos Kanban.
- El panel de contacto/conversacion reutiliza los candidatos de agentes del funnel y persiste altas/bajas con los endpoints de items Kanban.
- El tablero abre la conversación vinculada desde el icono de canal sin reinicializar sus datos. En móvil, el detalle del item separa el contenido comercial del perfil/acordeones y reutiliza los diálogos de estado, movimiento y agentes desde ContactPanel.
- El bloque Kanban del panel de contacto/conversacion se oculta si el usuario no tiene items visibles ni funnels disponibles para crear items.
- La entrada Kanban del sidebar principal se oculta para usuarios no administradores cuando no tienen funnels activos accesibles.
- Los cambios de agentes del funnel emiten un evento en tiempo real para refrescar sidebar, funnels e items visibles sin recargar.
- Un item Kanban puede vincular varias conversaciones: `conversation_display_id` conserva la conversacion principal por compatibilidad y `item_details.conversation_ids` guarda el conjunto completo; la visibilidad, los filtros, el realtime de la lista de chats y el bloque Kanban del ContactPanel consideran cualquiera de las conversaciones vinculadas. El selector de relaciones se limita a los inboxes del funnel y muestra icono de canal/nombre de inbox.
- `AutoCreateItemJob` garantiza un solo ítem abierto por contacto y funnel: serializa el procesamiento mediante el bloqueo del contacto, reutiliza el ítem abierto más antiguo y agrega la nueva conversación cuando su inbox pertenece al funnel. Los contactos distintos no se infieren por sus datos, los funnels se evalúan de forma independiente y los ítems `won`/`lost` permiten una nueva oportunidad.
- Al abrir una conversación desde el drawer de Kanban, `ConversationSidebar` propaga `hidePreviousConversations` al `ContactPanel` para ocultar el acordeón de conversaciones anteriores; el panel de conversación estándar conserva ese acordeón. La tarjeta deduplica las conversaciones serializadas por `inbox.channel_type` y, si falta, por `inbox_id`, para mostrar un icono por canal y filtra el selector al canal del icono pulsado.
- Si se elimina una conversacion vinculada, el item Kanban queda como historico y se limpia la relacion rota.
- Alcance de acceso consistente en API, cache y eventos en tiempo real: los administradores ven todos los embudos e items; `agent` y el permiso de rol personalizado `kanban_view` reciben solo los recursos autorizados.
- El administrador actual puede asignarse a cualquier ítem, de forma individual o masiva, y removerse individualmente, aunque no pertenezca a `settings.agents` ni a los inboxes del funnel; esta excepción no permite asignar a otros usuarios inelegibles.
- El permiso de rol personalizado `kanban_view` permite operar ítems visibles; `kanban_manage` además crea embudos y queda agregado a `settings.agents` del embudo creado. Solo los embudos asignados se pueden editar en contenido y estructura; no permite eliminar, elegir el predeterminado ni cambiar `unassigned_visibility`.
- Los items conservan `created_by_id`; el creador siempre mantiene visibilidad. Con una conversacion vinculada valida, el responsable actual solo puede verlo si tambien esta seleccionado en el funnel, y cualquier agente asignado manualmente al item puede verlo; un enlace stale solo es visible para administrador y creador.
- `unassigned_visibility` admite `everyone` (valor legado/predeterminado) y `assigned_only`; `everyone` concede a todos los agentes del funnel visibilidad sobre todos sus ítems, incluso si tienen un responsable, mientras `assigned_only` conserva el alcance de los agentes autorizados.
- Cualquier miembro de la cuenta con acceso Kanban puede agregarse a `settings.agents`, independientemente de `settings.inboxes`; un rol personalizado requiere `kanban_view` o `kanban_manage`. Con inboxes configurados, las asignaciones manuales nuevas a ítems requieren acceso a por lo menos uno; al mover un ítem, sus agentes asignados se agregan automáticamente al funnel destino sin cambiar sus permisos de inbox.
- La configuracion global permite lectura a `agent`, `kanban_view`, `kanban_manage` y administradores; crear, editar o eliminar exige administrador. Los endpoints de automatizaciones globales son exclusivos de administrador; `kanban_manage` solo modifica funnels asignados.

### 3.10 Integraciones y extensibilidad

- API universal de salida: `POST /api/v1/accounts/:account_id/outbound_messages` exige `api_access_token` y autorización sobre el inbox; acepta exactamente uno de `phone_number`, `email`, `contact_id` o `source_id`, resuelve o crea contacto/contact-inbox/conversación y entrega texto, un adjunto o una plantilla de WhatsApp mediante `Messages::MessageBuilder` y `SendReplyJob`. En plantillas, renderiza el BODY aprobado sincronizado con sus variables antes de persistir el mensaje, para que el dashboard y los webhooks expongan el contenido enviado. Los templates de canales WhatsApp nativos (no Twilio) con cabecera multimedia aceptan `header.media_file` por multipart o signed blob ID; el servicio lo almacena y genera `header.media_url` para el proveedor. `Idempotency-Key` es opcional: si se omite, cada petición es un envío nuevo; si se proporciona, un reintento idéntico devuelve la respuesta original y un payload diferente responde `409`. El `202` confirma encolado local, no entrega del proveedor.
- Webhooks con payload enriquecido y secreto global HMAC-SHA256.
- Evento `inbox_updated` para cambios de estado y desconexion de inboxes.
- Dashboard Apps para iFrames embebidos por contexto; los usuarios autenticados de la cuenta pueden leerlos, pero solo los administradores pueden crearlos, editarlos o eliminarlos.
- Dashboard Scripts (Super Admin) para personalizacion global sin tocar core.
- Platform Apps para extensiones de alto nivel via API.
- Integraciones de negocio: Slack, Linear, Shopify, WooCommerce, Notion, CRM, Google Calendar y Tareas.
- Tareas está protegida por el feature de cuenta `activities` y un `Integrations::Hook` de cuenta habilitado; el mismo par controla la visibilidad de la integración, acceso API, ruta y entrada del sidebar.
- `/activities` persiste en la query de la ruta la vista calendario/lista y sus criterios operativos. Sin `status` —o con uno inválido— inicia en `all` y no envía filtro; los valores explícitos válidos se conservan. El calendario sigue sin paginar; la lista usa búsqueda por título, orden y agrupación del servidor, y metadatos opcionales de `page`/`per_page`.
- Las consultas de calendario usan la intersección explícita `overlaps_from`/`overlaps_to`. El cliente proyecta una tarea de varios días en cada fecha visible intersectada, no solo en su fecha de inicio.
- La autorización usa tres permisos de rol personalizado: `task_manage` crea tareas y gestiona solo las asignadas al usuario o creadas por él, `task_view_all` agrega lectura global sin edición y `task_reports_view` habilita informes y sus detalles de solo lectura. Los agentes estándar reciben implícitamente el alcance propio/asignado; los administradores conservan acceso total y eliminación exclusiva.
- `AccountTask` es la fuente de verdad para tipo, prioridad, responsable, participantes, invitados, contacto/conversación y enlaces únicos a Kanban y `CalendarEvent`; persiste pendiente/en curso/completada/cancelada y deriva vencida según `ends_at`; todos los IDs se resuelven en la cuenta actual.
- `ActivityType#color` persiste uno de los 22 identificadores de la paleta visual compartida con Google Calendar. Una migración convierte los seis colores legados y la UI reutiliza un único mapa de clases; el estado añade decoración sin sobrescribir el fondo del tipo.
- `outcome_summary` conserva el resultado del cierre y es obligatorio, tanto en UI como en el modelo, para los estados `completed` y `cancelled`; al reabrir se preserva como historial editable.
- `AccountTasks::TriggerDueNotificationsJob` corre cada minuto y crea una única notificación `account_task_due` al llegar `ends_at`, exclusivamente para `assignee_id` y solo mientras la tarea siga pendiente/en curso y Tareas esté disponible. El responsable puede marcarla como vista o posponerla mediante `snoozed_until`; el reactivador global la vuelve a publicar automáticamente. Reprogramar, reasignar o cerrar elimina el aviso anterior para recalcularlo.
- Las raíces recurrentes persisten tipo, intervalo, días y límite por fecha o cantidad. `AccountTasks::RecurrenceService` materializa hasta 100 tareas hijas independientes, hereda responsable/contexto/participantes/Kanban/Google, actualiza ocurrencias abiertas y conserva las ya cerradas.
- Las referencias opcionales de una tarea y su proyección `CalendarEvent` usan `ON DELETE SET NULL`. La tarea conserva snapshots de creador, responsable, contacto, conversación e ítem Kanban; al borrar relaciones limpia los IDs vivos, resincroniza Google y mantiene etiquetas históricas legibles. La cascada de contacto tiene un único propietario por nivel (`ContactInbox` → conversación → mensaje), evitando trabajos duplicados.
- Eliminar un `AccountUser` limpia sincrónicamente sus asignaciones, participaciones y avisos de vencimiento solo en esa cuenta; tras el commit resincroniza los eventos Google afectados para retirar al agente invitado. Eliminar una tarea conserva el ítem Kanban administrado, quita su metadato de propiedad y reintenta una cancelación Google fallida.
- `/account_tasks` coordina transaccionalmente la tarea y un único ítem Kanban, libre o asociado al cliente. La edición actualiza o mueve el mismo ítem y la desvinculación no lo elimina.
- La UI solo carga y muestra Kanban cuando la cuenta tiene `kanban_board`; la API ignora enlaces Kanban nuevos mientras el feature está deshabilitado y conserva cualquier vínculo previo oculto al editar la tarea.
- Al seleccionar una conversación, el editor consulta sus ítems Kanban visibles. Un ítem existente se vincula sin modificarlo y puede compartirse entre varias tareas; “Crear nuevo” conserva el flujo administrado por funnel y etapa.
- El ReplyBox expone la creación rápida solo con feature y hook de Tareas habilitados. Carga tipos, agentes, funnels y capacidades Google bajo demanda, y abre `TaskDialog` con el contacto y la conversación actuales; el diálogo resuelve automáticamente sus ítems Kanban relacionados.
- El ContactPanel muestra un acordeón específico de Tareas con el patrón visual de calendario y consulta `/account_tasks?contact_id=...&status=open`; cada tarjeta muestra el `display_id` estable de la conversación vinculada y el filtro incluye estados persistidos pendiente/en curso, por lo que la proyección vencida y el seguimiento sobreviven al cambio de conversación del contacto.
- `/activities` usa una proyección `CalendarEvent` para sincronización saliente opcional con inicio/fin exactos y asistentes sin duplicados; los fallos externos quedan visibles sin revertir la tarea válida.
- En móvil, `/activities` reorganiza filtros y navegación pero conserva el lienzo mensual de escritorio con desplazamiento horizontal para no comprimir sus celdas. `TaskDialog` limita el área desplazable con `dvh`, apila la cabecera y mantiene el pie fuera del contenido desplazable.
- `TaskDialog` abre registros existentes en modo lectura, pasa explícitamente a edición y solicita `outcome_summary` en un diálogo secundario para concluir/cancelar. Eliminar exige confirmación, solo se muestra a administradores y `AccountTaskPolicy#destroy?` impone la misma restricción en la API.
- El detalle del ítem Kanban muestra la pestaña operativa de Tareas solo con feature y hook habilitados; consulta `/account_tasks?kanban_item_id=...`, mantiene el historial del ítem en una pestaña independiente y precarga contacto, conversación e ítem al crear.
- `AccountTasks::KanbanHistoryService` agrega eventos `account_task_changed` al JSONB acotado del ítem dentro de la transacción local; registra el ciclo de vida y los cambios de vínculo sin duplicarlos como mensajes de conversación.
- El contrato CRUD completo de Tareas y Tipos de tarea con alcance de cuenta se mantiene en las fuentes modulares de `swagger/`, los documentos Swagger resueltos y por audiencia, `docs/openapi.yml` y la colección Postman generada. Documenta filtros, `q`, intersección de intervalo, allowlists de orden seguro, metadatos de paginación opcional, relaciones enriquecidas, recurrencia, condiciones de Kanban/Google, permisos y respuestas de validación.
- Informes agrega una ruta visible solo con feature y hook activos y `GET /account_tasks/reports?since=&until=`, autorizado únicamente para administradores y `task_reports_view`. `AccountTasks::ReportsService` filtra por `COALESCE(ends_at, starts_at)`, genera la serie diaria de completadas y agrega total, pendientes, en curso, completadas, vencidas y canceladas por responsable y tipo. Cada tarea pertenece a una sola categoría de estado. Los gráficos y filas abren un drawer que consulta `GET /account_tasks` por fecha programada, responsable o tipo; desde allí se reutiliza `TaskDialog` en modo lectura. No expone métricas de tiempo transcurrido porque la tarea todavía no persiste una marca temporal de cierre.
- Los controles Google solo aparecen con feature habilitado, integración conectada, conexión activa saliente, módulo `calendar` habilitado y al menos un calendario escribible. El selector de destino e invitados externos se revelan después de activar “Sincronizar”.
- Google Calendar usa APIs OAuth/config con scope de cuenta, `CalendarConnection` seleccionado, `CalendarEvent` interno y mapeo de proveedor en `ExternalCalendarEvent`; `settings.import_all_calendars` controla el alcance entrante separado del `calendar_id` saliente concreto.
- La ruta operativa `/app/accounts/:accountId/calendar` lee `calendar_events` locales para dia, semana, mes, lista, crear, editar, cancelar, sync al guardar y sync manual de respaldo. `CalendarSync::PollConnectionsJob` corre cada cinco minutos e importa cambios Google con `last_polled_at` por calendario guardado en `CalendarConnection.settings`; los eventos eliminados en Google borran sus proyecciones locales vinculadas, y las recurrencias se expanden entre un año atras y cinco años adelante.
- La navegación, ruta operativa, acción del compositor y sección del panel de conversación exigen el feature de cuenta y `GoogleCalendarIntegration.connected?` con un `CalendarConnection#calendar_id`; los usuarios con rol personalizado además necesitan `calendar_manage`, y la configuración de la integración sigue siendo solo administrativa.
- La vista mensual limita a dos eventos por celda para reservar espacio al control `+N más`; el clic derecho abre acciones del evento y cada fila conserva acceso al editor. El color se guarda en `metadata.color_id`; el borrado permanente requiere administrador y elimina primero el evento vinculado de Google antes de borrar su registro local.
- Las respuestas de `calendar_events` incluyen resumenes ligeros de contacto, conversacion e item Kanban para selectores buscables; el payload de edicion envia `null` para desvincular relaciones.
- El selector de relaciones del calendario busca items Kanban en toda la cuenta, sin heredar el funnel activo, y acepta IDs de items (incluido el formato `#ID`).
- Las tareas del checklist tienen su propia sincronizacion con Google Calendar y su propio calendario de destino; cada tarea sincronizada se guarda como un evento independiente vinculado por `checklist_item_id`.
- El agente asignado al checklist se agrega como invitado de Google y recibe el recordatorio de la plataforma; al completar o eliminar la tarea se cancelan el evento y el recordatorio pendiente.
- El compositor de conversaciones carga la conexion de cuenta y los calendarios escribibles antes de abrir el `CalendarEventDialog` compartido; la accion explicita “Crear y enviar” formatea el resultado `saved` con campos localizados y lo envia una sola vez mediante `createPendingMessageAndSend`, usando `metadata.google_meet_url` sin reintentar la creacion si falla el mensaje.
- El panel de contacto filtra `calendar_events` por `conversation_display_id`, recalcula cada 30 segundos el avance Inicio–Fin para un punto pulsante verde (<50%), amarillo (50–90%) o rojo (≥90%), opaca los vencidos, reutiliza `CalendarEventDialog` y consume actualizaciones de eventos guardados.
- `GoogleCalendar::EventMapperService` mapea metadata del evento a campos Google de ubicacion, invitados, recordatorios, recurrencia simple, disponibilidad, visibilidad, permisos de invitados y Google Meet.
- El editor responsive usa filas con iconos, selector de zonas IANA y chips removibles; la columna lateral coloca el contexto con la marca de instalación debajo de los permisos de invitados, con búsquedas flotantes y el icono del inbox en cada resultado de conversación; persiste destino y URL Meet.
- Google Calendar soporta importacion manual entrante via `google_calendar_integration/import_events` y backfill Kanban legacy via `google_calendar_integration/backfill_kanban`; los triggers de Flow Builder quedan diferidos.
- Assets de notificaciones y PWA generados dinamicamente desde `NOTIFICATION_ICON` (por defecto `/favicon-badge-16x16.png`), con fallback a `LOGO_THUMBNAIL`, fondo configurable y cache invalidada por asset, color y timestamp del blob; el favicon conserva `LOGO_THUMBNAIL`, cambia a `NOTIFICATION_ICON` al recibir un mensaje con la pestaña oculta o sin foco y se restaura al regresar.

### 3.11 Registro y onboarding

- Finalizacion guiada del perfil de cuenta mediante endpoint administrativo dedicado `/api/v1/accounts/:account_id/onboarding`.
- Persistencia del sitio web como URL completa para consumidores posteriores como Help Center y enriquecimiento de marca.
- Separacion entre actualizaciones generales de cuenta y el cierre del paso `account_details`.
- El callback OAuth de Instagram conserva la pista firmada `return_to` para volver al setup de la bandeja cuando la autorizacion parte del onboarding.

### 3.12 Layouts de email con marca

- La feature flag de cuenta `branded_email_templates` habilita un layout de respaldo por cuenta y una sobrescritura por bandeja de Email.
- `EmailTemplate` separa los layouts por instalación, cuenta y bandeja; valida la sintaxis Liquid y el slot `content_for_layout`, y limita el cuerpo a 256 KiB (262.144 caracteres).
- El endpoint del layout de cuenta y la actualización de una bandeja de Email requieren administrador; los esquemas OpenAPI exponen el mismo límite.

### 3.13 Seguridad y cumplimiento

- 2FA/MFA, SAML/SSO, roles personalizados y logs de auditoria. El informe de evidencia de eliminaciones de Super Admin consulta únicamente filas retenidas de `audits`: la destrucción de Inbox usa su asociación con Account, mientras que las de Conversation y Contact usan la captura de `account_id` en `audited_changes`; nunca une registros vivos eliminados ni infiere eliminaciones de Message.
- Los registros de sesion de usuario soportan una etiqueta `custom_name` editable por el agente; la metadata de IP queda interna y no se expone en los payloads de sesiones del dashboard.
- La autenticación web envía un ID persistente y validado de 128 bits por perfil de navegador como client ID del token. Las pestañas reutilizan un único `UserSession`, la reautenticación rota el mismo espacio y un logout exitoso elimina token y fila. Los perfiles nuevos reciben el selector bloqueante solo al alcanzar `MAX_USER_SESSIONS`; los clientes móviles conservan IDs generados y expulsión silenciosa.
- El estado de dashboard para cuenta suspendida mantiene visible el widget de soporte y expone una accion explicita para contactar soporte. En Cloud, el guard de rutas y la pantalla suspendida permiten solo a los administradores acceder a facturación para restaurar la cuenta; los agentes permanecen en la pantalla suspendida. Super Admin valida una categoría y un motivo de hasta 256 caracteres, agrega eventos en `accounts.internal_attributes.suspensions`, conserva la metadata interna no relacionada y permite corregir el último evento sin alterar su marca de tiempo.
- Proteccion de licencia en despliegues Mega.
- Observabilidad de release para trazabilidad por version.

## 4. Operacion y validacion

### Paridad API y colección Postman

Las rutas soportadas bajo `/api`, `/platform/api` y `/public/api` se comparan con OpenAPI 3.1 por método y ruta normalizada. La validación detecta operaciones ausentes, obsoletas o duplicadas; no afirma cobertura de pruebas para cada campo de respuesta. `bundle exec rake swagger:build` regenera Swagger y `swagger/postman_collection.json` con estructura lista para importar: los recursos de Application API aparecen en el primer nivel y heredan `api_access_token`; Mega Platform APIs y Mega Public APIs conservan carpetas y autenticación propias. Las variables de colección centralizan `host`, `api_version`, `account_id`, credenciales e identificadores de ruta. Los mensajes multimedia incluyen ejemplos separados para seleccionar un archivo con `multipart/form-data` o utilizar un `signed_blob_id` con JSON. `Idempotency-Key` aparece desactivado y es opcional; puede habilitarse con `{{$guid}}` o una clave fija para comprobar reintentos.

Los mensajes programados se pueden crear a nivel de cuenta con `contact_id` e `inbox_id`, sin requerir una conversación, dentro de una conversación, o mediante `POST /scheduled_outbound_messages` con teléfono, email, `contact_id` o `source_id`: este último resuelve o crea el contacto/contact-inbox en una transacción y deja el mensaje pendiente sin crear una conversación anticipadamente. Los fallidos se recuperan mediante acciones explícitas y autorizadas: el reintento los deja pendientes y encola el envío inmediato; la reprogramación exige una fecha futura, preserva contenido, plantilla y adjuntos, y mantiene los límites de cuenta y conversación. Un mensaje enviado puede volver a programarse como una copia independiente no recurrente, con fecha futura y contenido editables, conservando destinatario, inbox, plantilla y adjuntos.

Checklist recomendado por cambio funcional:

1. Validar permisos por rol y alcance de cuenta.
2. Probar eventos realtime (Action Cable) en escenarios concurrentes.
3. Ejecutar tests unitarios del dominio afectado.
4. Ejecutar prueba manual en navegador para el flujo completo.
5. Verificar i18n en ES, EN y PT-BR para textos nuevos.

## 5. Referencias tecnicas relacionadas

- [docs/kanban_api_reference.md](../kanban_api_reference.md)
- [docs/chat_rooms_api_reference.md](../chat_rooms_api_reference.md)
- [docs/scheduled_messages_api_reference.md](../scheduled_messages_api_reference.md)
- [docs/platform_banners_api_reference.md](../platform_banners_api_reference.md)
- [docs/whatsapp_voice_calls.md](../whatsapp_voice_calls.md)
