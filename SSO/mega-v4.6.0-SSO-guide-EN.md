
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
*(Same YAML example as above translated to English.)*

---

## 🧾 Environment Variables (.env)
*(Same `.env` block translated to English comments.)*

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
