# MEGA autohospedado: integración con Google

Documentación consolidada de las opciones de Google en MEGA: Gmail/Google Workspace, inicio de sesión OAuth, despliegue en Google Cloud Platform (GCP) y almacenamiento en Google Cloud Storage (GCS).

## Google Workspace y Gmail mediante OAuth

Las aplicaciones menos seguras de Google Workspace dejaron de ser una opción para esta integración. Para que MEGA lea y gestione correo de Gmail o Google Workspace, cree una aplicación OAuth en Google Cloud.

1. En la [consola de Google API](https://console.developers.google.com/), cree o seleccione el proyecto y registre la aplicación OAuth.
2. Al registrar la aplicación para el canal de correo, agregue la URL de redirección `https://<url-de-tu-instancia>/google/callback`.
3. Copie el ID y el secreto de cliente a la configuración de MEGA:

```bash
GOOGLE_OAUTH_CLIENT_ID=369777777777-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.apps.googleusercontent.com
GOOGLE_OAUTH_CLIENT_SECRET=ABCDEF-GHijklmnoPqrstuvwX-yz1234567
```

![Registro de la aplicación OAuth](images/oauth-app-setup.png)

Si ya existe una aplicación para el inicio de sesión OAuth de Google, puede reutilizarla añadiendo esta URL de redirección; no elimine la URL anterior. Reinicie MEGA después de cambiar las variables.

### Permisos OAuth requeridos

En **OAuth consent screen** > **Edit App**, agregue y guarde los siguientes scopes:

- `https://mail.google.com/`: leer, enviar, eliminar y administrar correo.
- `email`: ver la dirección de correo del usuario.
- `profile`: ver el nombre, la imagen y otros datos básicos del perfil.

![Demostración para agregar el scope de correo](images/add-scope-demo.gif)

Para organizaciones de menos de 100 usuarios, la aplicación puede permanecer en modo de pruebas. Para más de 100 usuarios o para atender a varios clientes, publíquela. Como usa un permiso restringido, Google exige completar el [proceso de verificación](https://support.google.com/cloud/answer/9110914), que puede tardar varios días.

## Inicio de sesión con Google

El OAuth de inicio de sesión usa una URL de retorno distinta a la del canal Gmail. Configure las tres variables y reinicie MEGA:

```bash
GOOGLE_OAUTH_CLIENT_ID=369777777777-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.apps.googleusercontent.com
GOOGLE_OAUTH_CLIENT_SECRET=ABCDEF-GHijklmnoPqrstuvwX-yz1234567
GOOGLE_OAUTH_CALLBACK_URL=https://<dominio-de-tu-servidor>/omniauth/google_oauth2/callback
```

La ruta `/omniauth/google_oauth2/callback` es fija en MEGA y debe coincidir exactamente con la URL autorizada en Google API Console.

## Google Calendar en MEGA

MEGA utiliza las mismas credenciales OAuth globales para Google Calendar y, opcionalmente, para el inicio de sesión con Google. La credencial se configura una vez por instalación; después, cada cuenta conecta su propio calendario desde **Settings > Integrations > Google Calendar**.

### Configuración en Google Cloud

1. En **APIs & Services > Library**, active **Google Calendar API**.
2. En **OAuth consent screen**, complete los datos de la aplicación. Use **Internal** solo para usuarios del mismo Google Workspace; use **External** para cuentas Gmail o Workspace de clientes. Si queda en pruebas, agregue los usuarios de prueba.
3. Agregue los scopes que solicita MEGA:

```text
openid
email
profile
https://www.googleapis.com/auth/calendar
```

4. En **APIs & Services > Credentials**, cree un cliente OAuth de tipo **Web application**.
5. En *Authorized JavaScript origins*, agregue únicamente el origen HTTPS, sin ruta ni `/` final: `https://<tu-dominio>`.
6. En *Authorized redirect URIs*, agregue obligatoriamente el callback de Calendar:

```text
https://<tu-dominio>/google_calendar/callback
```

Si también activa el login con Google, agregue además:

```text
https://<tu-dominio>/omniauth/google_oauth2/callback
```

> La URL de Calendar y la de login son distintas. En MEGA, Calendar se construye con `FRONTEND_URL` más `/google_calendar/callback`; por eso el dominio público configurado en `FRONTEND_URL` debe coincidir exactamente con el origen y callback autorizados.

### Cargar credenciales desde Super Admin

Como super admin, abra:

```text
https://<tu-dominio>/super_admin/app_config?config=google
```

![Configuración de Google desde Super Admin](images/super-admin-google-settings.png)

Complete y guarde los campos mostrados en **Configure Settings - Google**:

| Campo | Valor |
|---|---|
| Google OAuth Client ID | Client ID de Google Cloud |
| Google OAuth Client Secret | Client Secret de Google Cloud |
| Google OAuth Redirect URI | `https://<tu-dominio>/google_calendar/callback` |
| Enable Google OAuth login | `False` si solo se usará Calendar; `True` si también se permitirá iniciar sesión con Google |

No es necesario guardar el Client ID ni el secreto en variables de entorno cuando se cargan desde Super Admin. Mantenga `FRONTEND_URL=https://<tu-dominio>` en el servidor. Las variables de entorno siguen siendo un fallback válido para despliegues antiguos.

### Conectar un calendario por cuenta

1. En la cuenta correspondiente, abra **Settings > Integrations > Google Calendar**.
2. Pulse **Connect**, elija la cuenta Google y acepte los permisos.
3. Tras volver a MEGA, seleccione o confirme el calendario de destino y guarde la configuración.
4. Active la sincronización, elija su dirección (**MEGA → Google**, **Google → MEGA** o **Bidirectional**) y los módulos necesarios: Calendar, Kanban, Conversations y Reminders.

La tarjeta de Google Calendar solo está disponible cuando la funcionalidad de la cuenta está habilitada y existen Client ID y Client Secret globales. La conexión y los tokens se guardan por cuenta, no como un calendario compartido de toda la instalación.

## Desplegar MEGA en GCP

Esta guía instala MEGA en una única VM de Compute Engine. Para un despliegue cloud-native, use charts de Helm con Google Kubernetes Engine (GKE).

1. En GCP, abra **VM > Compute Engine** y cree una instancia.
2. Seleccione la región adecuada, al menos 4 vCPU y 8 GB de RAM (N2 de propósito general).
3. Use Ubuntu 20.04 y un disco de 120 GB.
4. Conéctese por SSH y siga la instalación de MEGA en Linux VM.
5. Acceda a `http://<ip-de-la-instancia>:3000` o, tras configurar el dominio, a `https://<tu-dominio>`.

![Creación de una VM de Compute Engine](images/gcp-compute-engine.png)

Luego configure dominio, correo y el resto de variables del entorno de la instalación Linux VM.

## Almacenamiento de adjuntos en Google Cloud Storage

Active GCS como servicio de almacenamiento:

```bash
ACTIVE_STORAGE_SERVICE='google'
```

### Proyecto y bucket

1. En Google Cloud Console, copie el ID del proyecto y asígnelo:

```bash
GCS_PROJECT=tu-id-de-proyecto
```

![Ubicación del ID de proyecto](images/get-project-id.png)

2. Abra **Storage > Browser**, cree un bucket con **Create bucket** y conserve los valores predeterminados si son adecuados para su entorno.

![Creación de un bucket](images/create-bucket.png)

3. Configure su nombre:

```bash
GCS_BUCKET=nombre-de-tu-bucket
```

### Cuenta de servicio y credenciales

1. Vaya a **Identity & Services > Identity > Service Accounts**, cree una cuenta de servicio y asígnele **Cloud Storage > Storage Admin**.

![Rol Storage Admin](images/storage-admin.png)

2. En **Storage > Browser > tu bucket > Permissions**, agregue esa cuenta como miembro con el rol **Cloud Storage > Storage Admin**.

![Permisos del bucket](images/bucket-permissions.png)

3. En la cuenta de servicio, abra **Keys > Add Key** y elija JSON.

![Creación de clave JSON](images/service-account-json-key.png)

Copie el contenido JSON en una sola línea. En MEGA 2.17 o superior, encierre el valor entre comillas simples:

```bash
GCS_CREDENTIALS='{"type":"service_account","project_id":"","private_key_id":"","private_key":"","client_email":"","client_id":"","auth_uri":"","token_uri":"","auth_provider_x509_cert_url":"","client_x509_cert_url":""}'
```

### Carga directa

De forma predeterminada, los archivos pasan primero por el servidor de MEGA. Para subirlos directamente a GCS, active:

```bash
DIRECT_UPLOADS_ENABLED=true
```

Después configure [CORS en el bucket](https://edgeguides.rubyonrails.org/active_storage_overview.html#cross-origin-resource-sharing-cors-configuration) para permitir las cargas directas.
