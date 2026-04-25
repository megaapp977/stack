# MEGA - Detalle Tecnico de Funcionalidades (ES)

Version: Enterprise
Ultima actualizacion: 25 de abril de 2026
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
- WhatsApp Evolution, WAHA y Uazapi: proveedores alternativos con soporte multimedia y grupos.
- Notificame: variante oficial orientada a operaciones LATAM.
- Instagram, Facebook, TikTok, Telegram, X, SMS y Email integrados como inboxes.
- API Channel: canal generico para integrar sistemas propietarios via API/webhooks.
- Voz Twilio y llamadas WhatsApp Cloud: flujo WebRTC con historial unificado en conversacion.

### 3.2 Nucleo de conversaciones

- Estados: open, pending, resolved, snoozed.
- Prioridad: urgencia operativa por conversacion.
- Participantes: colaboracion multiagente en una misma conversacion.
- Borradores y pinned: continuidad de trabajo por agente.
- Filtros avanzados y vistas personalizadas: segmentacion operativa de alto volumen.
- Assignment V2: distribucion inteligente con capacidad y reglas.

### 3.3 Automatizacion y bots

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
- Firmas de webhook por canal para validar autenticidad de eventos salientes.

### 3.4 IA Captain

- Proveedores soportados: OpenAI, Anthropic, Google, Azure OpenAI, Bedrock, DeepSeek.
- Assistants: configuracion por inbox con instrucciones y contexto.
- Captain Documents: carga, indexacion y campos de auto-sincronizacion.
- Captain Scenarios: reglas de activacion y prioridad.
- Captain Custom Tools: integraciones HTTP con GET, POST, PUT, PATCH y DELETE.
- MCP Servers: extension de capacidades via Model Context Protocol.
- Auto-resolve mode: evaluated, legacy o disabled por cuenta.

### 3.5 CRM y gestion de contactos

- Atributos personalizados por tipo y uso en automatizaciones.
- Control de visibilidad de atributos por rol en Enterprise.
- Etiquetas para contactos y conversaciones.
- Empresas con agrupacion por dominio y vista unificada.
- Bloqueo activo en WhatsApp para descartar mensajes entrantes de contactos bloqueados.

### 3.6 Campanas

- Ongoing campaigns para widget/live chat.
- One-off campaigns para WhatsApp, SMS y API Channel.
- Constructor de templates Meta con ciclo de aprobacion y sincronizacion.
- Control de velocidad, rotacion multi-inbox y metricas de ejecucion.

### 3.7 Help Center

- Articulos multi-idioma con estado por idioma.
- Editor con menu slash y tablas nativas.
- Insercion de articulos en conversacion con busqueda y popover estable.
- Embedding search en Enterprise para busqueda semantica.

### 3.8 Kanban comercial (Mega)

- Embudos con etapas configurables y etapa predeterminada.
- Vista board y list para distintos flujos de trabajo.
- Filtros por inbox, canal, etapa y actividad.
- Item 360: checklist, notas, adjuntos, ofertas, agentes y atributos.
- Relacion nativa con contacto y conversacion.
- Automatizaciones por etapa y mensajes rapidos.
- Sincronizacion en tiempo real con lista de chats y panel de contacto.

### 3.9 Integraciones y extensibilidad

- Webhooks con payload enriquecido y secreto global HMAC-SHA256.
- Dashboard Apps para iFrames embebidos por contexto.
- Dashboard Scripts (Super Admin) para personalizacion global sin tocar core.
- Platform Apps para extensiones de alto nivel via API.
- Integraciones de negocio: Slack, Linear, Shopify, WooCommerce, Notion y CRM.

### 3.10 Seguridad y cumplimiento

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
