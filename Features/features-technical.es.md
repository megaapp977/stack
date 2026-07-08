# MEGA - Detalle Tecnico de Funcionalidades (ES)

Version: Enterprise
Ultima actualizacion: 3 de julio de 2026
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
- Mega Hub para Meta: modo opcional por Super Admin para conectar WhatsApp, Messenger e Instagram usando apps compartidas del Hub; los inboxes creados siguen enviando por los servicios nativos y reciben eventos reenviados por webhook.
- Salud de conexión de WhatsApp Cloud: los fallos de token manual se muestran sin bloquear el procesamiento de webhooks entrantes, mientras el registro integrado conserva el flujo de reautorización.
- WhatsApp Evolution, WAHA y Uazapi: proveedores alternativos con soporte multimedia y grupos.
- Vinculación WAHA con passkey: detección proactiva de extensión vía `WAHA_PASSKEY_CHROME_EXTENSION_ID`, aviso de instalación, estado/webhook `passkey.required`, flujo temporal por token para challenge/aserción, firma con extensión de navegador en `web.whatsapp.com` y confirmación manual por código cuando WAHA emite `passkey.confirmation.required`.
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
- Frontend Vuex `chatRooms` centraliza salas, mensajes, replies de hilo, categorias, borradores y resultados de busqueda; la UI expone filtros, secciones, creacion rapida, DMs, borradores, encuestas y panel lateral de hilo.
- Realtime via Action Cable y eventos `CHAT_ROOM_*` para creacion/actualizacion/eliminacion de mensajes, salas, reacciones, encuestas, lectura y typing.
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

- Agent Bots por inbox con handover inteligente.
- Typebot extendido con comandos MEGA_CMD para asignacion de agente/equipo.
- Typebot ignora reacciones de WhatsApp para evitar inicios o mensajes artificiales.
- Firmas de webhook por canal para validar autenticidad de eventos salientes.

### 3.5 IA Captain

- Proveedores soportados: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: configuracion por inbox con instrucciones y contexto.
- Resumen del asistente: endpoints Enterprise de estadisticas, drilldown y resumen cacheado basados en `Captain::AssistantStatsBuilder`, `Captain::AssistantStatsWindow`, `Captain::AssistantDrilldownBuilder` y `Captain::OverviewSummaryService`; el tiempo ahorrado estimado se deriva de las respuestas publicas del asistente usando una suposicion fija de 2 minutos de esfuerzo de agente por respuesta.
- Routing de modelos Captain por feature (`assistant`, `copilot`, `document_faq_generation`, `pdf_faq_generation`, `audio_transcription`, etc.) con override por cuenta y fallback a configuracion global.
- Captain Documents: carga, indexacion y auto-sincronizacion por plan con jitter, cola purgable y limites configurables por cuenta y globales.
- Captain Scenarios: reglas de activacion y prioridad.
- Captain Custom Tools: integraciones HTTP con GET, POST, PUT, PATCH y DELETE.
- MCP Servers nativo por cuenta: endpoints dedicados por slug en /mcp/:account_id/:slug.
- OAuth MCP: metadata .well-known, register, authorize, token, refresh token y PKCE.
- Autenticacion dual: Bearer OAuth o Api-Access-Token estatico.
- Catalogo MCP curado para uso cotidiano: herramientas con nombres estables por dominio (conversations, contacts, inboxes, help center, reports, kanban, etc.).
- Tools MCP publicadas: base (account_context, account_actions_list, account_action_call) + catalogo curado; incluye lectura/busqueda de Help Center con `help_center_articles_list`, `help_center_articles_search`, `help_center_articles_get` y `help_center_categories_list`; dinamicas explicitas via allowed_tools.
- Auto-resolve mode: evaluated, legacy o disabled por cuenta.

### 3.6 CRM y gestion de contactos

- Atributos personalizados por tipo y uso en automatizaciones.
- Control de visibilidad de atributos por rol en Enterprise.
- Etiquetas para contactos y conversaciones.
- Empresas con agrupacion por dominio y vista unificada.
- Los payloads de contacto exponen `company_id` cuando Companies esta habilitado; las actualizaciones de contacto pueden asignar o limpiar la empresa y mantienen sincronizado `additional_attributes.company_name`.
- Importacion y exportacion de contactos disponibles para administradores y roles Enterprise con permiso `contact_manage`.
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
- Automatizaciones por etapa y mensajes rapidos.
- Sincronizacion en tiempo real con lista de chats y panel de contacto.

### 3.10 Integraciones y extensibilidad

- Webhooks con payload enriquecido y secreto global HMAC-SHA256.
- Evento `inbox_updated` para cambios de estado y desconexion de inboxes.
- Dashboard Apps para iFrames embebidos por contexto.
- Dashboard Scripts (Super Admin) para personalizacion global sin tocar core.
- Platform Apps para extensiones de alto nivel via API.
- Integraciones de negocio: Slack, Linear, Shopify, WooCommerce, Notion y CRM.
- Assets PWA generados dinamicamente desde configuracion global, con fondo de icono configurable y cache invalidada por logo, color y timestamp del blob.

### 3.11 Registro y onboarding

- Finalizacion guiada del perfil de cuenta mediante endpoint administrativo dedicado `/api/v1/accounts/:account_id/onboarding`.
- Persistencia del sitio web como URL completa para consumidores posteriores como Help Center y enriquecimiento de marca.
- Separacion entre actualizaciones generales de cuenta y el cierre del paso `account_details`.
- El callback OAuth de Instagram conserva la pista firmada `return_to` para volver al setup de la bandeja cuando la autorizacion parte del onboarding.

### 3.12 Seguridad y cumplimiento

- 2FA/MFA, SAML/SSO, roles personalizados y logs de auditoria.
- Proteccion de licencia en despliegues Mega.
- Observabilidad de release para trazabilidad por version.

## 4. Operacion y validacion

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
