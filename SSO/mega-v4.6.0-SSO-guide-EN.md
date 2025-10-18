
# 🇬🇧 Mega v4.6.0 SSO Guide — Step-by-Step Implementation
**Last update:** 2025-10-18

## 🔍 What is SSO?
**SSO (Single Sign-On)** allows users to authenticate once with a corporate identity system (Google, Microsoft, Okta, Keycloak, etc.) and access Mega without re-entering credentials.

### 🎯 Benefits
- Centralized and secure login.  
- MFA enforcement via IdP policies.  
- Less password fatigue.  
- Simplified IT management.

---

## 🧩 Core Components
- **IdP (Identity Provider):** authentication provider (Google, Microsoft, Okta, etc.).  
- **SP (Service Provider):** Mega, which validates identity via IdP.  
- **Supported Protocols:**
  - OAuth 2.0 / OpenID Connect → Google, Microsoft.  
  - SAML 2.0 → Okta, Entra ID, Keycloak.  
  - SSO Link (Platform API) → automatic login.

---

## 🚀 How to implement SSO in Mega
1. **Choose integration type:** OAuth, SAML, or Platform API.  
2. **Configure IdP:** register Mega as an app and set redirect URLs.  
3. **Configure Mega:** edit `.env` with credentials.  
4. **Test authentication in staging.**  
5. **Enable MFA and check roles.**

---

## ⚙️ Deployment Example (Docker Swarm + Traefik + PostgreSQL)
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

## 🧾 Environment variables (.env)
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

---

## 🧪 Testing
- Check HTTPS certificate.  
- Validate redirect URLs.  
- Sync server time.  
- Test MFA and logout flow.  

---

## ✅ Checklist
- [ ] `.env` configured  
- [ ] SSL enabled  
- [ ] OAuth/SAML working  
- [ ] MFA enforced  
- [ ] Logs verified  
