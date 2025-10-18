
# 🇪🇸 Guía completa de SSO en Mega v4.6.0 — Implementación paso a paso
**Última actualización:** 2025-10-18

## 🔍 ¿Qué es SSO?
**SSO (Single Sign-On)** significa **Inicio de Sesión Único**.  
Permite que los usuarios se autentiquen una sola vez en un sistema de identidad corporativo (Google, Microsoft, Okta, Keycloak, etc.) y accedan a Mega sin ingresar credenciales nuevamente.

### 🎯 Beneficios
- Inicio de sesión rápido y centralizado.  
- Mayor seguridad con políticas del IdP.  
- Reducción de contraseñas múltiples.  
- Menor carga de administración para TI.

---

## 🧩 Componentes principales
- **IdP (Identity Provider):** sistema de autenticación (Google, Microsoft, Okta, etc.).  
- **SP (Service Provider):** Mega, que valida la identidad mediante el IdP.  
- **Protocolos compatibles:**
  - OAuth 2.0 / OpenID Connect → Google y Microsoft.  
  - SAML 2.0 → Okta, Entra ID, Keycloak.  
  - Enlace SSO (Platform API) → inicio de sesión automático.

---

## 🚀 Cómo implementar SSO en Mega
1. **Seleccionar el tipo de integración:** OAuth, SAML o Platform API.  
2. **Configurar el IdP:** registrar Mega como aplicación y definir URLs de redirección.  
3. **Configurar Mega:** editar `.env` con credenciales.  
4. **Probar la autenticación en entorno de staging.**  
5. **Habilitar MFA y revisar roles de usuario.**

---

## ⚙️ Ejemplo de despliegue (Docker Swarm + Traefik + PostgreSQL)
```yaml
version: "3.9"
services:
  mega_app:
    image: megaapp/mega:4.6.0
    environment:
      - FORCE_SSL=true
      - FRONTEND_URL=https://app.mega.com
      - DATABASE_URL=postgresql://mega_user:mega_pass@postgres:5432/mega_db
      - REDIS_URL=redis://redis:6379
      - GOOGLE_OAUTH_CLIENT_ID=example-id
      - GOOGLE_OAUTH_CLIENT_SECRET=example-secret
      - AZURE_APP_ID=example-azure-id
      - AZURE_APP_SECRET=example-azure-secret
      - SAML_ENABLED=false
    networks:
      - mega_net
    deploy:
      labels:
        - traefik.enable=true
        - traefik.http.routers.mega.rule=Host(`app.mega.com`)
        - traefik.http.services.mega.loadbalancer.server.port=3000
  redis:
    image: redis:7
  postgres:
    image: postgres:16
    environment:
      - POSTGRES_USER=mega_user
      - POSTGRES_PASSWORD=mega_pass
      - POSTGRES_DB=mega_db

networks:
  mega_net:
    external: true
```

---

## 🧾 Variables de entorno (.env)
```dotenv
FRONTEND_URL=https://app.mega.com
FORCE_SSL=true
GOOGLE_OAUTH_CLIENT_ID=
GOOGLE_OAUTH_CLIENT_SECRET=
GOOGLE_OAUTH_CALLBACK_URL=https://app.mega.com/auth/google_oauth2/callback
AZURE_APP_ID=
AZURE_APP_SECRET=
SAML_ENABLED=false
SAML_IDP_SSO_TARGET_URL=
SAML_IDP_CERT=
SAML_IDP_ENTITY_ID=
SAML_ATTRIBUTE_STATEMENTS_EMAIL=email
PLATFORM_APP_API_ACCESS_TOKEN=
```

---

## 🧪 Pruebas
- Verificar acceso HTTPS.  
- Confirmar redirección correcta.  
- Revisar sincronización horaria.  
- Probar cierre de sesión y MFA.  

---

## ✅ Checklist
- [ ] `.env` configurado  
- [ ] SSL activo  
- [ ] OAuth/SAML funcional  
- [ ] MFA habilitado  
- [ ] Logs revisados  
