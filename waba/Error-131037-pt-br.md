# Erro da API do WhatsApp Business: (#131037) Aprovação do Nome de Exibição Necessária

![Erro 131037](./images/error-131037.png)

**Última atualização: 13 de janeiro de 2026**

Ao tentar enviar mensagens através da sua Conta Comercial do WhatsApp (WABA), você pode encontrar esta mensagem de erro:

> **(#131037) WhatsApp provided number needs display name approval before message can be sent**  
> **(#131037) O número fornecido do WhatsApp precisa de aprovação do nome de exibição antes que a mensagem possa ser enviada**

Este problema ocorre quando o **nome de exibição do seu número de telefone ainda não foi aprovado pela Meta** (Plataforma de Negócios do WhatsApp). Até que essa aprovação seja concluída, o número não pode ser usado para enviar ou receber mensagens através do seu BSP (Provedor de Soluções Empresariais como MEGA).

---

## 🔍 Por Que Este Erro Acontece

Cada número de telefone do WhatsApp Business deve ter um **nome de exibição aprovado** antes que possa ser ativado.

Quando você registra um novo número sob sua Conta Comercial do WhatsApp, a Meta revisa o nome de exibição para garantir que ele esteja em conformidade com as políticas de nomenclatura e negócios do WhatsApp.

Se seu nome de exibição ainda estiver **"Em Revisão"** ou foi **"Rejeitado"**, o sistema bloqueará qualquer mensagem de entrada ou saída, resultando neste erro.

---

## ✅ Como Corrigir o Erro

Siga estes passos para resolver o problema:

### 1. Vá para o seu Meta Business Manager

- Faça login em [https://business.facebook.com/](https://business.facebook.com/)
- Abra **Configurações da Empresa → Contas → Contas do WhatsApp**

### 2. Selecione sua conta WABA e verifique a aba de Números de Telefone

- Procure o número que mostra o erro
- Você verá o **Status do Nome de Exibição** (por exemplo, "Revisão Pendente", "Aprovado" ou "Rejeitado")

### 3. Se status = Revisão Pendente

- **Aguarde a conclusão da revisão da Meta**
- Este processo normalmente leva até **24–48 horas**

### 4. Se status = Rejeitado

- Clique em **Editar Nome de Exibição** e reenvie seguindo as diretrizes do WhatsApp
- Evite usar nomes genéricos ou enganosos. Ele deve representar claramente seu negócio ou marca
- Você pode consultar a política da Meta aqui: [Diretrizes de Nome de Exibição do WhatsApp](https://www.facebook.com/business/help/757569725593362)

### 5. Uma Vez Aprovado

- O erro desaparecerá automaticamente
- Você poderá enviar mensagens normalmente do seu BSP (como MEGA)

---

## 💡 Dica

Se você migrou recentemente seu número para um novo BSP, a revisão do nome de exibição pode reiniciar sob o novo Business Manager. Nesse caso, certifique-se de verificar novamente o status de aprovação antes de tentar enviar mensagens.

---

## 🧾 Resumo

| Código de Erro | Motivo | Solução |
|----------------|--------|---------|
| (#131037) O número do WhatsApp precisa de aprovação do nome de exibição | O nome de exibição está pendente ou foi rejeitado pela Meta | Verifique o status no Business Manager → Reenvie ou aguarde a aprovação |

---

## Tags

`#WhatsApp` `#Erro131037` `#NomeDeExibição` `#WABA` `#Meta` `#SoluçãoDeProblemas`

---

## Recursos Relacionados

- [Diretrizes de Nome de Exibição do WhatsApp](https://www.facebook.com/business/help/757569725593362)
- [Meta Business Manager](https://business.facebook.com/)
- [Documentação da API do WhatsApp Business](https://developers.facebook.com/docs/whatsapp)
- [Documentação do MEGA](https://github.com/megaapp977/stack)
