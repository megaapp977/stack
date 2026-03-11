# Configuración del Canal TikTok en MEGA

Configure la integración de TikTok Business Messaging para gestionar conversaciones de TikTok directamente desde MEGA.

La integración del canal TikTok permite gestionar conversaciones de TikTok Business Messaging directamente desde MEGA. Los agentes pueden recibir y responder mensajes de usuarios de TikTok, ver publicaciones compartidas y manejar archivos adjuntos de imágenes, todo desde el panel de MEGA.

La configuración del canal TikTok consta de **7 pasos principales**.

## Prerrequisitos

Antes de comenzar, asegúrate de tener:

1. **Instancia MEGA auto-hospedada** accesible mediante una URL pública con HTTPS
2. **Cuenta TikTok Business** registrada en una región elegible
3. **Configuración de mensajes directos**: Tu cuenta TikTok Business debe estar configurada para aceptar mensajes directos de todos. De lo contrario, necesitarás aceptar manualmente los mensajes en la app de TikTok. [Aprende cómo actualizar tus configuraciones de mensajes](https://ads.tiktok.com/help/article/how-to-update-your-tiktok-direct-message-permission-for-tiktok-messaging-ads?lang=en)
4. **Cuenta de desarrollador de TikTok** en [developers.tiktok.com](https://developers.tiktok.com/)
5. **Acceso al API Business Messaging de TikTok** - [solicitar permisos especiales](https://business-api.tiktok.com/portal/docs?id=1832183871604753) (requiere aprobación manual)
6. **Acceso de Super Admin** a tu instancia de MEGA

> **⚠️ Advertencia Importante**  
> El API Business Messaging de TikTok tiene restricciones regionales. **Actualmente NO está disponible** para cuentas registradas en el Espacio Económico Europeo (EEA), Suiza o Reino Unido. Solo se admiten cuentas TikTok Business, no cuentas personales.

## Paso 1 — Crear Cuenta de Desarrollador de TikTok

1. Accede a [developers.tiktok.com](https://developers.tiktok.com/) y regístrate
2. Verifica tu dirección de correo electrónico
3. Acepta los Términos de Servicio

## Paso 2 — Registrar Tu Aplicación

![Crear aplicación TikTok](images/tiktok-create-app.png)

1. Ve a [business-api.tiktok.com/portal/apps](https://business-api.tiktok.com/portal/apps) y crea una nueva aplicación
2. Completa los campos requeridos:
   - **App Name**: ej. "Tu Empresa - MEGA"
   - **App Description**: Descripción breve de tu caso de uso de mensajería
   - **App Icon**: Sube el logo de tu empresa
   - **Terms of Service URL**: URL de los términos de servicio de tu empresa
   - **Privacy Policy URL**: URL de la política de privacidad de tu empresa
3. Una vez creada, anota tu **App ID** (client key) y **App Secret** (client secret)

## Paso 3 — Solicitar Acceso al Business Messaging API

El acceso al **TikTok Business Messaging API** requiere aprobación manual por parte de TikTok. Para instrucciones detalladas, consulta la [guía oficial de acceso al Business Messaging API](https://business-api.tiktok.com/portal/docs?id=1832184145137922).

1. Abre tu aplicación en el Portal de Desarrolladores de TikTok
2. Navega al producto Business Messaging API
3. Envía una solicitud incluyendo:
   - Tu caso de uso (ej. soporte al cliente mediante MEGA)
   - Cómo manejarás los datos de usuario
   - Detalles de tu organización
4. Espera la revisión y aprobación de TikTok

> **📌 Nota:** La aprobación generalmente toma algunos días, pero puede tardar más para accesos especializados. No puedes continuar con la integración hasta que tu solicitud sea aprobada.

## Paso 4 — Configurar Permisos y URLs de la Aplicación

Una vez aprobado, configura lo siguiente en el Portal de Desarrolladores de TikTok:

### Permisos Requeridos

Después de que tu aplicación sea aprobada, asegúrate de que el permiso **TikTok Accounts** esté habilitado en **Scope of permission** en la configuración de tu aplicación.

![Permiso TikTok Accounts](images/tiktok-accounts-permission.png)

### URL de Redirección de Autorización

Establece la URL de redirección de autorización en:

```text
https://<FRONTEND_URL>/tiktok/callback
```

Reemplaza `<FRONTEND_URL>` con la URL de tu instalación de MEGA.

## Paso 5 — Configurar MEGA

### Configuración de Super Admin

1. Inicia sesión en tu instancia de MEGA como Super Admin
2. Navega a la configuración de la aplicación para TikTok
3. Ingresa tu **TikTok App ID** y **TikTok App Secret**
4. Haz clic en Enviar

**Alternativamente**, puedes establecer estas variables de entorno:

```bash
TIKTOK_APP_ID=tu_tiktok_app_id
TIKTOK_APP_SECRET=tu_tiktok_app_secret
TIKTOK_API_VERSION=v1.3
```

> **📌 Nota:** La versión de la API de TikTok por defecto es `v1.3`. Configura esto si quieres usar una versión diferente de la API de TikTok. Asegúrate de que esté prefijada con 'v'.

**Reinicia el servidor MEGA** después de realizar cambios.

### Habilitar la Funcionalidad de TikTok

1. En Super Admin, navega a Cuentas
2. Selecciona la cuenta donde deseas habilitar TikTok
3. En Funcionalidades, habilita el canal TikTok
4. Guarda los cambios

> **📌 Nota:** TikTok solo aparecerá en las opciones de canal del inbox una vez que hayas configurado el App ID y App Secret, y habilitado la funcionalidad para la cuenta.

## Paso 6 — Configurar Webhook

Configura el webhook de TikTok para recibir mensajes entrantes. Abre una consola de Rails en tu servidor MEGA:

```bash
bundle exec rails console
```

Ejecuta el siguiente comando para registrar la URL de callback del webhook:

```ruby
Tiktok::AuthClient.update_webhook_callback
```

Esto establece la URL del webhook en `https://<FRONTEND_URL>/webhooks/tiktok`.

Puedes verificar la configuración del webhook ejecutando:

```ruby
Tiktok::AuthClient.webhook_callback
```

> **⚠️ Advertencia:** El webhook debe configurarse después de establecer el TikTok App ID y App Secret en Super Admin. Si cambias tu dominio de MEGA, necesitarás ejecutar este comando nuevamente.

## Paso 7 — Conectar MEGA con Tu Cuenta TikTok

1. Inicia la conexión desde MEGA (Settings → Inboxes → Add Inbox → TikTok)
2. Serás redirigido a TikTok para autorizar
3. Acepta los permisos solicitados

Tras la autorización:

- MEGA valida el acceso
- Se crea o actualiza el canal TikTok
- Se habilita el inbox asociado
- Los mensajes entrantes se reflejarán automáticamente en MEGA

## Solución de Problemas

### Canal TikTok no aparece en las opciones de inbox

- Verifica que la funcionalidad TikTok esté habilitada para la cuenta en Super Admin
- Confirma que `TIKTOK_APP_ID` y `TIKTOK_APP_SECRET` estén configurados correctamente
- Reinicia el servidor MEGA después de los cambios de configuración

### Falla la autorización OAuth

- Asegúrate de que la URL de redirección en el Portal de Desarrolladores de TikTok coincida exactamente con `https://<FRONTEND_URL>/tiktok/callback`
- Verifica que tu aplicación de TikTok tenga todos los scopes requeridos habilitados
- Confirma que tu aplicación de TikTok esté aprobada para el Business Messaging API

### No se reciben mensajes entrantes

- Verifica que el webhook esté configurado ejecutando `Tiktok::AuthClient.webhook_callback` en la consola de Rails
- Asegúrate de que la URL del webhook sea públicamente accesible mediante HTTPS
- Confirma que tu cuenta TikTok Business esté en una región elegible
- Revisa los logs de Sidekiq para errores de `Webhooks::TiktokEventsJob`

### Fallan los mensajes al enviarse

- Verifica si la ventana de respuesta de 48 horas ha expirado
- Confirma que el token de acceso sea válido - MEGA renueva automáticamente los tokens, pero si el refresh token expira (30 días), el canal necesitará reautorización
- Asegúrate de estar enviando un tipo de mensaje soportado (solo texto, o una sola imagen)
- Revisa los logs de Sidekiq para errores de `SendReplyJob`

### El canal muestra "Reautorización Requerida"

Esto ocurre cuando tanto el token de acceso (alrededor de 24 horas) como el refresh token (alrededor de 30 días) han expirado, típicamente debido a inactividad.

1. Ve a Settings → Inboxes → selecciona el inbox de TikTok
2. Haz clic en Reautorizar
3. Completa el flujo OAuth de TikTok nuevamente

### Falla la verificación de firma del webhook

- Asegúrate de que `TIKTOK_APP_SECRET` coincida con el secret en tu Portal de Desarrolladores de TikTok
- Verifica la sincronización del reloj del servidor - la verificación de firma de TikTok requiere timestamps dentro de 5 segundos

## Limitaciones

- Solo cuentas TikTok Business (cuentas personales no compatibles)
- Solo mensajes iniciados por usuarios
- Ventana de respuesta de 48 horas
- Tipos de mensaje soportados: texto, imagen, publicación compartida
- No disponible en EEA, Suiza o Reino Unido
- Tokens de acceso expiran (~24 horas, renovación automática)
- Tokens de refresco expiran (~30 días, requiere reautorización manual)
