
# 🇧🇷 Guia de SSO no Mega v4.6.0 — Implementação passo a passo
**Última atualização:** 2025-10-18

## 🔍 O que é SSO?
**SSO (Single Sign-On)** permite que os usuários se autentiquem uma única vez em um sistema de identidade corporativo (Google, Microsoft, Okta, Keycloak, etc.) e acessem o Mega sem precisar digitar credenciais novamente.

### 🎯 Benefícios
- Login rápido e centralizado.  
- Segurança reforçada com MFA.  
- Menos senhas para gerenciar.  
- Administração de TI simplificada.

---

## 🧩 Componentes principais
- **IdP (Provedor de Identidade):** autentica o usuário (Google, Microsoft, Okta).  
- **SP (Provedor de Serviço):** Mega, que valida a identidade.  
- **Protocolos compatíveis:**
  - OAuth 2.0 / OpenID Connect → Google, Microsoft.  
  - SAML 2.0 → Okta, Entra ID, Keycloak.  
  - Link de SSO (Platform API) → login automático.

---

## 🚀 Como implementar SSO no Mega
1. **Escolha o tipo de integração:** OAuth, SAML ou Platform API.  
2. **Configure o IdP:** registre o Mega como aplicativo e defina URLs de redirecionamento.  
3. **Configure o Mega:** edite o `.env` com credenciais.  
4. **Teste a autenticação em ambiente de staging.**  
5. **Ative MFA e revise papéis de usuário.**

---

## ⚙️ Exemplo de implantação (Docker Swarm + Traefik + PostgreSQL)
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

## 🧾 Variáveis de ambiente (.env)
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

## 🧪 Testes
- Verifique HTTPS.  
- Valide URLs de redirecionamento.  
- Sincronize o horário do servidor.  
- Teste o logout e MFA.  

---

## ✅ Checklist
- [ ] `.env` configurado  
- [ ] SSL ativo  
- [ ] OAuth/SAML funcional  
- [ ] MFA habilitado  
- [ ] Logs verificados  
