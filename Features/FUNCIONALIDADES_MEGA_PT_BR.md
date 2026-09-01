# 🚀 MEGA - Plataforma de Comunicação Omnichannel

## Seu Centro de Comando para o Atendimento ao Cliente do Futuro

As gravações de chamadas do Twilio Voice podem ser transcritas opcionalmente, exibidas com a gravação e encontradas na busca de conversas.

**Versão:** Enterprise
**Baseado em:** Plataforma MEGA e Funcionalidades Exclusivas da MEGA
**Última Atualização:** 1 de setembro de 2026

---

### APIs verificadas e prontas para Postman

Swagger/OpenAPI 3.1 mantém paridade automática com as rotas suportadas e gera uma coleção Postman separada por token da conta, token do aplicativo da plataforma e rotas públicas.

## 📋 Índice

1. [Canais de Comunicação](#-canais-de-comunicação)
2. [Gestão de Conversas](#-gestão-de-conversas)
3. [Comunicação Interna da Equipe](#-comunicação-interna-da-equipe)
4. [Automação e IA](#-automação-e-ia)
5. [CRM e Gestão de Contatos](#-crm-e-gestão-de-contatos)
6. [Campanhas em Massa](#-campanhas-em-massa)
7. [Central de Ajuda (Help Center)](#-central-de-ajuda-help-center)
8. [Relatórios e Analytics](#-relatórios-e-analytics)
9. [Gestão de Equipes](#-gestão-de-equipes)
10. [Integrações](#-integrações)
11. [Funcionalidades Enterprise](#-funcionalidades-enterprise)
12. [Funcionalidades Exclusivas Mega](#-funcionalidades-exclusivas-mega)

---

## 📱 Canais de Comunicação

- **Identificação clara das caixas de entrada** *(Mega)* - As listas e a barra lateral mostram o nome de cada caixa junto com seu identificador público (telefone, email ou URL). Os IDs de página do Facebook e de perfil do X continuam disponíveis para operações do provedor, mas não são exibidos. A busca também aceita os identificadores visíveis.

### WhatsApp Business

Conecte-se com seus clientes através do canal de mensagens mais popular do mundo.

- **WhatsApp Cloud API** - Integração oficial do Meta com todas as funcionalidades empresariais
- **Configuração manual guiada do WhatsApp** *(Mega)* - Administradores podem preparar seu próprio aplicativo Meta, validar um número de produção, o ID da WABA e um token permanente antes de criar uma caixa Cloud; o fluxo mostra o status do webhook/assinatura e permite tentar novamente o webhook sem sair da configuração
- **Cadastro integrado para coexistência com WhatsApp Business App** *(Mega)* - O cadastro integrado permite ativar um número do WhatsApp Business App, incluindo conclusões de coexistência sem ID de número de telefone, enquanto a MEGA configura a conexão e os webhooks necessários
- **Mega Hub para WhatsApp** *(Mega)* - Conexão opcional com apps compartilhados pelo Super Admin, usando credenciais dedicadas do Hub, webhooks reenviados, saúde baseada no forward e sem configuração manual de callback/token
- **WhatsApp Evolution** *(Mega)* - Conexão direta sem API oficial, ideal para contas pessoais
- **WhatsApp WAHA** *(Mega)* - Provedor alternativo com suporte completo a mensagens multimídia
- **WhatsApp Uazapi** *(Mega)* - Solução de baixo custo para múltiplas linhas
- **Alertas de saúde da conexão** *(Mega)* - Problemas de token e sessão aparecem nas listas de caixas, na barra lateral principal e nas configurações da caixa com atalho para configuração da sessão
- **Resiliência da saúde do número** *(Mega)* - A saúde do número da Cloud API continua disponível quando os dados da conta comercial vinculada não podem ser atualizados
- **Perfil comercial do WhatsApp na Saúde da conta** *(Mega)* - A Saúde da conta mostra o perfil comercial somente leitura visto pelos clientes, orientação clara sobre a revisão do nome e o limite de mensagens compartilhado pelo portfólio
- **Reconexão manual do WhatsApp** *(Mega)* - Caixas elegíveis do cadastro integrado podem ser reconectadas ao seu próprio aplicativo Meta por um fluxo guiado que preserva a caixa e o histórico de atendimento
- **Reconfiguração do cadastro integrado** *(Mega)* - Administradores podem atualizar as credenciais e a configuração do WhatsApp Business de uma caixa Cloud conectada pelo cadastro integrado quando o fluxo unificado de cadastro integrado está habilitado para a conta
- **Arquitetura multi-servidor** *(Mega)* - Configure vários servidores por provedor com resolução automática de credenciais
- **Capacidade por servidor** *(Mega)* - Defina limites por servidor para distribuir a carga operacional
- **Suporte BSUID** *(Mega)* - Identificação robusta do contato e envio confiável mesmo sem `wa_id` tradicional
- **Mensagens não suportadas por provedor** *(Mega)* - Distingue conteúdo incompatível de mensagens indisponíveis por coexistência; somente estas últimas orientam a verificar o WhatsApp Business
- **Mensagens de template** - Envie mensagens fora da janela de 24 horas com templates aprovados; as automações bloqueiam localmente o envio de texto livre nesse estado e orientam o uso de um template
- **Sincronização de contatos** - Mantenha sua base de dados atualizada automaticamente
- **Suporte a grupos** - Gerencie conversas de grupos do WhatsApp diretamente

**Rastreamento de Anúncios WhatsApp (Click-to-WhatsApp):**

Meça o ROI dos seus anúncios do Facebook/Instagram que direcionam para WhatsApp:

- **Origem do lead** - Detecta automaticamente se a mensagem vem de um anúncio
- **Dados da campanha** - Salva qual anúncio gerou cada conversa
- **Atribuição automática** - Conecta vendas com campanhas específicas
- **Métricas claras** - Saiba exatamente quantos leads cada anúncio gera
- **ID de anúncio** - Rastreia o anúncio específico que gerou a conversa
- **Contexto da mensagem** - Veja o texto do anúncio que o cliente clicou

**Gerenciamento de Membros de Grupos:** *(Mega)*

Controle completo dos grupos de WhatsApp diretamente da MEGA:

- **Lista de membros** - Visualize todos os participantes do grupo com seu papel e status
- **Sincronização automática** - Os membros são sincronizados automaticamente ao criar a conversa
- **Adicionar participantes** - Adicione novos membros ao grupo pela plataforma
- **Remover participantes** - Remova membros do grupo sem sair da MEGA
- **Alterar papéis** - Promova ou rebaixe membros a administrador
- **Menções no grupo** - Use @ para mencionar membros específicos nas mensagens
- **Busca de membros** - Encontre rapidamente participantes em grupos grandes
- **Paginação inteligente** - Carregamento eficiente para grupos com muitos membros
- **Avatares de membros** - Visualize a foto de perfil de cada participante
- **Sincronização em segundo plano** - Atualização periódica de nomes e fotos
- **Suporte multi-provedor** - Funciona com Evolution, WAHA, Uazapi e Cloud API

### Instagram Direct

Conecte-se com seu público do Instagram e converta seguidores em clientes no lugar onde eles já interagem com sua marca.

**Por que Instagram?**

Com mais de 2 bilhões de usuários ativos, o Instagram é essencial para marcas visuais. 90% dos usuários seguem pelo menos uma empresa, e as DMs são o canal preferido para consultas.

**Tipos de interações suportadas:**

- **Mensagens diretas (DMs)** - Responda a consultas privadas de seus seguidores
- **Mega Hub para Instagram** *(Mega)* - Conecte Instagram por apps compartilhados do Hub usando credenciais dedicadas configuradas no Mega Hub
- **Respostas a Stories** - Atenda quem reage aos seus stories
- **Respostas a Stories com conteúdo** - Veja imagens e vídeos anexados quando respondem aos seus stories
- **Menções em Stories** - Receba alertas quando te mencionam
- **Reações** - Visualize quando reagem às suas mensagens

**Rastreamento de anúncios:**

Uma funcionalidade poderosa para medir o ROI da sua publicidade no Instagram:

- **Origem do lead** - Detecta automaticamente se a mensagem vem de um anúncio
- **Dados da campanha** - Salva qual anúncio gerou cada conversa
- **Atribuição automática** - Conecta vendas com campanhas específicas
- **Métricas claras** - Saiba exatamente quantos leads cada anúncio gera

**Janela de resposta estendida:**

- **7 dias para responder** - Em vez das 24 horas padrão, você tem até 7 dias para responder
- **Ativação automática** - Aplicada sem configuração adicional

**Conteúdo multimídia:**

- **Imagens e vídeos** - Envie e receba conteúdo visual
- **Respostas rápidas** - Botões para o cliente escolher opções
- **Catálogos de produtos** - Envie produtos diretamente no chat
- **Sugestões de conversa** - Ajude o cliente a iniciar o papo

**Benefícios para seu negócio:**

- Converta seguidores em compradores
- Atendimento ao cliente onde seus fãs já estão
- Meça o impacto da sua publicidade no Instagram

### Facebook Messenger

Atenda seus clientes diretamente pelo app de mensagens mais usado do mundo, integrado com suas páginas do Facebook.

**Por que Facebook Messenger?**

Com mais de 1,3 bilhão de usuários ativos, o Messenger é o canal preferido para clientes entrarem em contato com empresas. Seus clientes podem te escrever pela sua página do Facebook, anúncios ou diretamente pelo app.

**Funcionalidades principais:**

- **Conexão em minutos** - Vincule sua página do Facebook com alguns cliques, sem configuração técnica
- **Mega Hub para Messenger** *(Mega)* - Use apps compartilhados do Hub como alternativa configurável com credenciais dedicadas do Hub
- **Múltiplas páginas** - Gerencie todas as suas páginas do Facebook em uma só plataforma
- **Confirmações de leitura** - Saiba quando o cliente leu sua mensagem
- **Confirmações de entrega** - Verifique que suas mensagens chegaram corretamente
- **Mensagens de boas-vindas** - Cumprimente automaticamente clientes de primeira vez
- **Integração com bots** - Combine respostas automáticas com atendimento humano de forma fluida
- **Vinculação com Instagram** - Conecte sua conta do Instagram associada para gerenciar ambos os canais

**Benefícios para seu negócio:**

- Responda onde seus clientes já estão
- Histórico completo de conversas com cada cliente
- Transição suave entre chatbots e agentes humanos
- Métricas de desempenho por canal

### TikTok Business

Conecte-se com o público mais jovem e dinâmico do mundo através do TikTok, a rede social de maior crescimento.

**Por que TikTok?**

Com mais de um bilhão de usuários ativos, o TikTok se tornou uma plataforma essencial para alcançar a Geração Z e Millennials. Agora você pode atender consultas de clientes que te contatam através de mensagens diretas.

**Funcionalidades principais:**

- **Mensagens de texto** - Envie e receba mensagens com seus seguidores
- **Imagens** - Compartilhe e receba conteúdo visual
- **Stickers** - Visualize os stickers que seus clientes enviam
- **Posts compartilhados** - Quando um cliente compartilha um post com você, veja diretamente na conversa
- **Respostas a mensagens específicas** - Responda em contexto a mensagens anteriores
- **Perfil social do contato** - Veja o perfil do TikTok do cliente diretamente nos dados de contato
- **Mensagens não suportadas** - Indicadores claros quando conteúdo incompatível é recebido
- **Versão de API configurável** - Flexibilidade para adaptar-se a diferentes versões da API

**Benefícios para seu negócio:**

- Alcance o público mais jovem onde passam seu tempo
- Converta interações sociais em oportunidades de venda
- Conexão segura e oficial pela API do TikTok Business
- O acesso para conectar o TikTok é controlado por conta; contas hospedadas sem acesso podem solicitá-lo ao suporte pela configuração da caixa de entrada.
- Sincronização completa de mensagens em tempo real

### Email

O email continua sendo um dos canais mais importantes para comunicação empresarial. Gerencie todos os seus emails como se fossem conversas de chat.

**Por que integrar Email?**

Muitos clientes preferem email para consultas formais, documentação ou acompanhamento. Com a MEGA, todos os seus emails são gerenciados junto com os demais canais.

**Funcionalidades principais:**

- **Caixa unificada** - Todos os emails aparecem como conversas junto com WhatsApp, redes sociais e mais
- **Respostas ricas** - Envie emails com formatação, imagens e anexos
- **Imagens inline redimensionáveis** - Insira imagens no corpo do email e ajuste o tamanho visualmente
- **Assinaturas personalizadas** - Configure assinaturas profissionais por agente ou caixa de entrada
- **Qualquer provedor** - Conecte Gmail, Outlook, seu servidor próprio ou qualquer email
- **Configuração guiada** - Detecta Gmail ou Outlook pelo seu domínio para sugerir a integração correta
- **Verificação de conexão do Gmail** - Teste IMAP e SMTP em tempo real, consulte a atividade recente e reconecte a conta nas configurações da caixa de entrada
- **Exclusão permanente sincronizada com o Gmail** - Ao excluir um email ou conversa de uma caixa Gmail, ele também é excluído permanentemente no Gmail
- **Histórico completo** - Toda a sequência de emails visível em uma só conversa
- **Resposta citada** - Responda citando partes específicas do email original
- **Editor rico** - Formatação completa, listas, negrito, itálico, links

**Benefícios para seu negócio:**

- Um só lugar para emails e mensagens instantâneas
- Agentes não precisam alternar entre aplicativos
- Métricas unificadas de todos os canais

### Widget Web (Chat ao Vivo)

Ofereça atendimento instantâneo aos visitantes do seu site com um chat ao vivo elegante e totalmente personalizável.

**Por que Chat ao Vivo?**

Os visitantes do seu site querem respostas imediatas. Um chat ao vivo aumenta as conversões em até 40% e melhora a satisfação do cliente.

**Configuração do formulário:**

- **Formulário pré-chat** - Colete nome, email e telefone antes de iniciar
- **Campos personalizados** - Adicione os campos que precisa para seu negócio
- **Validação automática** - Garanta que os dados informados estão corretos; caixas de seleção obrigatórias devem estar marcadas antes do envio
- **Modo offline** - Receba mensagens mesmo quando não há agentes disponíveis

**Personalização visual completa:**

- **Cores da sua marca** - Ajuste cores primárias e de fundo
- **Seu logo** - Mostre sua marca no widget
- **Posição flexível** - Canto esquerdo ou direito
- **Ícone personalizado** - Mude o botão flutuante
- **Mensagem de boas-vindas** - Cumprimente proativamente os visitantes

**Funcionalidades avançadas:**

- **Identificação de usuários** - Reconheça usuários logados no seu site
- **Transcrição por email** - Cliente pode solicitar o histórico da conversa; novos envios ficam temporariamente desabilitados após um envio bem-sucedido
- **Modo escuro** - Se adapta às preferências do visitante
- **Help Center integrado** - Mostre artigos de ajuda diretamente no widget
- **Mensagens predefinidas** - Inicie conversas com contexto
- **Imagens inline nas respostas** - Envie capturas ou recursos visuais dentro do corpo da mensagem e ajuste o tamanho
- **Domínios permitidos** - Restrinja o widget a domínios autorizados para maior segurança
- **Mostrar nome do agente** - Configure por inbox se o nome do agente é exibido ao visitante
- **Controle de autoatribuicao por resposta** - Desative por inbox se conversas sem responsavel sao atribuidas ao agente quando ele envia uma mensagem
- **Proteção de conversas resolvidas** - Quando um inbox não permite mensagens após a resolução, o widget rejeita novas tentativas e envios de texto ou anexos para essa conversa; o visitante pode iniciar uma nova conversa
- **Camadas e fundos corrigidos** - Melhor renderização entre launcher e portal, inclusive no modo escuro

**Benefícios para seu negócio:**

- Converta visitantes em clientes enquanto navegam
- Reduza o abandono de carrinho
- Ofereça suporte imediato sem o cliente sair do seu site

### SMS

Alcance seus clientes mesmo quando não têm internet ou apps de mensagens, com mensagens de texto tradicionais.

**Por que SMS?**

O SMS tem uma taxa de abertura de 98%, muito maior que qualquer outro canal. É ideal para notificações urgentes, confirmações e comunicação com clientes que não usam apps.

**Funcionalidades principais:**

- **Envio e recebimento** - Comunicação bidirecional com seus clientes
- **Números virtuais** - Configure múltiplas linhas telefônicas
- **Integração com Twilio** - Provedor líder mundial de SMS
- **Campanhas em massa** - Envie mensagens para toda sua base de contatos

**Benefícios para seu negócio:**

- Alcance clientes sem smartphones ou dados
- Notificações que realmente são lidas
- Ideal para lembretes e confirmações

### Telegram

Conecte-se com milhões de usuários que preferem o Telegram pela sua velocidade, segurança e funcionalidades avançadas.

**Por que Telegram?**

O Telegram é especialmente popular entre usuários tech-savvy e em regiões como Europa Oriental, Oriente Médio e partes da América Latina. É conhecido por sua velocidade e privacidade.

**Funcionalidades principais:**

- **Configuração em minutos** - Conecte seu bot do Telegram facilmente
- **Mensagens formatadas** - Envie texto com negrito, itálico e mais
- **Multimídia completa** - Imagens, vídeos, documentos e mais
- **Botões interativos** - Ofereça opções de resposta rápida aos seus clientes
- **Respostas contextuais** - Responda a mensagens específicas para maior clareza
- **Telegram Business** - Suporte para contas empresariais do Telegram

**Benefícios para seu negócio:**

- Fotos de perfil automáticas dos contatos
- Sem limites de tamanho para arquivos
- Mensagens chegam instantaneamente

### Canal de API

Para empresas com necessidades únicas: integre qualquer sistema de mensagens próprio ou de terceiros.

> **Disponibilidade:** O acesso por tokens de API e a entrega de Webhooks de saída exigem acesso a API e Webhooks para a conta em planos hospedados. Eles continuam disponíveis em instalações autogerenciadas.

**Quando usar Canal de API?**

Se você tem seu próprio sistema de mensagens, um app mobile com chat, ou precisa conectar uma plataforma que não está integrada nativamente, o Canal de API te dá total flexibilidade.

**Funcionalidades principais:**

- **Integração personalizada** - Conecte qualquer fonte de mensagens
- **Webhooks de entrada** - Receba mensagens de sistemas externos
- **API de resposta** - Envie respostas de volta para seu sistema
- **API de envio universal para integrações** *(Mega)* - Uma única requisição autenticada identifica o destinatário por telefone, email, contato ou ID do provedor, prepara automaticamente o contato e a conversa e envia texto, mídia ou templates de WhatsApp por qualquer inbox compatível. Templates de mídia do WhatsApp Cloud podem carregar o arquivo na mesma requisição, e o conteúdo renderizado permanece visível na conversa. Chaves de idempotência tornam as tentativas seguras.
- **Sem limites** - Adapte a plataforma a qualquer canal imaginável

**Casos de uso:**

- Apps mobile com chat próprio
- Portais de clientes
- Sistemas legados de mensagens
- Integrações com provedores não suportados nativamente

### LINE

Conecte-se com usuários do LINE, o app de mensagens líder no Japão, Taiwan, Tailândia e Indonésia com mais de 200 milhões de usuários ativos.

**Por que LINE?**

Se seu negócio atende clientes na Ásia, LINE é imprescindível. No Japão, 90% dos usuários de smartphone usam LINE diariamente.

**Funcionalidades principais:**

- **Configuração simples** - Conecte sua conta LINE Official em minutos
- **Mensagens de texto** - Comunicação fluida com seus clientes
- **Stickers e multimídia** - Envie conteúdo visual atrativo
- **Segurança** - Credenciais protegidas com criptografia avançada

**Benefícios para seu negócio:**

- Acesso ao mercado asiático
- Usuários altamente engajados
- Ideal para e-commerce internacional

### Twitter / X

Atenda consultas e gerencie a reputação da sua marca na rede social onde acontecem as conversas públicas mais importantes.

**Por que Twitter/X?**

Twitter é onde os clientes expressam reclamações, fazem perguntas e buscam suporte publicamente. Uma resposta rápida e profissional pode transformar uma reclamação em uma avaliação positiva.

**Funcionalidades principais:**

- **Mensagens diretas (DMs)** - Gerencie conversas privadas com seus clientes
- **Menções públicas** - Opção para monitorar quando te mencionam
- **Criação automática de contatos** - Perfis do Twitter são salvos automaticamente
- **Conexão segura** - Autenticação oficial com a API do X

**Benefícios para seu negócio:**

- Responda rapidamente a reclamações públicas
- Converta interações em oportunidades
- Melhore a percepção da sua marca
- Identifique tendências e feedback de clientes

### Canal de Voz - Twilio *(Enterprise)*

Transforme sua equipe em um call center profissional com telefonia VoIP integrada diretamente na plataforma usando Twilio Voice SDK.

**Por que adicionar chamadas à sua operação?**

Alguns clientes preferem falar por telefone, especialmente para assuntos urgentes ou complexos. Com o Canal de Voz, seus agentes podem receber e fazer chamadas sem sair da MEGA.

**Stack Tecnológico:**

- **Twilio Voice SDK** - Provedor VoIP líder do setor
- **WebRTC** - Chamadas pelo navegador, sem software
- **TwiML Apps** - Tratamento personalizado de chamadas e roteamento
- **Provisão de números** - Obtenha números em 100+ países

**Chamadas de Entrada:**

- **Recepção inteligente** - Chamadas criam conversas automaticamente
- **Identificação do chamador** - Reconheça contatos existentes pelo número
- **Novos contatos automáticos** - Se o número é novo, o contato é criado
- **Histórico unificado** - Chamadas e mensagens na mesma timeline
- **Gestão de filas** - Gerencie alto volume de chamadas

**Chamadas de Saída:**

- **Click-to-call** - Ligue para qualquer contato com um só clique
- **Do perfil do contato** - Sem discar números manualmente
- **Chamadas em conferência** - Conecte agente e cliente facilmente
- **Personalização de Caller ID** - Mostre seu número comercial

**Acompanhamento completo:**

- Registro de todas as chamadas (atendidas, perdidas, ocupadas)
- Duração e timestamps de cada chamada
- Identificação de chamadas de entrada vs saída
- Todo histórico visível na conversa do cliente
- Gravação nativa opcional do Twilio com aceite explícito do custo de storage
- Gravações baixáveis na conversa e no relatório de chamadas

**Funcionalidades do Agente:**

- **Webphone no navegador** - Atenda chamadas diretamente na MEGA
- **Mute/Unmute** - Controle o microfone durante chamadas
- **Função de espera** - Coloque clientes em espera quando necessário
- **Transferir chamadas** - Roteie para outro agente ou departamento

**Benefícios para seu negócio:**

- Canal adicional sem trocar de ferramenta
- Contexto completo do cliente ao atender
- Métricas de chamadas junto com outros canais
- Escalável de 1 a 1000+ agentes
- Preços pay-as-you-go com Twilio

### Chamadas WhatsApp Cloud *(Enterprise/Mega)*

Faça e receba chamadas de voz pelo WhatsApp usando a Cloud API do Meta com tecnologia WebRTC.

> **Disponibilidade:** As chamadas não estão disponíveis para números do WhatsApp Cloud conectados por coexistência com o WhatsApp Business App. Elas continuam no aplicativo WhatsApp Business e não são exibidas na MEGA.

**Por que Chamadas WhatsApp?**

Muitos clientes preferem comunicação por voz para questões complexas. As Chamadas WhatsApp permitem que seus agentes gerenciem chamadas de voz diretamente na plataforma, usando o mesmo número do WhatsApp usado para mensagens.

**Chamadas de Entrada:**

- **Notificações em tempo real** - Agentes recebem alertas de chamada instantâneos
- **Aceitar/Rejeitar do navegador** - Gerencie chamadas sem app externo
- **Atribuição inteligente de agentes** - Chamadas roteadas para membros disponíveis do inbox; administradores que ativaram as notificações de chamadas são usados apenas como alternativa
- **Auto-rejeição quando indisponível** - Comportamento configurável
- **Identificação do chamador** - Veja informações do contato antes de atender

**Chamadas de Saída (Business-Initiated):**

- **Click-to-call** - Inicie chamadas pela conversa ou pelo perfil de um contato, inclusive quando ele ainda não tiver uma conversa
- **Sistema de permissões** - Solicite e rastreie permissões de chamada dentro da janela de atendimento de 24 horas
- **Uma chamada por agente** - Impede iniciar uma segunda chamada enquanto o agente já tem uma ativa, inclusive em outra aba
- **Modelos de permissão de chamada** - Use modelos aprovados de solicitação de permissão no ReplyBox, defina um padrão por inbox e veja o envio na linha do tempo da conversa
- **Status de permissão** - Diferencie visualmente entre sem permissão, permissão temporária de 7 dias e permanente; confirme o status e a disponibilidade para iniciar uma chamada com o WhatsApp e registre cada alteração, inclusive o vencimento temporário, na atividade da conversa
- **Tom de ringback** - Feedback de áudio durante conexão

**Funcionalidades durante a chamada:**

- **WebRTC nativo** - Áudio de alta qualidade sem SDKs externos
- **Atribuição protegida** - Da aceitação até o encerramento da chamada, não é possível alterar o agente nem a equipe da conversa; enquanto ela apenas toca, a reatribuição continua disponível
- **Mute/Unmute** - Alterne o microfone durante chamadas
- **Duração da chamada** - Timer em tempo real visível
- **Otimização VoIP** - Áudio otimizado para chamadas de voz

**Histórico de Chamadas:**

- **Registro completo** - Todas as chamadas registradas na conversa
- **Metadados detalhados** - Duração, status, timestamps
- **Indicador de direção** - Entrada vs saída claramente marcados
- **Rastreio de status** - Atendida, perdida, rejeitada, etc.

**Configuração:**

- Requer WhatsApp Cloud API inbox
- Ativar recursos de chamadas nas configurações do inbox
- Janela de atendimento aberta ou template aprovado para reabrir a conversa antes de solicitar permissão
- Configurar permissões de agentes
- Configurar auto-rejeição para agentes offline

**Ideal para:**

- Equipes usando WhatsApp Cloud API oficial
- Empresas que precisam de chamadas de voz junto com chat
- Equipes que precisam da confiabilidade da API oficial

---

## 💬 Gestão de Conversas

### Caixa de Entrada Inteligente

- **Visão unificada** - Todas as conversas em um só lugar
- **Filtros avançados** - Por status, caixa de entrada, agente, equipe, etiquetas
- **Filtros multi-seleção** - Selecione múltiplas caixas de entrada ou equipes simultaneamente
- **Filtros de etiquetas com lógica AND** - Filtre por múltiplas etiquetas que devem todas corresponder
- **Visões personalizadas** - Salve filtros frequentes como visões rápidas
- **Busca poderosa** - Encontre conversas por conteúdo, contato ou metadados
- **Filtros rápidos no sidebar** - Navegue direto para Não lidas, Menções, Participando, Grupos e Não atendidas na barra lateral
- **Badges reativos de não lidas** - Menções, Participando, Grupos e Não lidas exibem contadores em tempo real sem recarregar
- **Data e hora exatas ao passar o cursor** - Datas relativas exibem a data e a hora completas na lista de conversas, mensagens, contatos, busca, relatórios e cartões relacionados do dashboard

### Integrações com atributos personalizados

As integrações podem atualizar apenas as chaves enviadas dos atributos personalizados de uma conversa ou substituí-los por completo. Elas também podem remover chaves específicas sem alterar as informações restantes.

### Busca de Mensagens na Conversa

Encontre mensagens específicas dentro de uma conversa:

- **Busca de texto** - Procure palavras ou frases em todas as mensagens
- **Busca em transcrições de áudio** - Encontre mensagens de voz por palavras ou frases contidas na transcrição
- **Filtro por datas** - Restrinja a busca a um período específico
- **Destaque de resultados** - Mensagens encontradas são destacadas visualmente
- **Scroll automático** - Navegue instantaneamente até a mensagem encontrada
- **Paginação de resultados** - Navegue entre múltiplas correspondências facilmente
- **Contexto preservado** - Veja a mensagem em seu contexto original de conversa

### Status de Conversa

- **Aberta** - Conversas que precisam de atenção
- **Pendente** - Aguardando resposta do cliente
- **Resolvida** - Conversas finalizadas
- **Adiada (Snooze)** - Programe reativação automática usando linguagem natural: escreva "amanhã às 3pm", "em 2 horas", "próxima segunda" ou qualquer expressão de tempo e o sistema interpreta automaticamente; seletor de data clássico também disponível

### Priorização

- **Níveis de prioridade** - Urgente, Alta, Média, Baixa
- **Ordenação inteligente** - Por atividade recente, tempo de espera, prioridade
- **Ordenação por não lidas** - Priorize conversas com mensagens não lidas diretamente no seletor de ordenação
- **Indicadores visuais** - Identifique rapidamente conversas críticas

### Colaboração em Equipe

- **Atribuição de agentes** - Manual ou automática
- **Atribuição de equipes** - Encaminhe para departamentos específicos
- **Menções (@)** - Notifique colegas nas conversas
- **Notas privadas** - Comunique-se internamente sem o cliente ver
- **Contador de menções em nota privada** - Menções internas atualizam o badge de Menções no sidebar em tempo real
- **Participantes** - Múltiplos agentes em uma conversa

### Participantes de Conversa *(Enterprise)*

Adicione múltiplos agentes para colaborar em conversas:

**Funcionalidades:**

- **Adicionar participantes** - Convide agentes para ajudar na conversa
- **Remover participantes** - Gerencie quem pode ver/interagir
- **Notificações** - Participantes recebem atualizações
- **Colaboração** - Todos podem responder e adicionar notas
- **Visibilidade** - Participantes veem toda a conversa

**Casos de uso:**

- Escalonar para especialistas mantendo o agente original
- Supervisores acompanhando conversas específicas
- Trabalho em equipe para casos complexos

### Conversas Fixadas (Pinned)

Fixe conversas importantes para acesso rápido:

**Funcionalidades:**

- **Fixar/desafixar** - Mantenha conversas importantes no topo
- **Seção dedicada** - Lista separada de conversas fixadas
- **Por agente** - Cada agente gerencia suas próprias fixadas
- **Acesso rápido** - Nunca perca de vista casos importantes

**Casos de uso:**

- VIPs que precisam de atenção constante
- Casos em andamento de alta prioridade
- Conversas com acompanhamento contínuo

### Filtros Personalizados (Pastas)

Crie visões personalizadas para organizar suas conversas:

**Funcionalidades:**

- **Criar pastas** - Organize conversas em grupos lógicos
- **Filtros múltiplos** - Combine condições (status, etiquetas, agente, inbox)
- **Multi-etiqueta consistente** - Normalização de valores em filtros com múltiplas etiquetas
- **Salvar visões** - Acesse rapidamente filtros frequentes
- **Acesso no sidebar** - Pastas aparecem no menu lateral

**Tipos de filtros:**

- **Por status** - Abertas, pendentes, adiadas, resolvidas
- **Por etiqueta** - Conversas com etiquetas específicas
- **Por agente** - Conversas de agentes específicos
- **Por inbox** - Conversas de canais específicos
- **Por equipe** - Conversas de equipes específicas
- **Combinações** - Múltiplas condições com AND/OR

### Respostas Prontas (Canned Responses)

Templates rápidos com atalhos para respostas mais rápidas:

- **Respostas pessoais** - Visíveis apenas para você
- **Respostas compartilhadas** - Disponíveis para toda a equipe
- **Ativação por atalho** - Digite / para acessar respostas
- **Substituição de variáveis** - Placeholders dinâmicos para dados do contato
- **Suporte a anexos** - Inclua imagens, documentos e arquivos nas respostas
- **Múltiplos anexos** - Anexe vários arquivos a uma resposta pronta
- **Anexos também em nova conversa** - Reutilize arquivos de respostas prontas mesmo ao iniciar uma nova conversa
- **Busca com visualização** - Busque por atalho e conteúdo, visualize a resposta renderizada e preserve variáveis sem valor para o backend
- **Busca instantânea em cache** - Carregue as respostas uma vez por conta e filtre localmente enquanto a invalidação em tempo real mantém os dados atualizados
- **Conteúdo rico** - Formate texto com suporte a markdown

### Gravador de Voz

- **Notas de áudio** - Grave e envie mensagens de voz
- **Gravação fácil** - Iniciar/parar com um clique
- **Preview** - Ouça antes de enviar

### Outras Ferramentas de Produtividade

- **Anexos multimídia** - Imagens, vídeos, documentos
- **Suporte a arquivos PFX** - Envie certificados `.pfx` com reconhecimento visual e de tipo adequado
- **Emojis e GIFs** - Comunicação mais próxima
- **Resposta citada (Reply-to)** - Responda a mensagens específicas
- **Rascunhos de mensagens** - Salva automaticamente rascunhos enquanto você digita, restaurados ao voltar à conversa
- **Editor de resposta redimensionável** - Ajuste manualmente a altura da caixa de resposta para lidar melhor com conversas longas
- **Edição de mensagens** - Corrija mensagens enviadas (canais compatíveis)
- **Exclusão de mensagens** - Remova mensagens enviadas por engano

### Resolução Automática

- **Auto-resolve** - Feche conversas inativas automaticamente
- **Temporizadores configuráveis** - Defina tempos por caixa de entrada
- **Limpeza de conversas órfãs** - Remove automaticamente conversas sem contato associado

### Ações em Lote (Bulk Actions)

Realize operações em massa em múltiplas conversas simultaneamente:

- **Resolver em lote** - Feche múltiplas conversas de uma vez
- **Reabrir em lote** - Reabra conversas resolvidas
- **Adiar em lote** - Aplique snooze em várias conversas
- **Atribuir em lote** - Atribua agente ou equipe a múltiplos chats
- **Etiquetar em lote** - Aplique etiquetas em massa
- **Atalhos de teclado** - Execute ações bulk com hotkeys

### Ações sobre Contatos (Bulk)

- **Mesclar contatos** - Combine contatos duplicados
- **Etiquetar contatos** - Aplique etiquetas a múltiplos contatos
- **Excluir contatos** - Exclusão em massa com confirmação

### Command Bar (Barra de Comandos)

Acesso rápido a qualquer ação via teclado:

- **Ativação rápida** - Abra com `Cmd/Ctrl + K`
- **Busca de ações** - Encontre comandos digitando
- **Navegação** - Vá para conversas, contatos, configurações
- **Mudança de aparência** - Modo claro, escuro ou sistema
- **Atribuição rápida** - Atribua agentes ou equipes
- **Mudança de status** - Resolva, reabra, adie
- **Ações de IA** - Acesse funções do Captain
- **Execução de macros** - Em uma conversa aberta, escolha **Executar uma macro** para usar as mesmas macros ordenadas da barra lateral

### Modo Escuro (Dark Mode)

- **Tema escuro** - Interface otimizada para ambientes com pouca luz
- **Tema claro** - Interface tradicional clara
- **Modo sistema** - Segue a preferência do sistema operacional
- **Widget adaptável** - O widget também suporta modo escuro

---

## 💬 Comunicação Interna da Equipe

### Salas de Chat (Chat Rooms) *(Mega)*

Sistema de salas de chat internas para comunicação fluida da equipe sem sair da plataforma. Perfeito para coordenação, perguntas rápidas e discussões internas.

**Por que Salas de Chat Internas?**

Mantenha sua equipe conectada e produtiva. Em vez de usar ferramentas externas como Slack ou Teams para comunicação interna, gerencie tudo em um só lugar junto com as conversas com clientes.

**Funcionalidades Principais:**

**Gestão de Salas (Settings):**

- **Criar salas** - Administradores podem criar salas com nome e descrição; o nome preserva as maiúsculas informadas e continua único na conta sem diferenciar maiúsculas de minúsculas
- **Canais públicos e privados** - Defina visibilidade e audiência para cada fluxo da equipe
- **Categorias** - Agrupe canais por tema, equipe ou departamento
- **Adicionar usuários** - Seleção múltipla de membros da equipe de sua conta
- **Editar salas** - Atualizar nome, descrição e membros pelo menu de três pontos do cabeçalho
- **Excluir salas** - Remover salas com confirmação de segurança
- **Avatares de sala** - Imagens personalizadas opcionais para cada sala
- **Chamadas de áudio e vídeo** - Comunicação WebRTC entre membros em DMs, grupos e canais, com tons e histórico de chamadas em andamento, perdidas e concluídas
- **Disponibilidade seletiva de chamadas** - As chamadas exigem a feature de conta independente `chat_room_calls`, desabilitada por padrão e habilitável apenas para contas selecionadas; as mensagens de Chat Rooms continuam disponíveis sem ela
- **Conectividade ICE administrável** - Super Admin > Call ICE permite configurar STUN/TURN e suas credenciais sem reiniciar; as variáveis de ambiente `MEGA_CALL_*` continuam compatíveis quando não há valores salvos
- **Conectividade premium por conta** - `chat_room_calls` usa Google STUN para chamadas P2P normais; a feature premium `premium_call_connectivity` muda essa conta para Call ICE e habilita TURN como fallback quando a configuração global está completa
- **Experiência nativa de chamadas** - O áudio mantém o widget compacto do WhatsApp/Twilio; o vídeo usa um espaço amplo limitado ou uma janela flutuante dentro do Mega, com câmera e tela simultâneas, palco de apresentação, trilho de participantes, avatares e mute autorizado pelo iniciador para pequenos grupos controlados
- **Localização** - Acessível em Settings > Chat Rooms

> **Nota:** As configurações de Salas de chat gerenciam apenas canais (públicos e privados). Mensagens diretas (DMs) são conversas pessoais gerenciadas a partir da barra lateral de chat e não aparecem nem podem ser editadas/excluídas em Settings.

**Permissões e Visibilidade:**

- **Administradores** - Veem TODAS as salas da conta na barra lateral, podem criar/editar/excluir qualquer canal, podem participar de todas as salas
- **Agentes e Funções Personalizadas** - Apenas veem as salas onde são membros na barra lateral, só podem participar de suas salas atribuídas, não podem criar/editar/excluir salas

**Interface de Chat:**

- **Localização na barra lateral** - Conversas > Salas
- **Busca integrada** - Encontre canais, mensagens diretas e mensagens dentro das salas
- **Filtros rápidos** - Tudo, canais, mensagens diretas, rascunhos e arquivadas
- **Seções visuais** - Rascunhos, favoritos, mensagens diretas, canais e arquivadas
- **Criação rápida** - Crie canais, categorias e mensagens diretas pela lista
- **Visualização de sala** - Cabeçalho com nome da sala + lista de mensagens + campo de envio
- **Design limpo** - 100% Tailwind CSS, moderno e responsivo

**Tipos de Mensagens:**

- **Mensagens de texto** - Comunicação de texto simples
- **Multimídia** - Imagens, vídeos, arquivos de áudio, documentos
- **Responder (Reply)** - Responder a mensagens específicas (cita a original)
- **Threads de resposta** - Abrir um painel lateral por mensagem, responder dentro da thread e opcionalmente publicar também no canal
- **Reações** - Responder rapidamente a mensagens com emoji
- **Mensagens fixadas** - Manter informações importantes visíveis na sala
- **Enquetes** - Criar votações com múltiplas opções pelo composer
- **Rascunhos** - Recuperar texto não enviado por usuário e sala
- **Status de digitação** - Ver quando outros membros estão digitando
- **Gravação de áudio** - Gravador de áudio integrado para notas de voz

**Layout Inteligente de Mensagens:**

- **Lado direito** - Suas próprias mensagens (saída)
  - Cor de fundo diferente
  - Seu avatar exibido
- **Lado esquerdo** - Mensagens de outros usuários (entrada)
  - Avatar do remetente exibido
  - Identificação clara do remetente

**Notificações em Tempo Real:**

- **Integração WebSocket** - Usando Action Cable para entrega instantânea
- **Atualizações ao vivo** - Mensagens aparecem imediatamente sem atualizar
- **Eventos de sala** - Atualização, exclusão, leitura, unread, reações, enquetes e digitação
- **Transmissão inteligente** - Administradores recebem eventos de todas as salas, usuários regulares apenas de suas salas
- **Rastreamento de eventos** - Eventos de mensagem criada e atualizada

**Segurança e Validações:**

- **Acesso apenas para membros** - Apenas membros da sala podem ver e enviar mensagens
- **Controles de administrador** - Apenas administradores podem gerenciar salas
- **Validação de conta** - Associação à sala é validada em relação à conta
- **Nomes únicos** - Nomes de sala devem ser únicos por conta

**Benefícios para sua equipe:**

- Não precisa alternar entre ferramentas para comunicação interna
- Discussões contextuais sem sair da visualização de clientes
- Comunicação organizada por tópico ou departamento
- Histórico completo de mensagens e arquivo pesquisável
- Controle de acesso seguro baseado em permissões

---

## 🤖 Automação e IA

### Regras de Automação

Configure fluxos automáticos baseados em eventos e condições:

- **Regras com espera** - Execute ações entre 10 minutos e 30 dias depois, enquanto a conversa permanecer em um status selecionado, o cliente não responder ou ninguém da equipe responder. Podem combinar condições adicionais com `AND`; uma resposta, mudança de status ou condição não atendida cancela a execução pendente.

**Eventos disponíveis:**

- Conversa criada
- Conversa atualizada
- Mensagem recebida
- Mensagem criada

**Condições:**

- Status, caixa de entrada, etiquetas, idioma
- País, navegador, email
- Atributos personalizados
- Conteúdo da mensagem
- Nota privada (mensagem interna)

**Ações:**

- Enviar mensagem automática
- Atribuir agente/equipe
- Atribuir ao último agente que respondeu
- Remover atribuição de agente/equipe
- Adicionar/remover etiquetas
- Alterar status ou prioridade
- Enviar webhook
- Enviar transcrição por email
- Silenciar conversa
- Redistribuir para agentes online

### Macros

Execute múltiplas ações com um só clique:

- **Macros pessoais** - Visíveis apenas para você
- **Macros globais** - Disponíveis para toda a equipe
- **Ações em cadeia** - Combine múltiplas operações
- **Atalho no editor de resposta** - Digite `#` para buscar, visualizar e executar macros sem sair da conversa
- **Atalho na barra de comandos** - Abra `Cmd/Ctrl + K` em uma conversa para selecionar a mesma macro ordenada; os atributos obrigatórios usam o diálogo compartilhado de resolução

### Agent Bots

- **Bots de webhook** - Conecte com lógica externa via HTTP
- **Integração Typebot** - Conecte com fluxos conversacionais do Typebot
- **Handover para humanos** - Transferência suave para agentes reais
- **Handover inteligente** - Se um humano responder em conversa pendente do bot, a transferência ocorre automaticamente
- **Handover por expiração** - Quando uma sessão de Webhook expira, a conversa é aberta, libera o bot e tenta a atribuição automática a um agente elegível; se ninguém estiver disponível, permanece aberta e sem atribuição
- **Bots por caixa de entrada** - Configure bots específicos por canal
- **Propriedade explícita do bot** - Conversas tratadas por um Agent Bot conectado ficam pendentes e atribuídas ao bot; a abertura, o handover por uma pessoa ou a desconexão do bot libera essa propriedade sem substituir atribuições humanas explícitas
- **Fila humana sem atribuição** - Conversas atribuídas a um Agent Bot não aparecem na fila Sem atribuição; ela inclui apenas conversas sem agente humano nem bot
- **Assumir pelo painel** - Enquanto um Agent Bot atende uma conversa pendente, o compositor fica em modo de nota privada e oferece uma ação para assumir, reabrir a conversa e atribuí-la ao agente atual
- **Atribuição manual restrita por inbox** - O seletor de agente oferece apenas Agent Bots ativos configurados no inbox da conversa
- **Indicador de digitação** - Os bots podem ativar e desativar o indicador "digitando..." para uma experiência mais natural
- **Opções avançadas de webhook** *(Enterprise)* - Configure timeout personalizado para requisições do bot, novas tentativas automáticas em caso de falha e tratamento granular de erros; melhora a confiabilidade das integrações com sistemas externos lentos ou instáveis
- **Assinaturas de webhook por canal** - Permite assinar eventos de saída de Agent Bots e canais API para validar autenticidade ponta a ponta

### Typebot *(Mega — Opções Avançadas)*

Além da integração padrão, a MEGA estende as capacidades do Typebot com comandos especiais:

- **Atribuição de agente via MEGA_CMD** - Use o comando `MEGA_CMD:assign_agent:email@empresa.com` no Typebot para atribuir automaticamente a conversa a um agente específico
- **Atribuição de equipe via MEGA_CMD** - Use `MEGA_CMD:assign_team:nome_equipe` para encaminhar a conversa à equipe correspondente de dentro do fluxo do bot
- **Placeholders de lista** - Injete listas dinâmicas de agentes ou equipes como variáveis Typebot para criar menus de seleção personalizados
- **Primeira mensagem só com mídia** - Abre corretamente nova conversa quando a primeira interação não tem texto
- **Reações de WhatsApp ignoradas** - Reações não iniciam o fluxo nem são enviadas ao Typebot como mensagens
- **Compatibilidade de localização** - Encaminha coordenadas em formato de link de mapas para continuidade do fluxo
- **Delay padrão estável** - Comportamento mais previsível quando o bot não define atraso explícito
- **Sem código adicional** - Tudo é configurado diretamente no fluxo do Typebot, sem modificar o bot da MEGA

### Captain *(Enterprise)*

Assistente de IA avançado que transforma como sua equipe trabalha.

**Assistentes de IA:**

Crie assistentes especializados para diferentes necessidades:

- **Múltiplos assistentes** - Configure assistentes diferentes por caixa de entrada
- **Contexto personalizado** - Cada assistente entende seu domínio específico
- **Personalidade configurável** - Defina tom, estilo e abordagem
- **Modelos por função** - Configure modelos separados para Assistant, Copilot, sugestões e geração de FAQs a partir de documentos e PDFs
- **Roteamento de modelos internos** - Superadministradores podem configurar separadamente o avaliador de conversas inativas; o override da conta tem prioridade sobre o modelo de instalação em ambientes auto-hospedados, enquanto as preferências do Captain para clientes mantêm os recursos internos ocultos
- **Sugestões de FAQ por conversa** - Conversas resolvidas com respostas reutilizáveis de agentes humanos são agrupadas em sugestões de FAQ para revisão; agentes só revisam sugestões e conversas de origem às quais têm acesso e podem editar, aprovar ou descartar sugestões abertas para publicar FAQs confiáveis
- **Troca fácil** - Alterne entre assistentes conforme necessário
- **Exclusividade com bots externos** - O Captain não responde nem agenda resolução automática em inboxes com um Agent Bot ativo ou Dialogflow
- **Visão geral do assistente** - Um redesenho opcional combina insights rotativos do período com métricas de resultados, fluxo e comparação de tendências de resolução, CSAT do Captain, uso e cobertura de conhecimento; preserva a visão legada por padrão e usa conjuntos de dados dedicados de resultados, fluxo e tendência de resolução
- **Detalhes da geração** - Abra o indicador “Gerado pelo Captain” em uma resposta do assistente ou nota privada de transferência para ver as etapas de ferramentas e cenários, fontes da base de conhecimento e raciocínio; o modelo e os créditos ficam disponíveis apenas para superadministradores
- **Citações confiáveis** - O Captain V2 exibe somente links web públicos validados pelo servidor, registra as fontes realmente selecionadas e mantém as URLs renderizadas fora do histórico enviado ao modelo; sessões anteriores preservam suas fontes existentes
- **Disponibilidade em planos pagos** - O Captain V2 é ativado automaticamente quando uma conta cloud é reconciliada com qualquer plano pago; o plano padrão permanece sem Captain V2
- **Compreensão de imagens** - O assistente pode analisar imagens enviadas nas conversas
- **Suporte multimodal** - Processa texto e imagens simultaneamente para respostas contextuais
- **Ignorar grupos** - Configure o assistente para não responder em conversas de grupo
- **Alvos ignorados** - Defina conversas ou contatos específicos que o assistente deve pular
- **Público e horário** - Limite as respostas a contatos que atendem a condições configuráveis e escolha se o assistente responde sempre, durante ou fora do horário comercial; as conversas fora dessas regras vão para a fila humana
- **Resolução por inatividade** - Com o Captain V2, cada assistente escolhe se o Captain revisa a conversa, sempre a resolve ou aguarda o cliente; os modos que resolvem usam um temporizador de 5 minutos a 24 horas e podem enviar uma mensagem de encerramento opcional

**Base de Conhecimento (Documentos):**

Treine o Captain com seu próprio conteúdo:

- **Upload de arquivos** - PDF, Word, texto e mais
- **URLs de sites** - Ingira páginas web automaticamente
- **Campos de auto-sincronização** - Registre status e data da última sincronização para manter as fontes atualizadas
- **Auto-sincronização escalonada** - Atualize fontes web conforme o plano com execução distribuída para evitar picos de carga
- **Texto puro** - Adicione conhecimento diretamente
- **FAQs** - Respostas estruturadas pergunta/resposta
- **Detalhes do documento** - Revise o conteúdo rastreado, os metadados da fonte e a
  quantidade de FAQs geradas
- **Uso em conversas** - Administradores podem ver as conversas distintas que usaram um documento ou uma FAQ criada por usuário, ordenar documentos por uso e abrir a lista de conversas; transferências e conversas excluídas não são consideradas
- **Vinculação com Help Center** - Use artigos existentes como base

**Cenários de IA:**

Fluxos automatizados que o Captain pode executar:

- **Ações predefinidas** - Mapeie ações comuns para o Captain executar
- **Coleta de informação** - Recolha dados do cliente antes de transferir
- **Execução de tarefas** - Deixe o Captain realizar ações por você
- **Gerenciamento de status** - Administradores podem ativar ou desativar cenários; os desativados continuam disponíveis para gerenciamento, mas não são executados pelo Captain
- **Criação completa por MCP** - IAs conectadas ao MCP da conta podem salvar e atualizar IDs de ferramentas integradas, personalizadas e MCP; IDs indisponíveis são rejeitados explicitamente
- **Escalonamento inteligente** - Saiba quando transferir para humano

**Ferramentas Personalizadas:**

Estenda as capacidades do Captain com integrações:

- **Contratos tipados completos** - Tools personalizadas e MCP preservam objetos, arrays, enums e campos aninhados; os cenários só as recebem quando estão habilitadas e conectadas

- **Chamadas de API** - Conecte o Captain com sistemas externos
- **Métodos HTTP ampliados** - Suporte a GET, POST, PUT, PATCH e DELETE nas ferramentas
- **Ferramentas personalizadas** - Crie ações específicas para seu negócio
- **Desativação segura** - Administradores recebem um aviso antes de desativar uma ferramenta usada por cenários ativos; ferramentas desativadas continuam visíveis e preservam referências salvas sem serem executadas
- **Contexto dinâmico** - Busque informação em tempo real

**Servidores MCP (Model Context Protocol):**

Conecte servidores MCP para ampliar as capacidades do seu assistente:

- **MCP nativo por conta** - Crie servidores MCP por conta com endpoint dedicado
- **Acesso seguro e flexível** - Compatível com autenticação OAuth e token estático
- **Arquivos de qualquer provedor de IA** - O ChatGPT descobre seu seletor nativo; Claude e outros clientes podem usar URL HTTPS temporária, base64, multipart ou signed ID sem exigir uma URL pública permanente
- **Upload direto autenticado** - Clientes MCP JSON podem solicitar destinos assinados pela API sem depender de CSRF do navegador
- **Outbound universal via MCP** - Inicie texto, mídia ou templates para telefone, email, contato ou identidade do provedor; arquivos diretos também funcionam em cabeçalhos de mídia de templates, e referências inválidas são rejeitadas antes do envio
- **Catálogo de uso cotidiano** - Publica ferramentas prontas para operações diárias da conta
- **Cobertura operacional ampliada** - Inclui agendamento, tarefas, campanhas, SLA, calendário, relatórios, notificações e chat interno; não expõe importação nem exportação de dados
- **Help Center via MCP** - Consulte, busque e obtenha artigos e categorias a partir de agentes conectados
- **Atribuição a assistentes** - Vincule servidores MCP a assistentes específicos
- **Ações nativas atribuídas ao Captain** - Execuções MCP nativas assinadas preservam o assistente como remetente e confirmam mensagens entregues sem duplicação nem handoff acidental
- **Playground fiel à produção** - O catálogo permanece disponível para configurar cenários. Com o Captain V2, o playground testa handoffs reais e carrega somente as tools atribuídas ao cenário; o fluxo legado testa o assistente base sem seleção direta
- **Gestão centralizada** - Administre todos seus servidores MCP nas configurações

**Modo Auto-Resolve do Captain:**

Configure como o Captain gerencia a resolução automática de conversas:

- **Modo avaliado** - O Captain analisa o contexto, incluindo o status da conversa e os papéis dos participantes, e decide autonomamente se resolve ou mantém a conversa aberta; transferências e acompanhamentos pendentes permanecem em aberto
- **Modo legado** - Comportamento original: resolve automaticamente conversas pendentes com base no temporizador
- **Modo desativado** - O Captain não resolve conversas automaticamente
- **Por assistente** - Cada assistente salva sua própria política; assistentes sem política salva mantêm a configuração da conta como compatibilidade

**Copilot para Agentes:**

Assistência em tempo real enquanto os agentes trabalham:

- **Sugestões de resposta** - IA gera respostas sugeridas baseadas no contexto
- **Rascunhos orientados pelo assistente** - Ao sugerir uma resposta, o Copilot usa instruções, FAQs, citações e ferramentas GET do assistente selecionado; o agente revisa e edita o rascunho antes de enviar
- **Sugestões legíveis** - Sugestões longas expandem o editor de resposta até 350 px sem substituir o tamanho escolhido manualmente
- **Resumo de conversa** - Obtenha contexto rapidamente de conversas longas
- **Busca no Help Center** - Encontre artigos relevantes automaticamente
- **Melhoria de texto** - Corrija gramática e melhore tom
- **Tradução instantânea** - Traduza mensagens on-the-fly

**Funcionalidades de IA:**

- **Correção gramatical** - Conserte erros em um clique
- **Expansão de texto** - Amplie respostas curtas
- **Simplificação** - Torne respostas complexas mais claras
- **Mudança de tom** - Formal, amigável, profissional
- **Resumos** - Condense conversas longas

**Transcrição de Áudio:**

Transcreva automaticamente mensagens de áudio para texto:

- **Transcrição automática** - Converta notas de voz em texto legível
- **Controle de gravações de chamadas** - Ative ou desative a transcrição por provedor (WhatsApp Cloud e WaVoIP)
- **Diarização de chamadas** - Separa gravações por turno usando o nome do contato e do agente atribuído
- **Transcrição manual** - Enfileira a transcrição pelo menu contextual quando uma mensagem de áudio ainda não tem texto
- **Modelos OpenAI** - Usa GPT-4o Mini Transcribe por padrão para notas de voz, com Whisper disponível como override por conta; para gravações de chamadas, normaliza o áudio e combina diarização GPT-4o com GPT-4o Transcribe para melhorar a fidelidade
- **Multi-idioma** - Suporte para múltiplos idiomas
- **Contexto nas conversas** - Os agentes podem ler o conteúdo dos áudios rapidamente

**Provedores de IA suportados:**

- **OpenAI** - GPT-4o, GPT-4, GPT-3.5 Turbo
- **Anthropic** - Claude (Sonnet, Opus, Haiku)
- **Google** - Gemini (Pro, Flash)
- **Azure OpenAI** - Implementações de OpenAI no Azure
- **Amazon Bedrock** - Modelos hospedados na AWS
- **DeepSeek** - Modelos de IA de código aberto

---

## 👥 CRM e Gestão de Contatos

### Perfis de Contato

- **Informação completa** - Nome, email, telefone, localização
- **Avatar automático** - Foto de perfil quando disponível
- **Última atividade** - Acompanhamento de interações
- **Tipo de contato** - Visitante, Lead, Cliente

### Atributos Personalizados

- **Campos flexíveis** - Crie atributos para contatos e conversas
- **Tipos de dados** - Texto, número, lista, data, checkbox, link
- **Integração com automações** - Use atributos como condições
- **Visibilidade configurável** *(Enterprise)* - Defina quais funções (roles) podem ver cada atributo; oculte campos sensíveis de agentes com nível inferior

### Etiquetas

- **Organização flexível** - Categorize contatos e conversas
- **Etiquetas de conversa** - Classifique por tema ou status
- **Busca rápida ao atribuir** - Filtre etiquetas de forma aproximada no menu de contexto de uma conversa, com as já atribuídas primeiro
- **Etiquetas de contato** - Segmente sua base de clientes
- **Cores personalizadas** - Identificação visual rápida

### Empresas/Companies *(Enterprise)*

- **Agrupe contatos** - Organize contatos por empresa
- **Seletor de empresa em contatos** - Atribua, limpe ou crie uma empresa diretamente pelo formulario do contato
- **Acesso por função personalizada** - Administradores podem conceder a permissão "Gerenciar empresas" a funções personalizadas para que vejam e gerenciem o menu Empresas
- **Domínio automático** - Associação por domínio de email
- **Visão unificada** - Histórico de todas as conversas da empresa
- **Favicon automático** - O sistema baixa automaticamente o favicon do domínio da empresa para exibir como avatar; funciona com qualquer site que tenha favicon configurado

### Notas

- **Notas por contato** - Documente informações importantes
- **Histórico interno** - Mantenha contexto entre interações

### Importação de Dados

- **Upload de CSV** - Importe contatos em massa
- **Mapeamento de campos** - Associe colunas com atributos
- **Importação histórica do Intercom** - Administradores podem importar contatos, conversas e mensagens históricas do Intercom em segundo plano
- **Monitoramento da importação** - Consulte o progresso, registros ignorados, erros e baixe os registros de ignorados
- **Nova tentativa de importação interrompida** - Tente novamente uma importação do Intercom interrompida após 15 minutos sem perder o progresso
- **Validação automática** - Detecte erros antes de importar
- **Acesso controlado** - Importação e exportação disponíveis para administradores e gestores de contatos
- **Exportação segura** - Valores iniciados por caracteres de fórmula são exportados como texto para impedir sua execução em planilhas

### Bloqueio de Contatos

- **Bloqueio manual** - Evite mensagens de contatos problemáticos
- **Filtragem automática** - Não aparecem na caixa de entrada principal
- **Bloqueio ativo no WhatsApp** - Mensagens recebidas de contatos bloqueados são descartadas antes de abrir conversa

### CRM V2 *(Beta)*

Sistema avançado de gestão de relacionamento com clientes:

**Visão 360° do cliente:**

- **Perfil unificado** - Todas as informações em um lugar
- **Histórico completo** - Todas as interações e canais
- **Timeline de atividades** - Cronologia de eventos

**Funcionalidades avançadas:**

- **Campos personalizados** - Crie atributos ilimitados
- **Empresas/Organizações** - Agrupe contatos por empresa
- **Busca por empresa** - Encontre contatos pelo nome da empresa/organização
- **Relacionamentos** - Conecte contatos relacionados
- **Scoring de leads** - Priorize contatos por valor
- **Segmentação** - Crie segmentos dinâmicos
- **Scroll infinito** - Carregamento automático de mais contatos ao rolar
- **Paginação inteligente** - Indicador de mais resultados disponíveis

---

## 📢 Campanhas em Massa

Sistema completo de campanhas para comunicação proativa com clientes através de múltiplos canais.

### Tipos de Campanhas

#### Campanhas Ongoing (Chat ao Vivo)

Mensagens proativas para visitantes do seu site:

- **Triggers por URL** - Ative campanhas em páginas específicas
- **Triggers por tempo** - Mostre mensagem após X segundos na página
- **Triggers por eventos** - Ative conforme comportamento do usuário
- **Horário comercial** - Só dispara durante horário de trabalho
- **Habilitar/desabilitar** - Ative ou pause campanhas facilmente

#### Campanhas One-Off (Envio Único)

Envios em massa para uma audiência segmentada:

- **WhatsApp** - Campanhas via WhatsApp Business
- **SMS (Twilio)** - Mensagens de texto em massa
- **SMS (Bandwidth/outros)** - Provedores SMS alternativos
- **Canal de API** - Campanhas através de canais personalizados

### Audiência e Segmentação

**Seleção de contatos:**

- **Por contatos individuais** - Selecione contatos específicos
- **Por etiquetas** - Inclua todos os contatos com certas etiquetas
- **Combinação** - Misture contatos diretos e etiquetas
- **Deduplicação automática** - Evite duplicados por número de telefone

**Filtragem inteligente:**

- Exclui contatos sem número de telefone
- Deduplicação por telefone (pega o primeiro contato)
- Contador de audiência pré-envio

### Agendamento

- **Envio imediato** - Execute a campanha no momento
- **Envio agendado** - Agende para data e hora específica
- **Só em horário comercial** - Pausa envios fora do horário e retoma automaticamente
- **Fuso horário da caixa de entrada** - Respeita a configuração de cada inbox

### Conteúdo de Campanhas

**Mensagens de texto:**

- Mensagem personalizável com texto livre
- Suporte a emojis
- **Spintax** - Variações automáticas de texto usando sintaxe `{Olá|Bom dia} {amigo|parceiro}` para mensagens únicas por destinatário

**Arquivos anexos** *(Evolution/WAHA/Uazapi/API)*:

- Imagens (JPEG, PNG, WebP)
- Vídeos (MP4, 3GP)
- Documentos (PDF, Office, etc.)
- Múltiplos arquivos por campanha

**Templates de WhatsApp** *(Cloud API/Notificame)*:

- Templates aprovados pelo Meta
- Parâmetros dinâmicos por contato
- Componentes de header, body e buttons
- Multi-idioma

### Multi-Inbox (Rotação de Linhas) *(Mega)*

Envie campanhas de múltiplas linhas de WhatsApp para maximizar o alcance e evitar limites:

- **Distribuição automática** - As mensagens são distribuídas entre suas linhas
- **Rotação configurável** - Defina quantas mensagens enviar por cada linha antes de trocar
- **Evite bloqueios** - Ao distribuir a carga, você reduz o risco de limites por linha
- **Maior velocidade** - Envie mais mensagens em menos tempo usando várias linhas

### Controle de Velocidade *(Mega)*

Envio inteligente que protege suas linhas de WhatsApp:

- **Pausas automáticas** - O sistema faz pausas entre mensagens para simular envio humano
- **Velocidade adaptável** - Configuração otimizada conforme o provedor
- **Prevenção de bloqueios** - Evita que o WhatsApp detecte comportamento de spam
- **Sem configuração manual** - Valores ótimos pré-configurados

### Status de Campanha

| Status | Descrição |
| -------- | ----------- |
| **Active** | Campanha pronta para executar |
| **Running** | Campanha em execução |
| **Completed** | Campanha finalizada com sucesso |
| **Error** | Campanha com erros críticos |

### Métricas e Acompanhamento

Monitore o desempenho das suas campanhas em tempo real:

- **Contador de audiência** - Saiba a quantos contatos sua campanha vai chegar
- **Mensagens enviadas** - Acompanhamento em tempo real do progresso
- **Mensagens com falha** - Identifique problemas de entrega
- **Relatório de erros** - Baixe detalhes de envios com falha para correção

### Proteção Anti-Spam

O sistema inclui múltiplas proteções para manter a qualidade dos seus envios:

- **Sem duplicados** - Não envia duas vezes para o mesmo contato
- **Detecção automática** - Pula contatos que já receberam a campanha
- **Histórico de envios** - Cada mensagem fica vinculada à sua campanha

### Remetente e Conversas

- **Atribua um agente** - As respostas da campanha chegam ao agente selecionado
- **Reutilização inteligente** - Se já existe conversa com o contato, usa a mesma
- **Fechamento automático** - Opção de fechar a conversa após o envio

### Canais Suportados

| Canal | Tipo | Templates | Anexos | Multi-inbox |
| ------- | ------ | ----------- | -------- | ------------- |
| Website (Chat ao Vivo) | Ongoing | ❌ | ❌ | ❌ |
| WhatsApp Cloud | One-off | ✅ | ✅ (no template) | ✅ |
| WhatsApp Notificame | One-off | ✅ | ✅ (no template) | ✅ |
| WhatsApp Evolution | One-off | ❌ | ✅ | ✅ |
| WhatsApp WAHA | One-off | ❌ | ✅ | ✅ |
| WhatsApp Uazapi | One-off | ❌ | ✅ | ✅ |
| Twilio SMS | One-off | ❌ | ❌ | ❌ |
| SMS | One-off | ❌ | ❌ | ❌ |
| Canal de API | One-off | ❌ | ✅ | ✅ |

### Gestão de Campanhas

- **Criar e editar** - Interface intuitiva para configurar campanhas
- **Pausar e retomar** *(Mega)* - Pause uma campanha em execução e retome a qualquer momento sem perder o progresso
- **Editar antes de enviar** *(Mega)* - Modifique o conteúdo, audiência e configuração de campanhas que ainda não foram enviadas ou estão pausadas
- **Ver métricas** - Dashboard com estatísticas em tempo real
- **Exportar relatórios** - Baixe detalhes da campanha

### Métricas de Campanha

- **Contador de audiência** - Saiba quantos contatos a campanha vai atingir
- **Mensagens enviadas** - Acompanhamento do progresso em tempo real
- **Mensagens com falha** - Identifique problemas de entrega
- **Relatório de erros** - Baixe detalhes de envios com falha para correção
- **Progresso em tempo real** *(Mega)* - Barra de progresso ao vivo que se atualiza automaticamente enquanto a campanha é executada
- **ETA estimado** *(Mega)* - Tempo estimado de conclusão visível durante a execução da campanha

---

## 📚 Central de Ajuda (Help Center)

### Portais de Conhecimento

- **Múltiplos portais** - Crie bases de conhecimento por produto/marca
- **Domínio personalizado** - Hospede no seu próprio domínio
- **Design configurável** - Cores, logo, texto de cabeçalho
- **Integrações de análise** - Administradores podem conectar Google Analytics 4, Google Tag Manager, Microsoft Clarity, Hotjar, Plausible, Amplitude e Meta Pixel; os scripts são publicados apenas com um identificador válido
- **Layouts selecionáveis** - Escolha entre uma página inicial clássica ou navegação lateral em estilo documentação
- **Multi-idioma** - Artigos em múltiplos idiomas
- **Conteúdo recomendado por localidade** - Selecione e ordene até 3 categorias e 6 artigos em destaque por localidade; o conteúdo popular permanece como fallback quando nada é configurado
- **Embeds GuideJar** - Insira guias interativos do GuideJar no conteúdo da Central de Ajuda

### Organização de Conteúdo

- **Categorias** - Agrupe artigos por tema
- **Subpastas** - Organização hierárquica
- **Artigos** - Conteúdo rico com markdown
- **Criar a partir da categoria** - Inicie novos artigos diretamente da tela de cada categoria
- **Redimensionamento de imagens** - Ajuste imagens dentro do editor para layouts de artigo mais limpos
- **Menu slash no editor** - Insira blocos e comandos rapidamente digitando /
- **Menu slash seguro em tabelas** - Dentro das células, use apenas formatação inline preservada pelo Markdown, com navegação por setas e Ctrl+N/P contida no menu
- **Vídeos pelo menu slash** - Incorpore links de vídeo compatíveis (YouTube, Vimeo, Loom, Wistia, Arcade, Bunny, CodePen, GuideJar e MP4) ou envie um MP4 com progresso, cancelamento, nova tentativa e pré-visualização redimensionável no editor e no artigo publicado
- **Envios de mídia confiáveis** - As imagens aparecem no cursor enquanto são enviadas em segundo plano; envios com falha podem ser tentados novamente ou removidos sem perder o rascunho
- **Divisores pelo menu slash** - Insira um divisor horizontal pelo menu do editor para separar seções do artigo
- **Tabelas nativas no editor** - Crie e edite tabelas diretamente no editor de artigos
- **Tabelas em Markdown** - Renderização correta de tabelas dentro dos artigos
- **Posicionamento** - Ordene artigos manualmente
- **Reordenamento de categorias** - Arraste e solte para reordenar categorias do help center; a ordem é salva automaticamente

### Status de Artigos

- **Rascunho** - Em preparação
- **Publicado** - Visível para usuários
- **Arquivado** - Oculto mas preservado
- **Rascunho por idioma** - Cada tradução de um artigo pode estar em rascunho de forma independente; publique apenas os idiomas prontos sem afetar os demais
- **Edições não publicadas** - Alterações em um artigo publicado ficam em rascunho até serem revisadas e publicadas explicitamente; elas podem ser comparadas à versão visível ou descartadas

### SEO e Acesso

- **Meta descrições** - Otimize para buscadores
- **URLs amigáveis** - Slugs personalizáveis
- **Widget integrado** - Conecte portal com chat ao vivo

### Geração de Conteúdo com IA *(Enterprise)*

- **FAQs a partir de PDF** - Envie documentos PDF para gerar rascunhos de FAQ com IA
- **Contexto adicional** - Adicione instruções opcionais para orientar a geração do conteúdo
- **Publicação assistida** - Revise e publique apenas as entradas geradas que desejar manter

### Inserir Artigos nas Conversas

- **Busca de artigos** - Busque artigos a partir da caixa de resposta
- **Pré-visualização** - Visualize o artigo antes de inserir
- **Inserir como link** - Adicione o link do artigo à mensagem
- **Busca estável no popover** - Resultados restaurados e confiáveis no popover da conversa
- **Copiar link** - Copie a URL do artigo para a área de transferência
- **Acesso rápido** - Botão dedicado no painel de resposta

### Busca por Embeddings *(Enterprise)*

- **Busca semântica** - Encontre artigos por significado, não apenas palavras-chave
- **IA contextual** - Sugira artigos relevantes nas conversas

---

## 📊 Relatórios e Analytics

### Relatórios de Conversas

- **Volume** - Novas, resolvidas, pendentes
- **Tempo de resolução** - Média e distribuição
- **Primeira resposta** - Tempo de resposta inicial
- **Tendências** - Evolução temporal
- **Drilldown de barras** - Abra cada barra do gráfico para revisar as conversas ou mensagens que compõem a métrica, com navegação entre buckets e contagem de resultados

### Relatórios de Agentes

- **Produtividade individual** - Conversas gerenciadas
- **Tempo de resposta** - Por agente
- **Satisfação** - CSAT por agente
- **Disponibilidade** - Tempo online/offline

### Relatórios de Inbox

- **Comparativo de canais** - Desempenho por inbox
- **Distribuição de carga** - Equilíbrio entre inboxes
- **Horários de pico** - Identifique momentos de maior demanda

### Relatórios de Equipes

- **Performance por equipe** - Métricas de grupo
- **Distribuição** - Carga de trabalho entre equipes

### Relatórios de Etiquetas

- **Uso de etiquetas** - Frequência e tendências
- **Categorização** - Análise por classificação

### Pesquisas CSAT

- **Satisfação do cliente** - Pesquisas pós-conversa
- **Notas 1-5** - Escala de satisfação
- **Comentários** - Feedback qualitativo
- **Filtros** - Por agente, inbox, equipe, data
- **Notas de revisão** *(Enterprise)* - Adicione notas internas às respostas CSAT para acompanhamento de qualidade
- **CSAT via Templates WhatsApp** *(Mega)* - Envie pesquisas CSAT usando templates oficiais do WhatsApp em vez da mensagem clássica no chat; requer aprovação da Meta; o sistema cria e gerencia automaticamente o template com versionamento; configurável por inbox com alternância entre modo clássico e modo template
- **Visibilidade do feedback para agentes** *(Mega)* - Permite ocultar por inbox os comentários escritos de CSAT dos agentes mantendo as avaliações visíveis; os administradores conservam acesso completo e o padrão mantém a visibilidade atual

### Relatórios Resumidos

- **Métricas consolidadas** - Visão geral das métricas chave em um só lugar
- **Filtros por período** - Filtre por faixa de datas personalizada
- **Agrupamento** - Agrupe dados por agente, equipe ou inbox

### Exportação

- **CSV/Excel** - Baixe dados para análise externa
- **Filtros personalizados** - Exporte exatamente o que precisa
- **Compatibilidade regional de CSV** - Exportação com UTF-8 BOM e separador `;` para planilhas

### Relatórios de Bots *(Enterprise)*

Analytics completos de desempenho dos seus chatbots:

**Métricas de uso:**

- **Total de sessões** - Quantas conversas o bot gerenciou
- **Taxa de resolução** - Percentual de casos resolvidos sem humano
- **Tempo de resposta** - Velocidade média do bot
- **Mensagens processadas** - Volume total de interações

**Análise de handover:**

- **Taxa de transferência** - Quando o bot transfere para humanos
- **Motivos de transferência** - Por que os clientes precisam de humanos
- **Tempo até transferência** - Quanto tempo tentou resolver

**Métricas de satisfação:**

- **CSAT pós-bot** - Satisfação após interação com bot
- **Comparação bot vs humano** - Veja diferenças de qualidade

**Insights por bot:**

- **Por caixa de entrada** - Desempenho por canal
- **Por tipo de bot** - Compare agentbots vs Captain
- **Tendências temporais** - Evolução de métricas

### Relatórios de Chamadas *(Enterprise)*

Analytics completos do canal de voz:

**Métricas de volume:**

- **Total de chamadas** - Entrada e saída
- **Taxa de atendimento** - Percentual de chamadas atendidas
- **Chamadas perdidas** - Identificar horas de pico sem cobertura
- **Distribuição horária** - Quando mais ligam

**Métricas de desempenho:**

- **Duração média** - Tempo médio de chamada
- **Tempo de espera** - Quanto o cliente espera antes de ser atendido
- **Taxa de abandono** - Clientes que desligam esperando

**Análise por agente:**

- **Chamadas por agente** - Distribuição de carga
- **Duração por agente** - Tempo médio de cada agente
- **Taxa de resolução** - Efetividade por agente

**Exportação:**

- **Relatórios detalhados** - Baixe registros de chamadas
- **Gravações** - Acesse gravações para revisão de qualidade

---

## 👨‍👩‍👧‍👦 Gestão de Equipes

### Agentes

- **Funções** - Administrador, Agente
- **Permissões granulares** - Controle de acesso por funcionalidade
- **Perfil personalizado** - Avatar, nome, assinatura
- **Avatar específico por conta** - Um usuário compartilhado mantém um único seletor enquanto cada conta armazena e exibe sua própria foto de perfil
- **Sessões de navegador nomeadas** - Agentes podem rotular sessões ativas para reconhecer estações, perfis de navegador ou contextos de teste
- **Controle confiável de sessões do navegador** - As abas de um perfil compartilham uma sessão lógica; sair remove essa sessão, enquanto outro navegador, perfil ou janela privada usa uma vaga diferente. O login só é interrompido quando um novo navegador atinge o limite configurado
- **Status de disponibilidade** - Online, Ocupado, Offline
- **Desligamento guiado de agentes** - Antes de remover um agente, escolha entre deixar as conversas sem atribuição ou reatribuir em lote
- **Convites protegidos** - Convites para novos agentes respeitam o limite diário de e-mails da conta sem bloquear a inclusão de usuários existentes

### Equipes

- **Departamentos** - Vendas, Suporte, Faturamento, etc.
- **Atribuição automática** - Round-robin dentro da equipe
- **Restrição de visibilidade** - Membros veem apenas suas conversas
- **Identificação visual** - Configure um emoji ou ícone com cor por equipe para reconhecê-la em listas e seletores de atribuição

### Inboxes e Membros

- **Acesso por inbox** - Atribua agentes a canais específicos
- **Limite de capacidade** - Máximo de conversas por agente
- **Políticas de atribuição** - Configure regras de distribuição

### Políticas de Atribuição *(Enterprise)*

Sistemas avançados para distribuir conversas de forma justa e eficiente:

**Tipos de política:**

- **Round Robin** - Rotação entre agentes disponíveis
- **Distribuição Justa** - Considera carga atual de cada agente
- **Auto-atribuição** - Agentes escolhem quais conversas aceitar

**Regras de atribuição:**

- **Por caixa de entrada** - Cada inbox pode ter sua própria política
- **Por equipe** - Configure regras diferentes por departamento
- **Limites de capacidade** - Respeita o máximo de conversas por agente

**Lógica inteligente:**

- **Só agentes disponíveis** - Só atribui para quem está online
- **Peso de agentes** - Alguns agentes podem receber mais que outros
- **Rebalanceamento** - Redistribui quando agentes ficam sobrecarregados

### Política de Capacidade de Agente *(Enterprise)*

Controle avançado da carga de trabalho:

**Configuração de capacidade:**

- **Limite por agente** - Máximo de conversas ativas por agente
- **Limite por conta** - Máximo total de conversas por conta
- **Por caixa de entrada** - Limites diferentes por canal

**Tipos de conversa:**

- **Abertas contam** - Conversas ativas consomem capacidade
- **Pendentes contam** - Configurável se pendentes consomem capacidade
- **Adiadas não contam** - Conversas adiadas liberam capacidade

**Comportamento quando cheio:**

- **Fila de espera** - Novas conversas aguardam em fila
- **Não atribuir** - Ficam sem agente até liberar capacidade
- **Reatribuição automática** - Move para outro agente com capacidade

### Funções Personalizadas *(Enterprise)*

- **Permissões sob medida** - Crie funções com permissões específicas
- **Gestão de conversas** - Todas, não atribuídas, ou apenas participando
- **Acesso a funcionalidades** - Contatos, empresas, relatórios, campanhas, etc.
- **Permissões de CSAT** - Controle quais funções podem visualizar e gerenciar pesquisas de satisfação

### Horários de Trabalho

- **Disponibilidade por inbox** - Defina horários de atendimento
- **Fusos horários** - Suporte multi-região
- **Mensagens fora do horário** - Respostas automáticas
- **Pausa para almoço** - Configure intervalos de descanso dentro do horário comercial
- **Horários por dia** - Defina horários diferentes para cada dia da semana

### Web Push operacional

- **Entrega com a página fechada** - Lembretes do Calendário, atribuições em notas do Kanban, automações de etapa, vencimentos de checklist e Tarefas podem chegar a navegadores inscritos mesmo com o dashboard fechado
- **Navegação direta** - As ações da notificação abrem o evento, item do Kanban ou Tarefa exata que originou o alerta
- **Controle do canal** - Os agentes configuram essas categorias operacionais somente para Push; os popups em primeiro plano continuam disponíveis quando o MEGA está aberto

### Configuração de Notificações

Cada agente pode personalizar exatamente quando e como receber alertas:

**Tipos de notificação:**

- Nova conversa criada
- Conversa atribuída a você
- Nova mensagem nas suas conversas
- Quando te mencionam numa conversa
- Mensagens em conversas onde participa

**Canais de notificação:**

- **Email** - Receba alertas no seu email
- **Push** - Notificações instantâneas no navegador ou app móvel
- **Personalização total** - Escolha que tipo de alerta receber por cada canal

### Adiamento de Notificações (Notification Snooze)

Pause notificações temporariamente para conversas específicas:

- **Opções de snooze** - 1 hora, 3 horas, 1 dia, 1 semana, ou tempo personalizado
- **Reabertura automática** - Notificação reativa após período de snooze
- **Acesso via command bar** - Adie rapidamente via atalho de teclado
- **Por notificação** - Adie notificações individuais sem afetar outras
- **Indicador visual** - Veja quando uma notificação está adiada

---

## 🔌 Integrações

### Webhooks

Conecte a MEGA com qualquer sistema externo através de notificações automáticas:

> **Disponibilidade:** A entrega de Webhooks de saída exige acesso a API e Webhooks para a conta em planos hospedados. Ela continua disponível em instalações autogerenciadas.

- **Eventos em tempo real** - Receba alertas instantâneos quando algo acontece
- **Integração com seu CRM** - Sincronize dados automaticamente
- **Automações externas** - Acione fluxos em outras ferramentas
- **Flexibilidade total** - Configure quais eventos te interessam
- **Normalização de inscrições** - Validação e normalização consistentes de eventos e aliases
- **Payload enriquecido de anexos** - Inclui `content_type` e extensão dos arquivos em eventos webhook
- **Evento de atualização de Agent Bot** - Dispara webhook quando uma conversa gerenciada por bot é atualizada
- **Evento `inbox_updated`** - Notifica mudanças relevantes da inbox, incluindo desconexões do canal
- **Aliases de inscrição** - Atribua nomes descritivos a cada inscrição de webhook para facilitar o gerenciamento
- **Segredo global de webhook** *(Enterprise)* - Configure uma assinatura de segurança no nível da instalação para verificar a autenticidade de todos os eventos webhook; os payloads são assinados com HMAC-SHA256 usando o segredo configurado

### Tarefas *(Mega)*

Planeje e acompanhe o trabalho interno em visualizações compartilhadas de calendário e lista:

- **Ativação controlada** - Superadministradores habilitam o recurso da conta e administradores conectam Tarefas em Configurações -> Integrações
- **Tipos personalizados** - Administradores definem categorias reutilizáveis e cores semânticas para o trabalho da equipe
- **Paleta consistente** - Os tipos usam a mesma paleta visual de 22 cores do Google Agenda e mantêm a cor escolhida no calendário, detalhes e listas, sem que o status a substitua
- **Permissões por escopo** - Administradores controlam todas as tarefas; roles personalizadas podem receber separadamente gestão das próprias/atribuídas, leitura global e relatórios; agentes padrão só veem e gerenciam tarefas criadas por eles ou atribuídas a eles
- **Visualizações de calendário e lista** - Alterne entre o calendário mensal e uma lista operacional persistente com tarefa, tipo, responsável, datas, prioridade e status; ambas abrem o mesmo detalhe
- **Filtros operacionais** - Busque por título, filtre por responsável —inclusive sem responsável—, tipo e hoje, esta semana ou próximos 30 dias; um único seletor de status começa em Todas as tarefas e oferece pendentes, em andamento, vencidas, concluídas ou canceladas; ordene e agrupe a lista por status, responsável ou vencimento
- **Tarefas de vários dias** - Uma tarefa aparece em cada dia do calendário que intersecta sua programação, inclusive quando começou antes do mês visível
- **Experiência mobile** - Em telas pequenas, os filtros se reorganizam sem comprimir o calendário mensal; formulários e detalhes mantêm as ações visíveis sem cobrir o conteúdo
- **Leitura antes de editar** - Ao abrir uma tarefa, seus detalhes são exibidos; concluir e cancelar ficam no cabeçalho com resumo obrigatório, enquanto editar e, somente para administradores, excluir com confirmação ficam no rodapé
- **Responsabilidade clara** - Atribua uma tarefa a um agente da conta ou deixe-a sem responsável
- **Histórico resiliente** - Excluir contato, conversa, item Kanban ou responsável preserva seus rótulos históricos, limpa referências ativas e resincroniza a projeção Google sem duplicar a cascata de exclusão
- **Estados operacionais** - Gerencie tarefas pendentes, em andamento, concluídas ou canceladas; vencimentos são detectados automaticamente após o prazo
- **Encerramento documentado** - Concluir ou cancelar exige um resumo do resultado para registrar o que ocorreu e os próximos passos
- **Aviso ao responsável** - Ao atingir o prazo, somente o agente responsável recebe um popup e uma notificação para abrir, concluir, cancelar ou editar a tarefa; ele pode marcar o aviso como visto ou adiá-lo para reaparecer automaticamente, e tarefas sem responsável não geram aviso
- **Tarefas recorrentes** - Repita tarefas por dia, semana, mês ou ano, com intervalo, dias semanais e término por data ou até 100 repetições
- **Contexto conectado** - Vincule opcionalmente contato e conversa, ou crie um item em um funil e etapa sem exigir cliente
- **Criação a partir de conversas** - O ReplyBox mostra uma ação ao lado do calendário quando Tarefas está habilitada e conectada; abre o formulário com contato, conversa, responsável atual e qualquer item Kanban relacionado preenchidos
- **Acompanhamento por contato** - O ContactPanel inclui um acordeão próprio de Tarefas no formato do calendário, identifica cada conversa vinculada pelo número visível estável e mantém tarefas pendentes, em andamento e vencidas do contato visíveis em novas conversas
- **Kanban condicionado** - O vínculo e a criação de itens Kanban aparecem somente quando `kanban_board` está habilitado na conta
- **Tarefas dentro do item** - Quando Tarefas está habilitada e conectada, o detalhe Kanban separa o histórico técnico de uma aba operacional para criar, consultar e abrir tarefas vinculadas ao item
- **Rastreabilidade no Kanban** - O histórico do item registra quando uma tarefa vinculada é criada, atualizada, iniciada, concluída, cancelada, reaberta, vinculada, desvinculada ou excluída, incluindo status e responsável
- **Participantes e prioridade** - Defina prioridade, responsável, participantes da conta e convidados externos
- **Google Agenda opcional** - Sincronize início, fim e participantes em um único evento, preservando a tarefa local em caso de falha
- **Relatórios de tarefas** - Administradores e roles personalizadas com a permissão específica de relatórios de tarefas acompanham data, responsável, tipo e status; a permissão geral de relatórios não concede esse acesso
- **API para desenvolvedores** - Use os CRUDs de Tarefas e Tipos de tarefa com escopo de conta pelo Swagger/OpenAPI ou pela coleção Postman gerada, incluindo busca, interseção de intervalo, ordenação, paginação opcional e campos de workflows vinculados

### Google Agenda *(Mega)*

- **Lembretes pessoais** - O criador recebe um aviso no MEGA e por push do navegador, pode adiá-lo com intervalos predefinidos e reabrir o diálogo compartilhado. Novos eventos incluem como convidados, sem duplicação, o criador e o contato quando nascem de uma conversa.

Conecte o Google Agenda como integracao de produtividade no nivel da conta, nao como inbox/canal:

- **OAuth por conta** - Administradores conectam o calendario em Configuracoes -> Integracoes -> Google Agenda
- **Acesso por função personalizada** - Administradores podem conceder a um agente atribuído a permissão “Acessar Calendário” para Calendário, ReplyBox e ContactPanel
- **Disponibilidade condicionada** - O espaço `/calendar`, o ícone do compositor e os eventos do painel da conversa só aparecem quando a conta está conectada com um calendário selecionado; os controles de sincronização Kanban exigem a mesma configuração da conta
- **Criacao minimalista** - Use um editor de duas colunas inspirado no Google Agenda com fusos selecionaveis, convidados removiveis, Google Meet e contexto com a marca da instalação visivel na busca de conversas
- **Selecao de calendario** - Importe por padrao todos os calendarios acessiveis ou limite a entrada a um; o MEGA preserva um destino de saida concreto e novas configuracoes iniciam com sync bidirecional
- **Camada interna de eventos** - O MEGA salva eventos internos e rastreia IDs externos do Google separadamente
- **Calendario operacional do MEGA** - Agentes gerenciam visoes de dia, semana, mes e lista em `/calendar`; a visao mensal limita os eventos visiveis por dia e oferece `+N mais` ou menu contextual para abrir acoes sem ocultar eventos. Os eventos aceitam cores e a exclusao permanente, restrita a administradores, tambem remove o evento vinculado do Google
- **Formulario completo de evento** - Eventos manuais suportam fuso horario, local, convidados, lembretes, recorrencia simples, disponibilidade, visibilidade e Google Meet
- **Vinculos MEGA buscaveis** - Ao criar ou editar eventos, agentes buscam e selecionam contato, conversa e item Kanban sem digitar IDs internos
- **Controles por modulo** - Habilite sincronizacao para calendario interno, Kanban, conversas e lembretes em um so lugar
- **Sync ao salvar** - Quando a sincronizacao de saida esta habilitada, o MEGA cria ou atualiza o evento no calendario Google selecionado preservando o estado interno
- **Polling automatico do Google** - A cada cinco minutos o MEGA importa somente eventos alterados desde o ultimo poll bem-sucedido de cada calendario; `/calendar` le dados locais e mantem sync manual como fallback
- **Estado da conexao** - Veja a identidade conectada, reconecte quando necessario e desconecte sem apagar eventos internos
- **Sincronizacao de exclusoes** - Quando o Google informa que um evento sincronizado foi excluido, o MEGA remove automaticamente a entrada local vinculada; tarefas e itens Kanban relacionados sao preservados
- **Ponte com Kanban** - Itens com data programada ou deadline podem criar eventos internos e sincronizar com o calendario selecionado
- **Agenda e envio em conversas** - Os agentes usam no compositor o mesmo formulário com recursos do Google, contato e conversa preenchidos, e o botão “Criar e enviar” compartilha horário, local, detalhes e link do Google Meet gerado
- **Acompanhamento em conversas** - O painel mostra eventos vinculados com ponto pulsante verde (<50%), amarelo (50–90%) ou vermelho (≥90%) conforme o avanço de Início a Fim, deixa vencidos opacos e reabre o editor compartilhado
- **Importacao e backfill** - Administradores podem importar eventos do Google e migrar IDs legados do Kanban para o modelo global de calendario

### Construtor de Templates Meta *(Mega)*

Crie e gerencie seus templates do WhatsApp diretamente da MEGA, sem precisar acessar o Meta Business Manager:

**Gestão de templates:**

- **Lista centralizada** - Veja todos os templates de todas as suas caixas de entrada do WhatsApp em um só lugar
- **API unificada de templates em cache** - Integrações podem listar templates em cache de inboxes WhatsApp nativos e Twilio, filtrar pelo nome exato do provedor e consultar a última tentativa de sincronização sem contatar o provedor
- **Status de aprovação** - Monitore se cada template está aprovado, pendente ou rejeitado pela Meta
- **Métricas de uso** - Veja quantas vezes cada template foi entregue e sua taxa de leitura
- **Filtros avançados** - Filtre por status, categoria, idioma, canal e intervalo de datas
- **Busca** - Encontre templates rapidamente por nome ou conteúdo
- **Excluir templates** - Exclua templates individuais ou em lote com confirmação
- **Sincronizar templates** - Botão de sincronização para trazer novos templates da Meta
- **Sincronização inicial automática** - Ao criar o canal, uma sincronização inicial de templates é executada
- **Prevenção de duplicados** - Validações de inserção para evitar duplicados durante sincronização
- **Tabela responsiva** - Melhor visualização de metadados de templates em desktop e mobile

**Construtor visual:**

- **Criação passo a passo** - Fluxo guiado: Informações Básicas → Construtor
- **Cabeçalho opcional** - Cabeçalho de texto ou multimídia (imagem, vídeo, documento)
- **Corpo da mensagem** - Editor com negrito *texto*, itálico *texto*, variáveis {{1}}, {{2}}
- **Barra de formatação** - Botões de formato e inserção de variáveis com um clique
- **Rodapé opcional** - Texto de rodapé (até 60 caracteres)
- **Botões de ação** - Visitar site, ligar, resposta rápida ou copiar código
- **Pré-visualização em tempo real** - Veja como o template ficará antes de enviar
- **Valores de exemplo** - Defina exemplos para variáveis para facilitar a aprovação da Meta
- **Categorias** - Marketing, Utilidade, Autenticação
- **Multi-idioma** - Crie templates em qualquer idioma suportado pelo WhatsApp

**Edição de templates:**

- **Visualização detalhada** - Consulte a estrutura completa do template antes de editar
- **Upload de mídia otimizado** - Melhorias no envio de arquivos multimídia para edição/envio

### Apps de Dashboard

Estenda a plataforma com apps personalizados exibidos na interface de conversa:

**Tipos de apps:**

- **Panel de conversa** - Apps na barra lateral da conversa
- **Panel de contato** - Apps no perfil do contato
- **Background** - Apps que rodam sem interface visível

**Funcionalidades:**

- **iFrames personalizados** - Incorpore apps externos nas conversas
- **Contexto dinâmico** - Passe informações da conversa para o app
- **SDK JavaScript** - Interaja com dados da MEGA
- **Eventos em tempo real** - Reaja a mudanças na conversa
- **Scripts de dashboard (Super Admin)** *(Mega)* - Publique personalizações globais sem alterar o código base
- **Preview seguro e ativação por script** *(Mega)* - Teste alterações com segurança e ative/desative scripts de forma independente

**Casos de uso:**

- Mostrar dados de CRM externos
- Calculadoras ou ferramentas internas
- Integração com sistemas legados
- Formulários personalizados para agentes

### Platform Apps (Developer API)

APIs para desenvolvedores criarem integrações avançadas:

**Tipos de integração:**

- **Inbox Apps** - Crie canais personalizados
- **Bots** - Automatize com webhooks de bot
- **Dashboard Apps** - Estenda a interface
- **Gestão administrativa** - Os Dashboard Apps de toda a conta só podem ser criados, atualizados e excluídos por administradores; agentes autenticados mantêm acesso de leitura

**Recursos de API:**

- **API REST completa** - Acesso a todas as entidades
- **Webhooks** - Receba eventos em tempo real
- **SDKs** - Node.js e outras linguagens
- **Documentação** - Referência completa de API

### Templates de Email

Personalize emails transacionais e de notificação:

**Funcionalidades:**

- **Editor de templates** - Modifique o conteúdo e design
- **Variáveis dinâmicas** - Insira dados do contato e conversa
- **Preview** - Veja como fica antes de salvar
- **Multi-idioma** - Templates diferentes por idioma
- **Layouts de resposta com marca** - Administradores podem configurar um HTML Liquid de fallback por conta e uma substituição por caixa de Email; o layout deve incluir `{{ content_for_layout }}` e aceita até 262.144 caracteres.

**Tipos de email:**

- Notificação de nova mensagem
- Resumo de conversa
- Convite para agentes
- Emails de campanha

### Slack

Gerencie conversas de clientes diretamente do Slack, sem trocar de ferramenta:

- **Sincronização automática** - As conversas aparecem em canais do Slack
- **Responda do Slack** - Responda a clientes sem abrir a MEGA
- **Somente alertas** - Mantenha os tópicos do Slack para discussão interna sem enviar respostas ao cliente
- **Notas privadas** - Comunique-se com sua equipe sem o cliente ver
- **Vinculação de perfis** - Conecte usuários do Slack com agentes da MEGA
- **Canais privados** - Organize por equipe ou tipo de conversa
- **Alertas de reconexão** - Aviso se a integração precisa de renovação

### Dialogflow

- **Bot de NLU** - Conecte com agentes do Dialogflow
- **Intents e entidades** - Processamento de linguagem natural

### OpenAI / GPT

Funcionalidades de IA avançada com modelos GPT:

- **Assistente de escrita** - Melhore e corrija suas respostas
- **Resumo de conversa** - Gere resumos automáticos
- **Tradução automática** - Traduza mensagens para qualquer idioma
- **Tom de resposta** - Ajuste o tom (formal, amigável, etc.)
- **Expansão de texto** - Desenvolva ideias curtas em respostas completas
- **Simplificação** - Simplifique textos complexos

### Dyte (Chamadas de Vídeo)

Videochamadas integradas diretamente na conversa:

- **Criar reunião** - Inicie uma videochamada com um clique
- **Entrar na reunião** - Clientes podem entrar pelo widget
- **Botão na caixa de resposta** - Acesso rápido da caixa de resposta
- **Tipo de mensagem de vídeo** - As chamadas aparecem na timeline

### Google Translate

Tradução automática de mensagens nas conversas:

- **Tradução automática** - Traduza mensagens recebidas para seu idioma configurado
- **Detecção de idioma** - Identifica automaticamente o idioma da mensagem
- **Tradução em contexto** - As mensagens traduzidas são exibidas inline na conversa
- **Suporte multi-idioma** - Compatível com todos os idiomas do Google Translate

### Linear *(Enterprise)*

- **Gestão de tickets** - Crie issues a partir de conversas
- **Sincronização** - Mantenha status atualizados

### Shopify *(Enterprise)*

- **Dados do cliente** - Visualize histórico de compras
- **Pedidos recentes** - Contexto de e-commerce

### WooCommerce *(Enterprise/Mega)*

Integração completa com WooCommerce:

- **Conexão de loja** - Vincule sua loja WooCommerce
- **Histórico de pedidos** - Veja pedidos do cliente em contexto
- **Busca por email/telefone** - Encontre pedidos automaticamente
- **Webhooks do WooCommerce** - Receba eventos da loja
- **Painel de pedidos** - Visualização de pedidos na conversa

### Notion *(Enterprise)*

- **Documentação** - Conecte páginas do Notion
- **Base de conhecimento** - Acesso rápido a recursos

### CRM (LeadSquared)

- **Sincronização de leads** - Envie contatos para seu CRM
- **Histórico unificado** - Visão 360 do cliente

---

## 💎 Funcionalidades Enterprise

### SLA (Acordos de Nível de Serviço)

- **Políticas configuráveis** - Defina tempos alvo
- **Primeira resposta** - Tempo máximo para responder; seu relógio ativo termina após a primeira resposta do agente e os descumprimentos permanecem nos relatórios de SLA
- **Próxima resposta** - Tempo entre respostas
- **Resolução** - Tempo total de atendimento
- **Descumprimentos congelados** - Ao resolver uma conversa, a duração do descumprimento é registrada e deixa de aumentar
- **Horário comercial** - Prazos calculados no backend respeitando o horário útil do inbox
- **Contatos bloqueados** - Conversas com contatos bloqueados ficam fora de atribuição, processamento, relatórios e indicadores de SLA até serem desbloqueadas
- **Alertas e notificações** - Aviso antes de descumprir
- **Relatórios de SLA** - Cumprimento e tendências

### Logs de Auditoria

- **Registro completo** - Toda ação fica registrada
- **Quem, o quê, quando** - Rastreabilidade total
- **Conformidade** - Para requisitos regulatórios
- **Localização rápida de eventos** - Filtre por tipo de evento e intervalo de dias completos, busque pelo nome ou e-mail do usuário que realizou a ação e ordene por data; os filtros podem ser compartilhados pela URL
- **Evidências de exclusão (Super Admin)** *(Mega)* - Um relatório somente leitura filtra por conta as auditorias retidas de destruição de caixas de entrada, conversas e contatos, exibindo data, captura do objeto, responsável/IP quando registrados e a limitação explícita de que a ausência de auditorias de Message não comprova uma contagem de mensagens excluídas

### SAML/SSO

Single Sign-On empresarial para autenticação centralizada:

**Provedores suportados:**

- **Okta** - Integração completa com Okta
- **Azure AD** - Microsoft Entra ID
- **Google Workspace** - Google como provedor de identidade
- **OneLogin** - Suporte completo
- **Auth0** - Integração disponível
- **SAML 2.0 genérico** - Qualquer provedor compatível

**Funcionalidades:**

- **Provisionamento automático** - Crie usuários automaticamente no primeiro login
- **Isolamento por conta** - Não permite convites nem autenticação SAML para usuários associados a outra conta
- **Mapeamento de grupos** - Sincronize grupos/equipes do IdP
- **Força SSO** - Exija SSO para todos os usuários da conta
- **Múltiplos domínios** - Configure SSO para diferentes domínios de email
- **Logout único** - Single Logout (SLO) suportado

**Segurança:**

- **Autenticação centralizada** - Gestão de acesso unificada
- **Políticas de senha no IdP** - Use as regras de senha corporativas
- **MFA no IdP** - Multi-factor authentication do provedor
- **Revogação instantânea** - Remova acesso desativando no IdP

### Retrospectiva Anual (Year in Review)

Resumo visual do ano da sua equipe de atendimento:

**Métricas apresentadas:**

- **Volume de conversas** - Total gerenciado no ano
- **Tempo de resposta** - Média de velocidade de resposta
- **Satisfação** - Pontuação CSAT do ano
- **Agentes destaque** - Reconhecimento de top performers

**Funcionalidades:**

- **Visualização interativa** - Interface visual atraente
- **Comparação anual** - Evolução em relação ao ano anterior
- **Compartilhável** - Exporte para apresentar à equipe
- **Por equipe** - Veja métricas de departamentos específicos

### Atribuição Avançada (V2)

- **Capacidade por agente** - Limites dinâmicos
- **Balanceamento inteligente** - Distribuição ótima de carga
- **Regras complexas** - Lógica de atribuição personalizada

### Busca Avançada

- **Indexação completa** - Busca em todas as mensagens
- **Resultados com transcrições** - Encontre áudios transcritos nos resultados de mensagens e sua conversa associada
- **Filtros combinados** - Múltiplos critérios simultâneos
- **Resultados instantâneos** - Performance otimizada

### Atributos Obrigatórios de Conversa

Obrigue os agentes a preencher atributos específicos antes de resolver conversas:

- **Campos obrigatórios** - Defina quais atributos personalizados devem ser preenchidos
- **Validação ao resolver** - Bloqueia a resolução até completar os campos obrigatórios
- **Macros seguras** - Macros que resolvem solicitam os atributos obrigatórios; se forem ignorados, executam as demais ações, mas mantêm a conversa aberta
- **Melhoria na qualidade dos dados** - Garanta que toda conversa tenha as informações necessárias

### Conferências de Voz

Conferências de chamadas de voz entre agentes e clientes:

- **Chamadas múltiplas** - Conecte vários participantes em uma única chamada
- **Gestão de conferência** - Controles completos da conferência
- **Integrado nas conversas** - As conferências são associadas a conversas existentes

### Marca Personalizada (Custom Branding)

Personalize completamente a aparência da sua plataforma:

- **Logo personalizado** - Seu logo em vez do logotipo padrão da plataforma
- **Logo modo escuro** - Logo específico para dark mode
- **Logo thumbnail** - Imagem quadrada do aplicativo para favicon, ícone PWA instalável e splash, com fallback para o ícone de notificações
- **Ícone de notificações** - Imagem quadrada independente para alertas Push do sistema, badges e o indicador temporário da aba oculta; usa `/favicon-badge-16x16.png` por padrão e o logo thumbnail como fallback
- **Nome da marca** - Mude o nome exibido em toda a plataforma
- **Nome da instalação** - Nome para a instância específica
- **Cor primária** - Defina sua cor corporativa principal
- **Fundo do ícone PWA** - Configure a cor de fundo do ícone instalável sem recompilar a imagem
- **URL da marca** - Link da sua empresa
- **URL do widget** - Link no widget de chat
- **Termos e privacidade** - URLs personalizadas para páginas legais
- **Meta descrição** - SEO personalizado para sua instalação

### Desabilitar Branding

- **Widget sem marca** - Remove a atribuição da plataforma do chat ao vivo
- **Emails sem marca** - Emails enviados sem branding da plataforma
- **Portais limpos** - Help Center sem referências à plataforma

### Funções Personalizadas

Crie funções sob medida para sua organização com controle granular de permissões:

**Controle o acesso a:**

- **Conversas** - Quem pode ver e gerenciar quais conversas
- **Contatos** - Acesso a dados de clientes
- **Empresas** - Acesso ao menu Empresas e aos registros de empresa
- **Relatórios** - Quem vê as estatísticas
- **Campanhas** - Permissões para criar e enviar campanhas
- **Central de Ajuda** - Gestão de artigos e portais
- **Dados sensíveis** - Controle sobre números de telefone visíveis

**Exemplos de funções:**

- **Supervisor** - Vê relatórios e métricas sem editar configuração
- **Agente Sênior** - Pode pegar conversas não atribuídas
- **Agente Básico** - Só trabalha com suas conversas atribuídas
- **Analista** - Acesso exclusivo a relatórios e estatísticas
- **Community Manager** - Gerencia campanhas e conteúdo do Help Center

---

## ⭐ Funcionalidades Exclusivas Mega

### 🧭 Onboarding Guiado

- **Configuração inicial dedicada** - Complete os dados da conta por um fluxo administrativo específico
- **URL do site normalizada** - Salve o endereço com protocolo para integrações e automações posteriores
- **Conexão guiada do Instagram** - Retome a configuração da caixa de entrada após autorizar o Instagram pelo onboarding

### 📅 Mensagens Programadas

Programe o envio automático de mensagens nas suas conversas:

- **Programação flexível** - Escolha data e hora exata para enviar a mensagem
- **Recorrência** - Programe mensagens recorrentes: diário, semanal, mensal ou anual
- **Templates** - Use templates de mensagens predefinidos para envios programados
- **Anexos** - Inclua imagens, documentos e arquivos em mensagens programadas
- **Status de acompanhamento** - Monitore o status: pendente, enviado, falhou, cancelado
- **Cancelamento** - Cancele mensagens programadas antes de serem enviadas
- **Recuperação e novo envio** - Tente novamente ou reagende uma mensagem com falha, ou programe uma cópia editável de uma mensagem enviada preservando destinatário e anexos
- **API de programação universal** - Programe uma mensagem para telefone, e-mail ou identificador de provedor criando ou reutilizando o contato automaticamente
- **Múltiplas por conversa** - Programe várias mensagens na mesma conversa
- **Histórico** - Consulte o histórico de mensagens programadas e seu status

### 🔒 Placeholder de Mensagem Excluída

Configure por inbox se os agentes veem o texto original e os anexos junto ao aviso de exclusão:

- **Retenção para agentes** - Pode mostrar o texto original e os anexos abaixo de "Esta mensagem foi excluída" dentro do dashboard
- **Configurável por inbox** - Cada canal pode ter sua própria configuração
- **Proteção do contato** - A API pública e os eventos em tempo real destinados ao contato entregam apenas o aviso de exclusão, sem metadados nem URLs de anexos

### Provedores de WhatsApp Alternativos

A MEGA inclui múltiplos provedores de WhatsApp além da API oficial do Meta, permitindo flexibilidade em custos, funcionalidades e casos de uso.

**Gestão multi-servidor (Mega):**

- **Múltiplos servidores por provedor** - Configure mais de um servidor por canal para continuidade operacional
- **Capacidade configurável** - Defina limites por servidor para distribuir volume de mensagens
- **Edição parcial de servidores legados** - Ajuste configurações existentes sem recriar a conexão completa
- **Visibilidade do servidor atribuído** - Identifique rapidamente qual servidor está vinculado a cada inbox

---

### 📱 WhatsApp Evolution

Conexão direta ao WhatsApp sem necessidade de API oficial, ideal para empresas que buscam flexibilidade e economia.

**Vantagens principais:**

- **Conexão por QR** - Vincule seu WhatsApp em segundos escaneando um código
- **Sem templates obrigatórios** - Envie mensagens livremente sem aprovações
- **Sem janela de 24 horas** - Inicie conversas quando quiser
- **Sem custo por mensagem** - Evite as taxas da API oficial do Meta

**Todo tipo de conteúdo:**

- Textos, imagens, vídeos, documentos
- Áudio e notas de voz
- Stickers
- Suporte a grupos de WhatsApp

**Ideal para:**

- Empresas que buscam reduzir custos
- Operações que precisam de flexibilidade em mensagens
- Equipes que já usam WhatsApp pessoal ou business app

---

### 📱 WhatsApp WAHA

Solução robusta e de alta disponibilidade para operações exigentes que requerem máxima estabilidade.

**Vantagens principais:**

- **Alta disponibilidade** - Projetado para produção com reconexão automática
- **Múltiplos números** - Gerencie várias linhas em uma instalação
- **Muito estável** - Ideal para operações 24/7

**Conteúdo multimídia completo:**

- Textos, imagens, vídeos, documentos
- Áudio e notas de voz
- Stickers e reações, incluindo envio de reações com token de API
- Suporte completo a grupos

**Funções avançadas:**

- Status de presença (digitando, online)
- Confirmações de leitura
- Mensagens editadas e excluídas
- Autorização com passkey durante a vinculação do WhatsApp pelo fluxo da extensão de navegador do WAHA, com estados de sessão dedicados, aviso preventivo quando a extensão não está instalada e confirmação manual por código quando o WhatsApp solicitar
- Sincronização global e por conversa sob demanda de mensagens recentes, com proteção de concorrência por conta e processamento dedicado opcional para instalações de alto volume
- Download diferido de mídia de grupos WAHA (lazy media) opcional por caixa: a mídia recebida em grupos é salva como anexo pendente com um placeholder genérico e só é baixada quando um agente solicita na conversa; conversas individuais mantêm o download imediato
- Proxy por sessão com servidor `host:porta` e credenciais opcionais, que pode ser removido para voltar à conexão direta

**Ideal para:**

- Operações de alto volume
- Empresas que precisam de máxima estabilidade
- Equipes com múltiplas linhas de WhatsApp

---

### 📱 WhatsApp Uazapi

Solução econômica e escalável para operações de alto volume.

**Vantagens principais:**

- **Preço competitivo** - Ideal para alto volume de mensagens
- **Conexão flexível** - Por QR ou código de emparelhamento
- **Múltiplas linhas** - Cada número com sua própria configuração
- **Controle de velocidade** - Evite bloqueios com envio controlado

**Conteúdo suportado:**

- Textos, imagens, vídeos
- Áudio e notas de voz
- Documentos
- Sincronização global e por conversa sob demanda de mensagens recentes, com recuperação de mídia histórica

**Configuração de filtros de chat:**

Defina quais conversas você deseja receber na plataforma:

- **Filtrar por tipo** - Receba apenas chats individuais, grupos, ou ambos
- **Lista de exclusão** - Ignore números específicos
- **Lista de inclusão** - Receba apenas de números específicos
- **Configuração pela UI** - Gerencie filtros diretamente das configurações do canal

**Proxy regional:**

- **Seleção de cidade brasileira** - Salve uma cidade opcional do proxy gerenciado nas configurações do canal
- **Aplicação em novas conexões** - A localização salva é usada no QR, no código de pareamento e na recriação da sessão
- **Proxy personalizado ou sem proxy** - Alterne para uma URL de proxy própria ou remova completamente o proxy ativo

**Ideal para:**

- Empresas com orçamento apertado
- Operações de alto volume
- Equipes que precisam de múltiplas linhas de baixo custo

---

### 📱 WhatsApp Notificame

Provedor brasileiro que combina a API oficial do WhatsApp Business com facilidade de uso.

**Vantagens principais:**

- **API oficial do Meta** - Toda a confiabilidade da API oficial
- **Templates aprovados** - Envie mensagens fora da janela de 24h
- **Sincronização automática** - Seus templates aprovados são importados automaticamente
- **Múltiplas linhas** - Gerencie vários canais de uma conta

**Conteúdo suportado:**

- Textos e templates com parâmetros personalizados
- Imagens, vídeos e documentos
- Localizações compartilhadas

**Ideal para:**

- Empresas no Brasil ou América Latina
- Operações que requerem templates oficiais
- Equipes que precisam da confiabilidade da API oficial

---

### 🎙️ Integração WaVoIP (Webphone) *(Evolution/WAHA/Uazapi)*

Faça chamadas de voz pelo WhatsApp diretamente da plataforma usando provedores alternativos:

**O que é WaVoIP?**

WaVoIP permite chamadas de voz pelo WhatsApp para provedores que não usam a Cloud API oficial do Meta (Evolution, WAHA, Uazapi). É um serviço de terceiros que conecta as chamadas de voz ao seu navegador.

**Funcionalidades principais:**

- **Chamadas de entrada e saída** - Suporte completo de voz pelo WhatsApp
- **Webphone intuitivo** - Widget flutuante fácil de usar no navegador
- **Controles completos** - Silenciar, desligar, aceitar, recusar chamadas
- **Duração em tempo real** - Cronômetro visível durante a chamada
- **Indicador de qualidade** - Monitore a qualidade da conexão ao vivo
- **Sessão persistente do dispositivo** - Mantém autenticação e status por inbox para reduzir reconexões manuais
- **Gravação automática** - Gravação automática com opção de download
- **Armazenamento de gravações** - Gravações salvas e anexadas às conversas

**Como funciona:**

1. Configure suas credenciais de conta WaVoIP
2. Ative a função WaVoIP na sua conta
3. O widget webphone aparece quando chegam chamadas
4. Aceite/recuse chamadas diretamente do navegador
5. Faça chamadas de saída do perfil do contato

**Benefícios:**

- Chamadas de voz sem API oficial do WhatsApp Business
- Funciona com números pessoais de WhatsApp
- Sem cobranças por chamada do Meta
- Histórico completo de chamadas na conversa

---

### 🔄 Migração de Inbox

Quando precisar reorganizar seus canais:

- **Transfira conversas** - Mova chats entre canais sem perder histórico
- **Preserve todo o contexto** - Mensagens, arquivos e notas são mantidos
- **Operações em massa** - Migre múltiplas conversas de uma vez

### Histórico de Conversa Unificado

Contexto completo de cada cliente independentemente de como te contatou:

- **Visão 360°** - Todo histórico do contato em um lugar
- **Todos os canais** - WhatsApp, email, redes sociais, tudo junto
- **Contexto imediato** - Entenda o cliente antes de responder
- **Respostas do WhatsApp** - Respostas citadas podem referenciar mensagens de conversas anteriores quando o histórico está ativo e preservam o contexto em coexistência entre WAMIDs de escopo de telefone e BSUID

### Controles de Privacidade

Configure o que seus agentes podem ver e acessar:

- **Só minhas conversas** - Agentes veem apenas seus chats atribuídos
- **Ocultar contatos** - Restrinja acesso à base de dados completa
- **Interface simplificada** - Oculte opções que não precisam usar
- **Controle granular** - Configure permissões por conta

---

### 📝 Edição e Exclusão de Mensagens *(Evolution/WAHA/Uazapi)*

Edite e exclua mensagens do WhatsApp após o envio:

**Editar Mensagens:**

- **Janela de 15 minutos** - Edite mensagens enviadas dentro de 15 minutos
- **Sincronização** - Mensagens editadas sincronizam do WhatsApp automaticamente
- **Contexto do remetente do grupo** - Edições recebidas em grupos mantêm o número e o nome do participante visíveis abaixo do indicador de edição
- **Indicador de edição** - Mensagens editadas mostram label "editada"
- **Todos os provedores** - Funciona com Evolution, WAHA e Uazapi

**Excluir Mensagens:**

- **Apagar para todos** - Remova mensagens enviadas
- **Confirmação** - Confirmação de segurança antes da exclusão
- **Atualização de status** - Mensagens excluídas aparecem como excluídas na conversa

---

### 🧩 Quadro Kanban Comercial *(Mega)*

Gerencie oportunidades comerciais em um pipeline visual conectado ao contexto omnichannel das conversas:

- **Funis com etapas personalizáveis** - Crie múltiplos funis e defina uma etapa padrão por funil
- **Lista completa por carregamento progressivo** - A visualização em lista carrega 30 oportunidades por página e permite buscar as seguintes sem perder os cards já exibidos
- **Visão em quadro e em lista** - Alterne entre pipeline visual e lista operacional conforme o fluxo da equipe
- **Filtros avançados por inbox/canal/atividade** - Segmente oportunidades por origem e movimentação recente
- **Filtros por etiquetas** - Filtre por etiquetas de conversa em quadro/lista e reflita nas métricas por etapa
- **Colunas configuráveis por usuário** - Mostre ou oculte colunas e mantenha preferências salvas localmente
- **Ficha 360 do item** - Inclui checklist, notas, anexos, agentes atribuídos, ofertas e atributos personalizados
- **Notas longas legíveis** - Abra o texto formatado completo e os anexos em uma visualização com rolagem, com edição direta quando tiver permissão
- **Busca nas relações do item** - Encontre conversas vinculadas com busca remota ao gerenciar relações do item
- **Moeda padrão por conta** - A moeda base do quadro é definida nas configurações da conta (`default_currency`)
- **Moeda consistente em todo o Kanban** - Cards, detalhes, ofertas, atividades e histórico seguem a prioridade oferta → item → conta → idioma; cada lado de uma alteração histórica mantém sua própria moeda
- **Totais por moeda em cada etapa** - O cabeçalho mantém PYG, USD, EUR e qualquer outra moeda separados, sem conversão nem soma entre moedas; o tooltip cobre todas as ofertas filtradas mesmo quando a paginação ainda não carregou todos os cards
- **Override de moeda por oferta custom** - Em ofertas manuais do tipo produto/serviço, o usuário pode escolher a moeda por oferta
- **Sem moeda em itens sem ofertas** - Se o item não tem ofertas, o valor aparece como placeholder e não entra em totais monetários
- **Downloads fiéis de relatórios Kanban** - Os CSVs incluem todos os cards autorizados que correspondem aos filtros ativos de funil, data, agente e inbox; preservam texto livre com segurança para planilhas e usam o idioma selecionado, os nomes de etapas configurados e a moeda do card ou da conta
- **Etiquetas na criação e no card** - Selecione etiquetas existentes ao criar um item ou adicione e remova diretamente no seu card
- **Relacionamentos nativos com contato e conversa** - Mantenha o contexto comercial ligado ao chat real do cliente
- **Ponte com Google Agenda** - Itens com data programada ou deadline podem criar eventos de calendario do MEGA quando a sincronizacao de Kanban esta habilitada no nivel da conta
- **Automações por etapa** - Dispare ações ao entrar ou mover etapas, incluindo mensagens rápidas e regras operacionais
- **Acompanhamentos sem resposta** - Após a espera configurada, envie texto ou multimídia carregada para a conversa principal do item somente se o contato não respondeu. O editor autocompleta variáveis do ReplyBox para dados do contato, conversa, inbox, agente e atributos personalizados. Em inboxes configurados do WhatsApp Cloud, também permite templates aprovados e mantém mensagens livres bloqueadas fora da janela de 24 horas
- **Entrada sem grupos** - Cada etapa de entrada pode excluir conversas de grupos do WhatsApp para não criar itens nem iniciar seus fluxos automáticos
- **Entrega automática de modelos** - Os modelos automáticos de uma etapa são enviados apenas uma vez por item por padrão, evitando mensagens duplicadas quando o item entra novamente na etapa. O editor sugere variáveis como `{{contact.name}}` ao digitar `{{` e as resolve no envio; cada modelo pode habilitar explicitamente o reenvio a cada nova entrada; mensagens rápidas manuais não têm essa restrição
- **Alertas Kanban** - Notifica membros das equipes selecionadas e agentes atribuídos por automações de etapa, e o agente responsável quando uma tarefa de checklist chega à data limite; alertas dispensados reaparecem após o intervalo configurado no funil apenas enquanto essa tarefa permanecer pendente. Agrupa alertas em um banner não bloqueante e não envia email
- **Sincronização em tempo real** - Mudanças de etapa e dados do item refletem instantaneamente na lista de chats e no painel do contato
- **Negócios abertos do contato** - Cada funil pode habilitar na Configuração Avançada a exibição de seus itens Kanban abertos em todas as conversas do contato atual; a opção é desativada por padrão, preserva as regras de visibilidade e identifica as conversas relacionadas
- **Painéis autorizados** - O bloco Kanban do painel de conversa e a entrada do sidebar ficam ocultos quando o usuário não tem itens visíveis nem funis disponíveis para adicionar negócios
- **Detalhe Kanban pela conversa** - Os ícones de canal do cartão mostram cada tipo de inbox vinculado: abrem diretamente sua única conversa ou um seletor limitado a esse canal quando há várias, sem recarregar o quadro; no mobile, o detalhe mostra primeiro as informações comerciais e abre o perfil do item em um painel lateral. O painel de contato do drawer oculta conversas anteriores para manter o contexto do item
- **Acesso Kanban em tempo real** - Ao adicionar ou remover agentes do funil, o sidebar, a lista de funis e os itens visíveis atualizam sem recarregar
- **Múltiplas conversas vinculadas** - Um mesmo item Kanban pode se relacionar com várias conversas; a primeira permanece como vínculo principal e as adicionais aparecem na aba de relacionamentos, com seletor limitado aos inboxes do funil e ícones de canal
- **Uma oportunidade aberta por contato e funil** - A criação automática reutiliza o item aberto do contato e vincula nele novas conversas do Instagram, WhatsApp ou outros inboxes habilitados; cada funil é avaliado separadamente e uma oportunidade ganha ou perdida permite iniciar outra
- **Histórico sem vínculo quebrado** - Se uma conversa vinculada for excluída, o item Kanban permanece como histórico e o vínculo é limpo
- **Acesso Kanban por função e permissão** - Administradores gerenciam todos os funis e itens; agentes e funções com `kanban_view` trabalham os itens autorizados; `kanban_manage` também cria e edita os funis atribuídos, sem excluir, definir o padrão ou alterar a visibilidade
- **Autoatribuição administrativa** - O administrador pode se atribuir e se remover de qualquer item mesmo sem constar entre os agentes ou inboxes do funil; os demais usuários mantêm as regras normais de elegibilidade
- **Visibilidade controlada dos itens** - O criador sempre pode ver seu item; com uma conversa vinculada válida, o responsável só pode vê-lo se também estiver selecionado no funil, e os agentes atribuídos manualmente ao item podem vê-lo; um vínculo stale fica visível somente para administrador e criador. O modo `everyone` do funil permite que todos os seus agentes vejam todos os itens, enquanto `assigned_only` restringe a visibilidade aos agentes autorizados.
- **Agentes flexíveis por funil** - Qualquer membro da conta com acesso ao Kanban pode ser adicionado ao funil, com ou sem inboxes selecionadas; uma função personalizada requer `kanban_view` ou `kanban_manage`. Com inboxes configuradas, atribuições manuais de itens exigem acesso a pelo menos uma. Ao mover um item, seus responsáveis são incluídos automaticamente no funil de destino sem alterar permissões de inbox
- **Configuração e automações protegidas** - A configuração global é somente leitura para os atores Kanban; suas alterações e as automações globais são exclusivas de administradores. `kanban_manage` administra apenas os funis atribuídos ao usuário

---

## 🔐 Segurança e Conformidade

### Autenticação

- **2FA/MFA** - Autenticação de dois fatores
- **SAML/SSO** - Single Sign-On empresarial
- **Tokens de API** - Acesso programático seguro
- **Suporte para conta suspensa** - Usuários suspensos veem o aviso de política com uma ação direta para contatar o suporte; administradores no Cloud também podem abrir o faturamento para regularizar o pagamento e restaurar o acesso. Superadministradores registram uma categoria e um motivo para cada suspensão e podem consultar ou corrigir a entrada mais recente nos detalhes da conta.
- **Reenvio de confirmação** - Superadministradores podem reenviar o e-mail de confirmação de um usuário pendente pelos detalhes, sem expor links ou tokens.

### Privacidade

- **GDPR Ready** - Conformidade com regulamentações
- **Exclusão de dados** - Direito ao esquecimento
- **Exportação** - Portabilidade de dados

### Infraestrutura

- **Criptografia em trânsito** - HTTPS obrigatório
- **Criptografia em repouso** - Dados protegidos
- **Backups automáticos** - Recuperação de desastres
- **Autoescalonamento de workers por fila** - Publicação opcional no CloudWatch de latência, profundidade, jobs enfileirados e utilização do Sidekiq para ajustar a capacidade conforme o backlog
- **Proteção de licença** *(Mega)* - Verificação de integridade para reforçar controle de deploy
- **Observabilidade de release** - Melhor rastreabilidade de erros por versão no monitoramento

---

## 📱 Aplicativos

### Aplicativo Web Progressivo (PWA) *(Mega)*

MEGA funciona como um **Progressive Web App** completo: instale em qualquer dispositivo e tenha uma experiência idêntica a um app nativo, sem passar por lojas de aplicativos.

**Instalação e Experiência Nativa:**

- **Instalável com um toque** - Banner inteligente que aparece automaticamente em dispositivos móveis convidando a instalar o app
- **Desktop e celular** - Funciona no Chrome, Edge, Safari (iOS/macOS) e qualquer navegador compatível com PWA
- **Tela cheia** - Executa em modo standalone, sem a barra de endereços do navegador
- **Splash screen personalizada e ágil** - Tela de carregamento com sua marca que desaparece assim que o Vue pinta a interface, com limite de segurança se a inicialização falhar
- **Atalhos rápidos** - Acesse diretamente Conversas ou Notificações pelo menu contextual do ícone do app
- **Ícone dinâmico** - O ícone do app é gerado a partir do logo thumbnail configurado, com fallback para o ícone de notificações, em todos os tamanhos necessários (48px a 512px)
- **Fundo de ícone configurável** - Use uma cor própria para o ícone instalável mantendo branco como padrão
- **Badge monocromático** - Ícone badge otimizado com silhueta monocromática para notificações do sistema

**Notificações Push Avançadas:**

- **Notificações push nativas** - Receba alertas instantâneos mesmo com o app fechado, diretamente no sistema operacional
- **Indicador na aba** - Se uma mensagem chega com a aba oculta ou sem foco, o favicon muda para o ícone de notificações e volta ao normal quando o usuário retorna
- **Resposta rápida inline** - Responda mensagens diretamente pela notificação sem abrir o app
- **Marcar como lido** - Marque notificações como lidas pela própria notificação com um toque
- **Empilhamento de mensagens** - Mensagens da mesma conversa são empilhadas em uma única notificação (estilo WhatsApp) mostrando até 10 mensagens
- **Contador de não lidos** - O badge do ícone do app mostra o número exato de notificações não lidas
- **Timestamp de cache preciso** - Invalidação consistente de assets do Service Worker para evitar conteúdo desatualizado
- **Ativação inteligente** - Prompt automático ao abrir a PWA pela primeira vez para ativar notificações com flags pré-configurados (atribuição, menção, mensagem nova)
- **Ciclo de assinatura confiável** - A desativação por usuário e dispositivo persiste após recarregar, o logout revoga o vínculo do navegador e mudanças da chave VAPID são renovadas automaticamente
- **Som configurável** - Alertas de áudio que funcionam até no iOS, com desbloqueio automático do AudioContext ao primeiro toque
- **Som diferido** - Se o app está em segundo plano e não consegue reproduzir áudio, reproduz automaticamente quando você volta ao app
- **Vibração** - Padrão de vibração personalizado em dispositivos móveis ao receber notificações

**Funcionamento Offline:**

- **Página offline personalizada** - Quando não há conexão, exibe uma página elegante com o logo da sua marca e botão de tentar novamente
- **Cache inteligente** - Apenas assets Vite com fingerprint são armazenados, dentro de um cache de execução limitado para acelerar carregamentos repetidos
- **Navegação offline segura** - Páginas autenticadas e APIs nunca são persistidas; sem rede, a navegação usa a página offline pública
- **Limpeza automática** - O Service Worker remove versões obsoletas e limita os assets fingerprinted retidos

**Personalização de Marca (White-label):**

- **Manifesto dinâmico** - O manifesto PWA é gerado dinamicamente com o nome, descrição, cores e logo da sua instalação
- **Suporte SVG** - Os logos SVG são convertidos para PNG de alta resolução via librsvg ou libvips antes da composição final dos assets
- **Ícones para Apple** - Geração automática de apple-touch-icons em todos os tamanhos exigidos pelo iOS
- **Splash screens iOS** - 14 resoluções de splash screen pré-geradas para todos os modelos de iPhone e iPad
- **Cores da marca** - O theme-color e background-color do manifesto usam sua cor primária configurada

### Aplicativo Móvel *(Em desenvolvimento)*

- **iOS e Android** - Atenda clientes do seu celular
- **Notificações push** - Alertas instantâneos de novas conversas
- **Funcionalidade completa** - Todas as ferramentas no seu bolso

---

## 📞 Suporte e Recursos

- **Central de Ajuda** - Documentação completa e guias passo a passo
- **Comunidade ativa** - Conecte-se com outros usuários
- **Suporte Enterprise** - Atendimento prioritário e dedicado para clientes empresariais

---

*MEGA - Transformando a forma como as empresas se comunicam com seus clientes.*

**© 2026 MEGA - Todos os direitos reservados**
