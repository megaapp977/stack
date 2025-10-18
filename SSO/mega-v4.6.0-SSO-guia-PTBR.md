
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
*(Mesmo exemplo YAML traduzido.)*

---

## 🧾 Variáveis de ambiente (.env)
*(Mesmo bloco de variáveis traduzido.)*

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
