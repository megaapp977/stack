# MEGA - Detalle Tecnico de Funcionalidades (ES)

Version: Enterprise
Ultima actualizacion: 15 de julio de 2026
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

- WhatsApp Cloud API: canal oficial, templates y eventos de entrega.
- Mega Hub para Meta: modo opcional por Super Admin para conectar WhatsApp, Messenger e Instagram usando apps compartidas del Hub; el bloque de credenciales del Hub se configura en Super Admin → Mega Hub, y los inboxes creados siguen enviando por los servicios nativos y reciben eventos reenviados por webhook.
- Salud de conexión de WhatsApp Cloud: los fallos de token manual se muestran sin bloquear el procesamiento de webhooks entrantes, mientras el registro integrado conserva el flujo de reautorización.
- WhatsApp Evolution, WAHA y Uazapi: proveedores alternativos con soporte multimedia y grupos.
- Estado de conexión por proveedor: WAHA, Evolution y Uazapi consultan sus propias APIs y webhooks; la validación de firma de Meta se reserva para WhatsApp Cloud.
- Vinculación WAHA con passkey: detección proactiva de extensión vía `WAHA_PASSKEY_CHROME_EXTENSION_ID`, estados `PASSKEY_REQUIRED` y `PASSKEY_CONFIRMATION_REQUIRED` dentro de `session.status`, challenge por `/auth/passkey/challenge`, flujo temporal por token para aserción, firma con extensión de navegador en `web.whatsapp.com` y confirmación manual por código; los GET sin datos pendientes responden `422`.
- Sincronización global bajo demanda para WAHA y Uazapi: jobs Sidekiq con progreso en Redis, ventanas de 24h/7d, deduplicación por ids del proveedor, reutilización de conversaciones abiertas, descarga asincrónica de multimedia histórica, bloqueo de concurrencia por cuenta y worker dedicado opcional `whatsapp_history_sync` para instalaciones de alto volumen.
- Sincronización por conversación para WAHA y Uazapi: acción manual desde el menú de la conversación, con ventanas de 24h/7d y deduplicación por ids del proveedor.
- Reacciones de WhatsApp: actores del dashboard y tokens de API pueden agregar, reemplazar y remover una reaccion por mensaje sin romper los ecos de WhatsApp Device.
- Notificame: variante oficial orientada a operaciones LATAM.
- Instagram, Facebook, TikTok, Telegram, X, SMS y Email integrados como inboxes.
- Email IMAP con timeout dedicado de procesamiento para evitar jobs colgados en bandejas de correo.
- Inferencia del proveedor de email desde registros MX del dominio de registro para sugerir integraciones Gmail u Outlook durante el onboarding.
- Subida de adjuntos con reconocimiento explicito de archivos `.pfx` junto a formatos multimedia y documentales habituales.
- API Channel: canal generico para integrar sistemas propietarios via API/webhooks.
- Voz Twilio y llamadas WhatsApp Cloud: flujo WebRTC con historial unificado en conversacion; los reportes Twilio normalizan datos desde el modelo Call, las grabaciones nativas opcionales requieren aceptacion del costo de storage y las grabaciones se exponen en conversaciones y reportes de llamadas.
- Control de transcripcion de audio: GPT-4o Mini Transcribe por defecto para notas de voz con Whisper disponible como override por cuenta; las grabaciones mantienen flags por cuenta para habilitacion general y comportamiento por proveedor (WhatsApp Cloud y WaVoIP), normalizacion de audio, diarizacion por turno, transcripcion fiel con GPT-4o Transcribe, etiquetas basadas en el nombre del contacto/agente asignado y reintento manual desde el menu contextual de mensajes de audio sin texto.
- WaVoIP con persistencia de sesion por inbox y recuperacion segura de credenciales segun rol.

### 3.2 Nucleo de conversaciones

- Estados: open, pending, resolved, snoozed.
- Prioridad: urgencia operativa por conversacion.
- Participantes: colaboracion multiagente en una misma conversacion.
- Borradores y pinned: continuidad de trabajo por agente.
- Filtros avanzados y vistas personalizadas: segmentacion operativa de alto volumen.
- Orden dedicado por unread en la lista de conversaciones.
- Filtros laterales dedicados: unread, mentions, participating, groups y unattended en sidebar de conversaciones.
- Contadores reactivos en sidebar: unread por tipo de conversacion y mentions por notification_type=conversation_mention.
- Assignment V2: distribucion inteligente con capacidad y reglas.
- Los inboxes exponen `auto_assign_on_agent_reply` para conservar sin responsable las conversaciones no asignadas cuando un agente envia un mensaje saliente.
- Equipos: `icon` e `icon_color` se persisten en `teams`, se exponen por API/model JSON y viajan en payloads realtime para listas y selectores de asignacion.
- SLA Enterprise: `AppliedSla` expone deadlines FRT/NRT/RT calculados en backend; cuando la politica usa horarios de negocio, `Sla::BusinessHoursService` consume la configuracion de working hours del inbox y la respuesta JSON entrega `sla_*_due_at` al dashboard. Las conversaciones con contacto bloqueado no aceptan nueva asignacion SLA, se excluyen de procesamiento/reportes y limpian `sla_policy_id`, `applied_sla` y `sla_events` en payloads mientras sigan bloqueadas.
- Drilldown de reportes V2: `/api/v2/accounts/:account_id/reports/drilldown` entrega conversaciones, mensajes o eventos que componen una barra del grafico; `V2::Reports::DrilldownBuilder` valida metrica, bucket, permisos de administrador, paginacion, filtros por cuenta/inbox/agente/equipo/etiqueta, horarios de negocio y serializacion de ultimo mensaje, con rate limit dedicado en Rack::Attack.
- Respuestas predefinidas con adjuntos reutilizables tambien en flujos de nueva conversacion.
- Editor de respuesta con subida de imagenes inline en Email y Widget Web, redimensionado por ProseMirror y render seguro de `cw_image_width`/`cw_image_height`.
- La resolucion de `reply_to` en WhatsApp respeta `conversation_history` buscando identificadores citados en conversaciones anteriores del mismo contact inbox, sin ampliar la busqueda a todos los mensajes de la cuenta.
- Baja de agentes con revision previa de conversaciones asignadas y opcion de desasignar o reasignar en lote respetando acceso por inbox/equipo.

### 3.3 Comunicacion interna y salas

- Chat Rooms se mantiene como dominio propio sobre la base existente: `chat_rooms`, `chat_room_members` y `chat_room_messages`.
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

Condiciones:

- Estado, inbox, etiquetas, idioma, atributos y contenido.
- Nota privada como condicion para reglas internas.

Acciones:

- Asignar agente o equipo.
- Asignar al ultimo agente que respondio.
- Remover asignacion de agente o equipo.
- Etiquetar, cambiar estado/prioridad, enviar webhook, silenciar.

Bots:

- Agent Bots por inbox con handover inteligente; los selectores de asignación manual solo exponen bots activos configurados en todos los inboxes solicitados.
- Typebot extendido con comandos MEGA_CMD para asignacion de agente/equipo.
- Typebot ignora reacciones de WhatsApp para evitar inicios o mensajes artificiales.
- Firmas de webhook por canal para validar autenticidad de eventos salientes.

### 3.5 IA Captain

- Proveedores soportados: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: configuracion por inbox con instrucciones y contexto.
- Resumen del asistente: endpoints Enterprise de estadisticas, drilldown y resumen cacheado basados en `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder` y `Captain::OverviewSummaryService`; el tiempo ahorrado estimado se deriva de las respuestas publicas del asistente usando una suposicion fija de 2 minutos de esfuerzo de agente por respuesta.
- Routing de modelos Captain por feature (`assistant`, `copilot`, `document_faq_generation`, `pdf_faq_generation`, `audio_transcription`, etc.) con override por cuenta y fallback a configuracion global.
- Captain Documents: carga, indexacion y auto-sincronizacion por plan con jitter, cola purgable, limites configurables por cuenta y globales, y una vista de detalles con contenido rastreado, metadatos de origen y recuento de preguntas frecuentes generadas.
- Captain Scenarios: reglas de activacion y prioridad.
- Captain Custom Tools: integraciones HTTP con GET, POST, PUT, PATCH y DELETE.
- MCP Servers nativo por cuenta: endpoints dedicados por slug en /mcp/:account_id/:slug.
- OAuth MCP: metadata .well-known, register, authorize, token, refresh token y PKCE.
- Autenticacion dual: Bearer OAuth o Api-Access-Token estatico.
- Catalogo MCP curado para uso cotidiano: herramientas con nombres estables por dominio (conversations, contacts, inboxes, help center, reports, kanban, etc.).
- Tools MCP publicadas: base (account_context, account_actions_list, account_action_call) + catalogo curado; incluye lectura/busqueda de Help Center con `help_center_articles_list`, `help_center_articles_search`, `help_center_articles_get` y `help_center_categories_list`; dinamicas explicitas via allowed_tools.
- Auto-resolve mode: evaluated, legacy o disabled por cuenta. El modo evaluado envía al evaluador el estado de la conversación y el contenido etiquetado de los mensajes no privados; las transferencias y seguimientos pendientes se mantienen abiertas.

### 3.6 CRM y gestion de contactos

- Atributos personalizados por tipo y uso en automatizaciones.
- Control de visibilidad de atributos por rol en Enterprise.
- Etiquetas para contactos y conversaciones.
- Empresas con agrupacion por dominio y vista unificada.
- Los payloads de contacto exponen `company_id` cuando Companies esta habilitado; las actualizaciones de contacto pueden asignar o limpiar la empresa y mantienen sincronizado `additional_attributes.company_name`.
- Importacion y exportacion de contactos disponibles para administradores y roles Enterprise con permiso `contact_manage`.
- La importación de Intercom está restringida a administradores y protegida por la funcionalidad `data_import`; las credenciales y mapeos persistentes se almacenan por cuenta.
- Las páginas de contactos y conversaciones se procesan con jobs de Sidekiq, registros idempotentes de elementos/mapeos, logs de omisiones/errores, ejecuciones reanudables y bandejas API por origen.
- Bloqueo activo en WhatsApp para descartar mensajes entrantes de contactos bloqueados.

### 3.7 Campanas

- Ongoing campaigns para widget/live chat.
- One-off campaigns para WhatsApp, SMS y API Channel.
- Constructor de templates Meta con ciclo de aprobacion y sincronizacion.
- Control de velocidad, rotacion multi-inbox y metricas de ejecucion.

### 3.8 Help Center

- Articulos multi-idioma con estado por idioma.
- Layouts de portal seleccionables: landing clasica o documentacion con sidebar.
- Editor con menu slash y tablas nativas.
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
- Gestion de etiquetas desde la tarjeta del item con endpoint API por item.
- Item 360: checklist, notas, adjuntos, ofertas, agentes y atributos.
- Busqueda remota de conversaciones/contactos en selectores de relaciones del item.
- Moneda base configurable por cuenta via `accounts.update` (`settings.default_currency`).
- Ofertas custom monetarias con moneda por oferta (`item_details.offers[].currency`) y override sobre la moneda base.
- Items sin ofertas: se muestran sin moneda y no se agregan a totales monetarios para evitar mezcla por fallback.
- Relacion nativa con contacto y conversacion.
- La sincronizacion Google Calendar a nivel de cuenta puede convertir items con fecha programada/deadline en `CalendarEvent` sin sobrescribir campos Google legacy en `item_details`.
- Los recordatorios se evalúan cada minuto, crean una sola `Notification` idempotente con actor `CalendarEvent` para `created_by_user_id` y reutilizan ActionCable dirigido, Web Push y snooze; los emails invitados nunca determinan el destinatario interno.
- Los controles de calendario del item Kanban leen `CalendarEvent`/`ExternalCalendarEvent`, exponen link a Google cuando existe y mantienen IDs Google legacy solo como fallback.
- Automatizaciones por etapa y mensajes rapidos.
- Sincronizacion en tiempo real con lista de chats y panel de contacto.
- El panel de contacto/conversacion reutiliza los candidatos de agentes del funnel y persiste altas/bajas con los endpoints de items Kanban.
- El bloque Kanban del panel de contacto/conversacion se oculta si el usuario no tiene items visibles ni funnels disponibles para crear items.
- La entrada Kanban del sidebar principal se oculta para usuarios no administradores cuando no tienen funnels activos accesibles.
- Los cambios de agentes del funnel emiten un evento en tiempo real para refrescar sidebar, funnels e items visibles sin recargar.
- Un item Kanban puede vincular varias conversaciones: `conversation_display_id` conserva la conversacion principal por compatibilidad y `item_details.conversation_ids` guarda el conjunto completo; la visibilidad, los filtros, el realtime de la lista de chats y el bloque Kanban del ContactPanel consideran cualquiera de las conversaciones vinculadas. El selector de relaciones se limita a los inboxes del funnel y muestra icono de canal/nombre de inbox.
- Si se elimina una conversacion vinculada, el item Kanban queda como historico y se limpia la relacion rota.
- Alcance de acceso consistente en API, cache y eventos en tiempo real: los administradores ven todos los embudos e items; `agent` y el permiso de rol personalizado `kanban_view` reciben solo los recursos autorizados.
- El permiso de rol personalizado `kanban_manage` incluye tablero y administrador; los embudos que contienen ítems autorizados se exponen en modo lectura, y solo los asignados por `settings.agents` se pueden editar en contenido y estructura. No permite crear, duplicar, eliminar, elegir el predeterminado ni cambiar `unassigned_visibility`.
- Los items conservan `created_by_id`; el creador siempre mantiene visibilidad. Con una conversacion vinculada valida, el responsable actual solo puede verlo si tambien esta seleccionado en el funnel, y cualquier agente asignado manualmente al item puede verlo; un enlace stale solo es visible para administrador y creador.
- `unassigned_visibility` admite `everyone` (valor legado/predeterminado) y `assigned_only`; determina la visibilidad de items sin atribucion directa o de conversaciones vinculadas sin responsable.
- Los candidatos de `settings.agents` deben tener acceso a por lo menos uno de los inboxes de `settings.inboxes`; la union de esos inboxes se recalcula al configurarlos y bloquea nuevas atribuciones invalidas.
- La configuracion global permite lectura a `agent`, `kanban_view`, `kanban_manage` y administradores; crear, editar o eliminar exige administrador. Los endpoints de automatizaciones globales son exclusivos de administrador; `kanban_manage` solo modifica funnels asignados.

### 3.10 Integraciones y extensibilidad

- Webhooks con payload enriquecido y secreto global HMAC-SHA256.
- Evento `inbox_updated` para cambios de estado y desconexion de inboxes.
- Dashboard Apps para iFrames embebidos por contexto; los usuarios autenticados de la cuenta pueden leerlos, pero solo los administradores pueden crearlos, editarlos o eliminarlos.
- Dashboard Scripts (Super Admin) para personalizacion global sin tocar core.
- Platform Apps para extensiones de alto nivel via API.
- Integraciones de negocio: Slack, Linear, Shopify, WooCommerce, Notion, CRM y Google Calendar.
- Google Calendar usa APIs OAuth/config con scope de cuenta, `CalendarConnection` seleccionado, `CalendarEvent` interno y mapeo de proveedor en `ExternalCalendarEvent`; `settings.import_all_calendars` controla el alcance entrante separado del `calendar_id` saliente concreto.
- La ruta operativa `/app/accounts/:accountId/calendar` lee `calendar_events` locales para dia, semana, mes, lista, crear, editar, cancelar, sync al guardar y sync manual de respaldo. `CalendarSync::PollConnectionsJob` corre cada cinco minutos e importa cambios Google con `last_polled_at` por calendario guardado en `CalendarConnection.settings`; las recurrencias se expanden entre un año atras y cinco años adelante.
- La navegación, ruta operativa, acción del compositor y sección del panel de conversación exigen el feature de cuenta, credenciales OAuth globales completas y `GoogleCalendarIntegration.connected?` con un `CalendarConnection#calendar_id`; los payloads iniciales exponen únicamente booleanos de disponibilidad y configuración.
- La vista mensual limita a dos eventos por celda para reservar espacio al control `+N más`; el clic derecho abre acciones del evento y cada fila conserva acceso al editor. El color se guarda en `metadata.color_id` y el borrado permanente requiere administrador.
- Las respuestas de `calendar_events` incluyen resumenes ligeros de contacto, conversacion e item Kanban para selectores buscables; el payload de edicion envia `null` para desvincular relaciones.
- El selector de relaciones del calendario busca items Kanban en toda la cuenta, sin heredar el funnel activo, y acepta IDs de items (incluido el formato `#ID`).
- Las tareas del checklist tienen su propia sincronizacion con Google Calendar y su propio calendario de destino; cada tarea sincronizada se guarda como un evento independiente vinculado por `checklist_item_id`.
- El agente asignado al checklist se agrega como invitado de Google y recibe el recordatorio de la plataforma; al completar o eliminar la tarea se cancelan el evento y el recordatorio pendiente.
- El compositor de conversaciones carga la conexion de cuenta y los calendarios escribibles antes de abrir el `CalendarEventDialog` compartido; la accion explicita “Crear y enviar” formatea el resultado `saved` con campos localizados y lo envia una sola vez mediante `createPendingMessageAndSend`, usando `metadata.google_meet_url` sin reintentar la creacion si falla el mensaje.
- El panel de contacto filtra `calendar_events` por `conversation_display_id`, recalcula cada 30 segundos el avance Inicio–Fin para un punto pulsante verde (<50%), amarillo (50–90%) o rojo (≥90%), opaca los vencidos, reutiliza `CalendarEventDialog` y consume actualizaciones de eventos guardados.
- `GoogleCalendar::EventMapperService` mapea metadata del evento a campos Google de ubicacion, invitados, recordatorios, recurrencia simple, disponibilidad, visibilidad, permisos de invitados y Google Meet.
- El editor responsive usa filas con iconos, selector de zonas IANA y chips removibles; la columna lateral coloca el contexto MEGA vertical debajo de los permisos de invitados, con búsquedas flotantes y el icono del inbox en cada resultado de conversación; persiste destino y URL Meet.
- Google Calendar soporta importacion manual entrante via `google_calendar_integration/import_events` y backfill Kanban legacy via `google_calendar_integration/backfill_kanban`; los triggers de Flow Builder quedan diferidos.
- Assets PWA generados dinamicamente desde configuracion global, con fondo de icono configurable y cache invalidada por logo, color y timestamp del blob.

### 3.11 Registro y onboarding

- Finalizacion guiada del perfil de cuenta mediante endpoint administrativo dedicado `/api/v1/accounts/:account_id/onboarding`.
- Persistencia del sitio web como URL completa para consumidores posteriores como Help Center y enriquecimiento de marca.
- Separacion entre actualizaciones generales de cuenta y el cierre del paso `account_details`.
- El callback OAuth de Instagram conserva la pista firmada `return_to` para volver al setup de la bandeja cuando la autorizacion parte del onboarding.

### 3.12 Seguridad y cumplimiento

- 2FA/MFA, SAML/SSO, roles personalizados y logs de auditoria.
- Los registros de sesion de usuario soportan una etiqueta `custom_name` editable por el agente; la metadata de IP queda interna y no se expone en los payloads de sesiones del dashboard.
- El estado de dashboard para cuenta suspendida mantiene visible el widget de soporte y expone una accion explicita para contactar soporte.
- Proteccion de licencia en despliegues Mega.
- Observabilidad de release para trazabilidad por version.

## 4. Operacion y validacion

### Paridad API y colección Postman

Las rutas soportadas bajo `/api`, `/platform/api` y `/public/api` se comparan con OpenAPI 3.1 por método y ruta normalizada. La validación detecta operaciones ausentes, obsoletas o duplicadas; no afirma cobertura de pruebas para cada campo de respuesta. `bundle exec rake swagger:build` regenera Swagger y `swagger/postman_collection.json`, organizada en `Account API Token`, `Platform App Token` y `Public / No Token`, con variables de credencial independientes.

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
