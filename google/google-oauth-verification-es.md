# Verificación de OAuth consent screen para MEGA

Guía de preparación y envío de MEGA a la verificación de Google para usar Google Calendar con cuentas externas en producción.

## Alcance de esta verificación

MEGA solicita los siguientes scopes para conectar Google Calendar:

```text
openid
email
profile
https://www.googleapis.com/auth/calendar
```

El acceso completo a Calendar es un scope **sensible**. Una aplicación externa publicada necesita verificación de marca y de acceso a datos antes de que usuarios generales puedan autorizarla. No confundirlo con un scope restringido: la evaluación de seguridad anual aplica si se añaden scopes restringidos o se accede a esos datos desde un servidor de terceros.

La verificación no suele ser necesaria si el proyecto está solo en desarrollo/pruebas, para uso personal limitado, o si es una aplicación **Internal** usada exclusivamente por la misma organización de Google Workspace. Para cuentas Gmail o Workspace de clientes, configure **External** y prepare la verificación.

### APIs necesarias y relación con OAuth

En **APIs & Services > Library**, habilite **Google Calendar API**: es la API necesaria para esta verificación y para la sincronización de Calendar. La verificación de OAuth no se completa habilitando una API; también hay que declarar los scopes en **Data Access** y demostrar su uso.

Si la misma instalación usa otras funciones de Google, habilite **Cloud Storage API** para GCS. No habilite **Gmail API** solo porque MEGA usa Gmail por OAuth: la implementación actual usa IMAP/SMTP con XOAUTH2 y el scope `https://mail.google.com/`, no endpoints REST de Gmail. Gmail API sería necesaria únicamente si MEGA incorporase llamadas REST de Gmail.

## Antes de empezar

Use un proyecto de Google Cloud exclusivo de producción. Mantenga otro proyecto y cliente OAuth para desarrollo o staging. Reúna estos datos antes de editar la consola:

- Dominio público propio con HTTPS: `https://<tu-dominio>`.
- Página pública de inicio que identifique MEGA, explique la integración con Google Calendar y no sea únicamente una pantalla de login.
- Política de privacidad pública en el mismo dominio, enlazada también desde la página de inicio.
- Términos de servicio públicos en el mismo dominio.
- Correo de soporte y contactos de desarrollador que se supervisen activamente.
- Logo cuadrado de MEGA, que represente la aplicación, en PNG/JPG/BMP y de máximo 1 MB; se recomienda 120 × 120 px.
- Una cuenta Google que sea Owner o Editor del proyecto y propietaria verificada del dominio en Google Search Console.
- Video de demostración no listado y credenciales de prueba si el revisor las necesita.

La política de privacidad debe explicar de forma clara que MEGA solicita permisos de Calendar para que el usuario conecte su cuenta, consulta/crea/actualiza eventos según la configuración de sincronización, guarda tokens cifrados por cuenta para mantener la conexión y cómo el usuario puede desconectarla. Debe describir cualquier almacenamiento, uso o compartición de datos de Google, y coincidir con el comportamiento real del producto.

## 1. Verificar el dominio

1. En [Google Search Console](https://search.google.com/search-console), agregue y verifique la propiedad del dominio raíz, por ejemplo `chat2one.com`.
2. Use la misma cuenta como Owner o Editor del proyecto de Google Cloud.
3. En Google Cloud Console abra **Google Auth Platform > Branding**. En **Authorized domains**, agregue el dominio raíz antes de registrar sus URLs.
4. Revise que todos los dominios usados por la página principal, la política, los términos, los *Authorized JavaScript origins* y los *Authorized redirect URIs* pertenezcan a dominios autorizados y verificados.

No use dominios de terceros ni una URL con un dominio distinto para la política de privacidad.

## 2. Preparar Branding

En la consola actual, vaya a **APIs & Services > OAuth consent screen**; este acceso abre **Google Auth Platform**. En **Branding**, complete:

| Campo | Preparación para MEGA |
|---|---|
| App name | `MEGA` (debe coincidir con la web, el video y la aplicación) |
| User support email | Buzón real y supervisado para soporte de autorización |
| App logo | Logo propio de MEGA; no use marcas ni logotipos de Google |
| Application home page | URL pública de la página de inicio de MEGA |
| Application privacy policy link | URL pública de la política de privacidad de MEGA |
| Application terms of service link | URL pública de los términos de MEGA |
| Developer contact information | Uno o más correos que respondan a Google |

Para una aplicación **External** en producción, la página de inicio, política y términos son obligatorios. La página de inicio debe enlazar la misma política que figura en Branding. No modifique nombre, logo ni URLs mientras haya una revisión activa.

## 3. Configurar Audience, cliente y acceso a datos

1. En **Audience**, seleccione **External** para usuarios de clientes. Mantenga el estado Testing mientras valida el flujo con usuarios de prueba; antes del envío para producción, cambie a **In production** según lo requiera la consola.

![Audience: aplicación externa en pruebas y usuarios de prueba](images/google-auth-platform-audience.png)

2. En **Clients**, cree o revise el cliente OAuth de tipo **Web application**. Agregue:

   ```text
   Authorized JavaScript origin: https://<tu-dominio>
   Authorized redirect URI: https://<tu-dominio>/google_calendar/callback
   ```

   Si MEGA habilita inicio de sesión con Google, agregue además `https://<tu-dominio>/omniauth/google_oauth2/callback`.

3. En **Data Access**, declare únicamente los scopes que MEGA solicita: `openid`, `email`, `profile` y `https://www.googleapis.com/auth/calendar`.
4. Habilite **Google Calendar API** en **APIs & Services > Library**.
5. Verifique desde MEGA que el calendario se conecta, permite elegir calendario, sincroniza solo las funciones habilitadas y se puede desconectar.

No agregue scopes «por si acaso». Si una función solo lee eventos, evalúe primero un scope más limitado; el alcance completo de Calendar solo debe mantenerse si las acciones de lectura, creación, actualización o eliminación de MEGA lo requieren.

## 4. Preparar el envío

Antes de pulsar **Submit for verification**, prepare una respuesta breve y específica para cada scope:

| Scope | Justificación de MEGA |
|---|---|
| `openid`, `email`, `profile` | Identifican la cuenta Google que el administrador autoriza y muestran su identidad conectada en la integración. |
| `https://www.googleapis.com/auth/calendar` | Permite al administrador conectar un calendario, seleccionar el destino y sincronizar eventos de MEGA en la dirección que haya configurado. |

Incluya hasta tres enlaces de documentación funcional de MEGA si la consola los solicita. Describa solo funciones ya disponibles para el usuario y no prometa funcionalidades futuras.

### Video de demostración requerido

Suba a YouTube un video **Unlisted/No listado**. No use secretos, datos de clientes ni calendarios reales. El video debe estar en inglés y mostrar, de principio a fin:

1. La página pública de MEGA, con el mismo nombre, logo y dominio enviados a revisión.
2. Inicio de sesión como administrador de una cuenta de prueba.
3. **Settings > Integrations > Google Calendar** y el botón **Connect**.
4. El consentimiento de OAuth completo en inglés, incluida la barra de direcciones con el Client ID y los scopes solicitados.
5. La selección de la cuenta y el calendario de prueba.
6. La configuración de dirección/módulos de sincronización.
7. Una función real que use Calendar: crear o actualizar un evento desde MEGA y mostrar su resultado en el calendario autorizado; si se solicita importación, demostrar también la lectura de eventos.
8. La desconexión o el lugar donde el usuario puede retirar la conexión.

No oculte la pantalla de consentimiento ni sustituya el flujo por capturas; Google debe poder verificar que los scopes mostrados coinciden con los declarados.

## 5. Enviar y publicar

1. En **Branding**, complete la verificación de marca si aparece **Verify Branding**. Cuando termine en **Ready to publish**, pulse **Publish branding** dentro de los siete días.
2. Abra **Verification Center**. Solo tras tener la marca publicada podrá solicitar la verificación de **Data access**.
3. Revise los scopes, pegue el enlace no listado del video, las justificaciones y la documentación solicitada.
4. Confirme el cumplimiento de las políticas y pulse **Submit**.
5. Supervise los correos de soporte, de contacto del desarrollador y el estado en Verification Center. Responda a las solicitudes de Google con precisión y sin cambiar la configuración mientras está en revisión.

Como referencia de planificación, Google indica normalmente 2–3 días hábiles para marca y hasta 10 días hábiles para scopes sensibles; no son plazos garantizados. Un rechazo de scopes sensibles puede impedir nuevas autorizaciones de esos scopes hasta que se corrija y reenvíe la solicitud.

## Checklist final

- [ ] Proyecto de producción separado del proyecto de pruebas.
- [ ] Google Calendar API habilitada.
- [ ] Tipo de audiencia External y estado de publicación correcto.
- [ ] Dominio propio verificado en Search Console por un Owner/Editor del proyecto.
- [ ] Todos los dominios, orígenes y callbacks autorizados coinciden exactamente.
- [ ] Página de inicio, política y términos públicos, coherentes y bajo el dominio propio.
- [ ] Branding de MEGA coherente en consola, web, producto y video.
- [ ] Solo scopes mínimos declarados; Calendar justificado por funciones visibles.
- [ ] Video no listado, en inglés, con consentimiento OAuth completo y flujo real.
- [ ] Sin secretos, tokens ni información de clientes en video o documentación.
- [ ] Contactos de soporte y desarrollador activos para responder a Google.

## Referencias de Google

- [Verification requirements](https://support.google.com/cloud/answer/13464321)
- [Sensitive scope verification](https://developers.google.com/identity/protocols/oauth2/production-readiness/sensitive-scope-verification)
- [Manage OAuth App Branding](https://support.google.com/cloud/answer/15549049)
- [OAuth verification FAQ](https://support.google.com/cloud/answer/13463817)
