# Creación del canal TikTok en MEGA

## Paso 1 — Cuenta TikTok Business
Debes contar con una **TikTok Business Account**. Las cuentas personales no son compatibles.

## Paso 2 — Solicitar permisos especiales
El acceso a la **TikTok Business Messaging API** requiere aprobación manual por parte de TikTok.

1. Accede a la documentación oficial:
   https://business-api.tiktok.com/portal/docs?id=1832183871604753
2. Solicita acceso a *Business Messaging API*.
3. Completa el formulario indicando:
   - Caso de uso (soporte, atención al cliente, etc.).
   - Plataforma: MEGA.
4. Espera la aprobación de TikTok.

## Paso 3 — Crear aplicación en TikTok Developers
1. Crea una app en TikTok Developers.
2. Obtén:
   - App ID
   - App Secret
3. Configura:
   - Redirect URL: `https://<FRONTEND_URL>/tiktok/callback`
   - Webhook URL: `https://<FRONTEND_URL>/webhooks/tiktok`

## Paso 4 — Configurar MEGA
1. Define las variables de entorno:
   - `TIKTOK_APP_ID`
   - `TIKTOK_APP_SECRET`
2. Habilita la integración TikTok desde administración.

## Paso 5 — Autorizar la cuenta
1. Inicia la conexión desde MEGA.
2. Serás redirigido a TikTok para autorizar.
3. Acepta los permisos solicitados.

## Paso 6 — Creación automática del canal
Tras la autorización:
- MEGA valida el acceso.
- Se crea o actualiza el canal TikTok.
- Se habilita el inbox asociado.

## Paso 7 — Recepción de mensajes
TikTok enviará eventos al webhook configurado.
Los mensajes entrantes se reflejarán automáticamente en MEGA.

## Limitaciones
- Solo cuentas Business.
- Solo mensajes iniciados por usuarios.
- Tipos soportados: texto, imagen, post compartido.
- Restricciones regionales según TikTok.
