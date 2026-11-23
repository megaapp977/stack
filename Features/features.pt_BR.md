# 🚀 MEGA - Plataforma de Comunicação Omnichannel

## Mega Assistant

Administradores podem perguntar quais contatos enviaram mais mensagens em um período recente. O Mega Assistant conta as mensagens públicas recebidas em todas as conversas de cada contato e resume os assuntos observados em uma amostra claramente indicada de textos recentes. A descoberta de ferramentas encontra ações pelo significado e mostra os parâmetros necessários para consultas ou propostas de alterações.

Ao revisar as caixas de entrada, o Mega Assistant distingue canais sem consulta de saúde de uma conexão WhatsApp Cloud cuja credencial precisa de reautorização. Ele apresenta esses resultados como diagnósticos e evita repetir a mesma consulta sem alterações.

Antes de propor uma alteração, o Mega Assistant verifica se os dados estão completos e válidos. Se faltar algo, ele corrige ou pergunta na mesma resposta, evitando cartões de confirmação que falhariam depois. Ele também não repete consultas já feitas nem duplica uma proposta pendente.

O Mega Assistant resolve em uma única consulta os pedidos mais frequentes: conversas aguardando resposta, a ficha completa de um contato com suas conversas e últimas mensagens, um período comparado ao anterior por canal e o estado do Captain com seus assistentes, caixas de entrada e cenários. Para pedidos com várias partes, registra primeiro um plano e responde a cada item. Enquanto trabalha, mostra o que está consultando (caixa de entrada, contato, status, período), calcula “hoje” e “semana passada” no fuso horário do navegador e responde no idioma da sua última mensagem. Várias propostas de uma mesma resposta podem ser confirmadas ou canceladas juntas. Planos e contas podem escolher um modelo para tarefas complexas, que atende pedidos com várias partes, diagnósticos e relatórios comparativos e assume se o modelo principal falhar.

Quando uma alteração se aplica a muitas conversas de uma vez (resolver, atribuir ou etiquetar), ao confirmar ela é aplicada conversa por conversa e o cartão mostra quantas mudaram, quantas já tinham a alteração e quais não puderam ser alteradas e por quê, com um link para cada conversa. Você pode continuar conversando enquanto ela é aplicada, e o assistente informa o resultado ao terminar.

Para pedidos sobre muitos registros (todas as conversas de um período, as mensagens que mencionam um pedido, todos os contatos com uma etiqueta), o Mega Assistant seleciona todos no servidor, até 5.000, informa o total exato e guarda a seleção para os passos seguintes: as conversas dessas mensagens, os contatos dessas conversas, perguntas de acompanhamento sobre o mesmo conjunto, ou uma única alteração para todos que você confirma uma vez.

Para avaliar o que as conversas dizem (quais clientes pediram reembolso, quais são as mais urgentes, como se sentem), o Mega Assistant revisa as conversas selecionadas uma a uma em segundo plano, as 100 mais recentes por pedido, e um cartão mostra quanto avançou. Ao terminar, responde no chat com o que encontrou, quantas leu e quantas faltam, e oferece continuar com as 100 seguintes. As conversas que coincidem podem ser usadas no passo seguinte, como listar seus contatos ou etiquetar todas. Cada conversa revisada é cobrada pelo preço em AI Actions do modelo da revisão; a revisão para se a conta ficar sem elas.

O Mega Assistant sabe o que você está vendo. Com uma conversa ou um contato aberto, “resuma isto”, “transfira esta conversa para Vendas” ou “adicione uma nota a este contato” funcionam sem digitar nenhum identificador; com conversas selecionadas na lista, “resolva estas” age exatamente sobre essa seleção. Apenas referências são compartilhadas (o registro, os filtros da lista e as conversas selecionadas, nunca o texto da página), e cada uma é validada contra suas permissões antes de o assistente vê-la. Uma linha acima do campo de mensagem mostra o que o assistente vai usar, com um botão para ignorar. Os cartões de confirmação indicam o registro que alteram, marcam quando ele veio da sua tela e avisam se você não o está mais vendo; uma alteração em um registro excluído ou ao qual você perdeu acesso não pode ser confirmada. Ele também reconhece o quadro e a tarefa do Kanban, o fluxo aberto no Flow Builder, a caixa de entrada cujas configurações você está editando, os contatos selecionados na lista e o registro das páginas de um só: o assistente do Captain, a sala de chat, a empresa, o portal da Central de ajuda (com seu idioma), o relatório de uma campanha, de um agente, uma caixa de entrada, uma equipe ou uma etiqueta, o app do painel, a política de capacidade, o monitor e a importação de dados. Quando você pede para agendar algo, ele distingue uma mensagem agendada, uma campanha, uma tarefa, um evento do calendário ou adiar uma conversa pelo que deve acontecer nesse momento, e pergunta quando não está claro.

Ele também sabe qual formulário está aberto sobre a página, mesmo sem a URL mudar: criar ou editar uma resposta rápida, um atributo personalizado, um bot, uma automação, uma campanha ou uma mensagem agendada, e no Captain um novo assistente, uma pergunta frequente, um documento, um cenário, uma regra, uma ferramenta ou um servidor MCP. “Preencha este formulário” ou “altere esta campanha” se referem ao que você tem aberto, e ao ir para outra página ele deixa de usá-lo. Também pode alterar o que antes só consultava: a pesquisa de satisfação de uma caixa de entrada (e criar o template de WhatsApp dela), os templates de mensagem, os dashboard apps, os monitores do Captain, as ofertas do Kanban e o seu próprio perfil (nome, nome de exibição e assinatura; e-mail, senha e verificação em duas etapas são alterados na página de perfil). Como toda alteração, ele propõe primeiro e você confirma.

Ao confirmar uma mudança, o Mega Assistant verifica de novo se você ainda pode fazê-la: se a função foi desativada ou você não tem mais o papel que essa mudança exige, ela não é aplicada. Se alguém alterou os valores que o cartão mostrava como atuais desde a proposta, eles também não são sobrescritos: o assistente diz o que mudou e propõe de novo só se você ainda quiser.

Depois de aplicar uma mudança confirmada, o Mega Assistant lê o registro de novo e confere se ele ficou com os valores enviados. O cartão diz “Alteração aplicada e conferida no registro” ou avisa quando o registro mostra outros valores, e o assistente conta isso no chat sem afirmar mais do que conferiu.

Antes de explicar como configurar algo ou de se oferecer para fazê-lo, o Mega Assistant verifica na sua conta se essa função está habilitada, se o seu papel pode alterá-la e se existe uma ferramenta para isso no chat. Se estiver desativada ou exigir outro papel, ele avisa e explica quem pode habilitá-la, sem prometer configurá-la; se não houver ferramenta, ele guia você passo a passo na tela dela. “O que você pode configurar para mim?” é respondido com a lista real de módulos da sua conta e o status de cada um.

Você pode dizer o que quer conseguir com as suas palavras, por exemplo “quero automatizar o atendimento no WhatsApp, responder perguntas frequentes, identificar oportunidades de venda e passar para uma pessoa quando precisar”. O Mega Assistant separa em necessidades, verifica quais módulos você tem e o que já está configurado para reaproveitar, recomenda uma solução explicando o porquê, monta o plano e pede só os dados que faltam. Depois configura passo a passo, com a sua confirmação, conferindo cada resultado e seguindo para o próximo passo.

Quando você pergunta “como funciona…?”, o Mega Assistant responde a partir da documentação funcional de cada módulo, que vem com o aplicativo: o que é, como funciona, requisitos, limites, como configurar e exemplos, com a data em que foi revisada e a seção da documentação do produto de onde vem. Ele lê apenas o módulo de que você está falando e, quando um módulo não tem documentação, diz isso em vez de inventar menus ou opções.

Quando uma pergunta vira uma configuração de vários passos (“vamos configurar”), o Mega Assistant anota no chat o objetivo, as decisões que você tomou e os passos que faltam. Nas mensagens seguintes, ao voltar ao chat ou numa chamada de voz, ele continua dali com as suas decisões e só pergunta o que falta; se você mudar de ideia, atualiza a decisão, e encerra o objetivo quando a configuração termina ou é abandonada. No Captain ele anota cada fase da configuração e retoma na primeira pendente. É a memória do chat, não uma permissão: cada mudança continua sendo proposta e confirmada.

Se você retomar uma configuração deixada há dias, o Mega Assistant primeiro confirma se você ainda a quer e lê de novo a configuração atual antes de continuar.

Numa chamada de voz, quando a resposta mostra cartões, tabelas ou gráficos, a voz também recebe os valores: diz os números que respondem ao que você pediu (não só que está na tela) e responde perguntas de seguimento como “e as resoluções?” com esses mesmos dados.

No Flow Builder, o Mega Assistant altera um fluxo existente bloco a bloco: adiciona, altera ou remove só os blocos e conexões que você pedir e deixa o resto exatamente como estava. Antes de propor, verifica se o fluxo continua válido e, se alguém o editou nesse meio-tempo, confirmar a mudança não sobrescreve essa edição. Ele nunca publica por conta própria: publicar exige que você peça e confirme.

Para medir como o assistente funciona em cada conta, cada resposta registra quanto tempo levou, quantas ferramentas usou, quais falharam ou foram recusadas por permissão, os módulos consultados que estavam desativados, sem permissão ou sem documentação, e como terminou. Um relatório por conta junta isso com o custo dos modelos e o resultado das mudanças confirmadas (aplicadas, recusadas ao confirmar e conferidas no registro).

Os administradores veem isso na página do assistente, na aba Métricas do histórico (o ícone de gráfico), para os últimos 7, 30 ou 90 dias: respostas, com falha, sem fonte (respostas longas que não leram dados nem documentação, uma estimativa), tempo médio e das mais lentas, custo, mudanças aplicadas, não aplicadas, conferidas e com outros valores, e as ferramentas e módulos que mais falham ou são recusados.

Os cartões de confirmação mostram o que cada alteração faz em termos simples (para quem a conversa vai, quais etiquetas são adicionadas ou removidas, a tarefa ou o fluxo que cria ou altera) e permitem ajustar a equipe, o agente ou as etiquetas antes de confirmar. Cada ajuste, seu ou do assistente quando você diz “melhor para Suporte”, vira uma nova revisão do mesmo cartão, e só a última pode ser confirmada. Tabelas, gráficos e outros resultados aparecem assim que ficam prontos, podem ser atualizados em respostas seguintes e abrem em uma visualização maior. Formulários e passos sugeridos enviam exatamente o que você escolheu, validado contra o formulário que o assistente mostrou.

Voz: o microfone da caixa de mensagem grava o que você diz, transcreve e envia como sua mensagem. O botão de ondas abre uma conversa por voz em tempo real: um círculo animado mostra se o assistente está ouvindo, pensando ou falando, e você pode continuar digitando, se silenciar ou desligar com o X. O que você pede falando passa pelo mesmo assistente do chat, com as mesmas ferramentas, cartões e propostas, e fica no histórico como uma mensagem digitada; o assistente lê um resumo da resposta. Um “sim” falado a uma proposta inicia no cartão uma contagem regressiva de 5 segundos que você pode cancelar pela voz ou com um clique; exclusões, mesclagens e alterações em massa sempre exigem o clique. A voz é cobrada em blocos de 5 minutos de AI Actions e cada pedido conta como uma mensagem. Em Configurações → Captain você escolhe a voz (Marin e Cedar recomendadas), a velocidade e, se tiver, sua voz personalizada da OpenAI. Se você atualizar a página durante uma chamada, a próxima substitui a anterior. Durante uma chamada você pode trocar de tela: a chamada continua no mascote ou, se ele estiver fechado, em um pequeno controle que ocupa o lugar do mascote, com o mascote dentro e um anel colorido (verde quando ouve ou fala, âmbar quando trabalha, espera sua confirmação ou o microfone está silenciado), que diz "Chamada com …" e o que está fazendo, com silenciar, "Abrir chat" e desligar; arrastá-lo pelo mascote ou pelo texto move o mascote junto; ela só termina quando você desliga. A voz sabe em qual tela você está e lembra o que já foi dito no chat, inclusive em uma nova chamada. Ela conhece os nomes da conta (seus contatos recentes, caixas de entrada, equipes, agentes e etiquetas) para escrevê-los como estão salvos mesmo quando soam parecidos, e se um nome dito não aparece, o assistente tenta como a transcrição o ouviu e suas partes antes de dizer que não existe. O assistente pode abrir qualquer tela do painel para guiar você (por exemplo, as configurações de uma caixa de entrada, um contato ou um assistente do Captain), por chat ou por voz, apenas entre as páginas que você tem permissão para ver e que a conta tem habilitadas. Se um pedido demora, a voz vai contando o que está fazendo (por exemplo, que está procurando o contato) em vez de ficar em silêncio, sem falar por cima de você. Enquanto busca, um “obrigado” recebe uma resposta breve sem interromper a tarefa, “espera” o deixa em silêncio, uma correção (“só as do WhatsApp”) roda assim que termina e “cancela” interrompe a busca no servidor. Cada usuário pode dar ao assistente o seu próprio nome (no perfil ou pedindo: “de agora em diante quero te chamar de Rio”, salvo ao confirmar), e o administrador pode nomeá-lo para toda a conta em Configurações → Captain; o mesmo nome aparece na tela, no chat e na voz. Ao conectar a chamada, o assistente cumprimenta uma única vez com o seu nome. O que você diz na chamada e o que a voz responde são escritos no chat da chamada, assim o chat, o assistente escrito e a próxima chamada se lembram (um pedido falado fica como a sua mensagem de pedido; o cumprimento e os avisos de progresso não são escritos). Se você confirmar ou cancelar uma proposta com um clique durante a chamada, a voz fica sabendo e diz o resultado real. Durante uma chamada, o painel mostra sempre o chat dela: o botão de voz leva você a esse chat em vez de criar um vazio. Se durante a chamada você digitar uma mensagem ou anexar um arquivo no chat, é como se você tivesse falado: a voz responde em voz alta, como o mesmo assistente do chat (você digita "oi" e ela diz "Oi! Tudo bem?"), lê o arquivo quando precisa e a resposta fica escrita no chat; o que você diz fica com suas palavras e o que você ouve é o mesmo que fica escrito, em frases curtas; a voz sabe em que tela você está enquanto navega pelo painel; ao retomar um chat, a chamada cumprimenta dizendo do que vocês estavam falando.

Preferências do assistente: no seu perfil você escolhe, só para a conta em que está, o idioma das respostas (o da sua mensagem, ou sempre espanhol, inglês ou português), o estilo (equilibrado, breve ou detalhado), como ver listas de registros (automático, tabela ou cartões) e se a chamada de voz começa com uma saudação falada. São opcionais e valem para o chat e a voz; são dicas de estilo, nunca permissões: não mudam o que o assistente pode ver ou fazer. O administrador pode escrever a saudação da chamada em Configurações → Captain, na seção de voz: texto simples de até 200 caracteres, em que {name} é substituído pelo nome do assistente.

Privacidade e retenção: suas preferências e o nome que você deu ao assistente ficam salvos no seu usuário, separados por conta; só é salvo o que você mudou, nunca são aprendidos das suas conversas e são apagados com “Apagar minhas preferências” (o nome, deixando-o vazio). Como fazem parte dos dados do seu usuário, outros membros da conta podem lê-los pela API de agentes. De uma chamada de voz guardamos o registro da sessão (início, fim, modelo e blocos cobrados), os pedidos que a voz passou ao assistente e as respostas escritas, e o texto do que você disse e do que a voz respondeu, como mensagens do histórico; você e os administradores da conta os veem, e apagar o histórico os apaga. O áudio não é guardado. O áudio vai direto do seu navegador para a OpenAI, e a retenção segue a política de dados da API da OpenAI.

Os administradores veem ao lado de cada resposta quanto ela custou em chamadas ao modelo, incluindo qualquer revisão que ela tenha iniciado. O Mega Assistant também sabe o que significa cada status e prioridade de conversa e avalia a urgência ou o assunto lendo as conversas, não só pelo campo de prioridade.

Em pedidos que misturam perguntas e alterações, ele reserva espaço para deixar as alterações propostas mesmo depois de usar todas as consultas, e responde cada item pedido: resolvido, proposto ou pendente e por quê. Se uma consulta falhar no servidor, ele continua com o restante em vez de interromper a resposta.

### Comportamento atual (setembro de 2026)

Este bloco tem prioridade sobre os parágrafos anteriores desta seção.

- **Quem usa:** administradores da conta e membros cujo papel personalizado inclui “Usar o assistente de IA”. Administradores podem ler os chats da equipe com o assistente (somente leitura) na aba Equipe da página inteira; os chats não são mais privados do dono.
- **Histórico:** pesquisa, Fixados, Hoje, Últimos 7 dias e Anteriores, igual na página inteira e no painel flutuante. Um ponto âmbar marca chats com uma ação aguardando confirmação.
- **Ações:** cada proposta mostra um cartão com título, status, destinatário, link para a conversa e prévia do texto e arquivos que serão enviados, ou os campos que mudam com o valor atual e o novo. Mensagens de texto podem ser enviadas ou deixadas como rascunho na caixa de resposta.
- **Progresso e erros:** enquanto responde, o assistente mostra as ferramentas que usa. Respostas com falha dizem o motivo (sem modelo de IA disponível, o serviço de IA não respondeu).
- **Respostas enriquecidas:** quando você pede um relatório, uma tabela, um gráfico ou uma comparação, o assistente responde com blocos visuais abaixo do texto: texto, markdown, tabela (ordenável e exportável para CSV), métricas, cartão, gráfico (barras, linha, área, pizza, rosca), linha do tempo, contato, conversa, kanban, formulário, ações sugeridas e relatório HTML. Um relatório executivo é montado no chat com blocos (métricas, gráfico, conclusões, tabela) e o assistente oferece a versão em PDF como ação sugerida; o relatório HTML só é gerado quando você pede, abre sozinho no canvas da página completa e pode ser baixado ou salvo como PDF pela impressão do navegador. Formulários e ações sugeridas respondem no mesmo chat, então o assistente mantém o contexto. No pet, os blocos se adaptam à largura: métricas em 2×2, tabela com 3 colunas expansível e kanban com rolagem lateral. Relatórios e arquivos PDF, HTML, Markdown e de texto abrem em um canvas: na página completa é uma coluna à direita do chat (dá para continuar conversando) e no pet abre sobre a tela, com pré-visualização ou código, download e impressão.
- **Planos e AI Actions:** cada resposta concluída desconta as AI Actions do modelo que respondeu (a resposta automática após confirmar não). Sem AI Actions, as mensagens são recusadas e administradores veem um link para comprar um pacote; administradores veem o saldo. Os planos podem incluir o assistente só para consultas ou com ações. Administradores de contas sem o assistente veem o que ele oferece e um link para os planos.

A barra lateral da página completa separa Fixados de Recentes: cada seção pode ser recolhida independentemente, e chats fixados não se repetem em Recentes. Fixados aparece somente quando contém chats; os dois grupos mantêm a ordem pela atividade mais recente.

Cada linha do histórico na página completa oferece Renomear, Fixar/Desafixar e Excluir em um menu de três pontos, disponível ao passar o cursor, focar pelo teclado ou tocar. Títulos (1–100 caracteres sem espaços externos) e fixações persistem. Chats fixados aparecem primeiro, com atividade recente em ordem decrescente dentro de cada grupo e limite de 50 chats. Apenas os chats privados do usuário atual na conta atual podem ser gerenciados, com o recurso Mega Assistant habilitado. A exclusão exige confirmação e remove permanentemente o chat, mensagens, ações e anexos. Chats gerando uma resposta ou executando uma ação não podem ser excluídos até a conclusão. Excluir o chat selecionado inicia um novo chat e limpa seu rascunho e arquivos; gerenciar outro chat preserva o chat e rascunho atuais.

O histórico do assistente começa com Novo chat, seguido de uma seção Recentes que pode ser recolhida e expandida, com chats fixados primeiro e atividade em ordem decrescente dentro de cada grupo. Abrir ou renomear uma conversa antiga não muda sua ordem por atividade; novas mensagens atualizam sua posição.

O nome do assistente segue seu Custom Branding: Brand Name + “Assistant”, por exemplo “Acme Assistant”. Sua marca aparece de forma consistente no menu lateral, no chat e na ajuda de atalhos. Sem um nome configurado, usa “Mega Assistant”.

O mascote mostra a imagem Mega Assistant Pet configurada no Custom Branding, preservando suas proporções e controles de arrastar. Usa por padrão a imagem incluída do Mega Assistant e é independente do Logo Thumbnail.

O botão flutuante do Copilot fica oculto na página completa do Mega Assistant e continua disponível nas demais páginas do dashboard.

O atalho só aparece na ajuda quando a conta atual tem a feature Mega Assistant ativada, assim como no menu lateral. Não é executado com a feature desativada; abrir o chat também requer disponibilidade do assistente.

Alt + Shift + M alterna o assistente flutuante: se o chat estiver aberto, fecha o chat e oculta o mascote; caso contrário, restaura e abre o chat. Na página completa, foca o editor existente sem sair da conversa.

Alt + Shift + M recupera o mascote oculto e abre seu chat nas páginas do dashboard onde o assistente está disponível. Na página do assistente, foca o editor existente. O controle de fechar tem um X maior e com mais contraste; o atalho aparece na ajuda de teclado.

O mascote pode ser ocultado com seu próprio X e ativado novamente no cabeçalho da página do assistente. O botão de expandir do chat flutuante abre essa página com a mesma conversa, rascunho e anexos selecionados. A visibilidade é salva neste navegador; a transferência do chat fica apenas na memória e não sobrevive a uma recarga.

Ao iniciar um chat vazio, a página centraliza a saudação e o editor. O replybox compartilhado usa a superfície sólida e a borda do editor de conversas, com relevo sutil e foco visível; quando aparecem mensagens, permanece embaixo.

O menu lateral principal inclui uma página completa do assistente com histórico e conversa centralizada. Compartilha o editor arredondado com anexos com o painel flutuante; o mascote fica oculto enquanto esta página está aberta.

Mega Assistant começa com ferramentas nomeadas para contatos, conversas, contagens, caixas de entrada e leituras do Captain. Pode descobrir qualquer outra ferramenta nomeada elegível da conta em páginas explícitas e mantém no máximo 40 ferramentas nomeadas ativas por vez. Perguntas sobre configuração exigem consultar as APIs correspondentes, não apenas listar rotas; uma busca vazia ou parcial é informada como tal, e não como prova de que um registro ou recurso não existe. Captain é identificado como o módulo de IA da plataforma; resultados de leitura e alterações propostas ficam no histórico privado de ações da conversa.

Em cada chat privado, Mega Assistant reutiliza as ferramentas elegíveis e mantém estável o contexto inicial entre respostas para que provedores compatíveis possam usar cache e reduzir o custo.

Quando uma resposta propõe uma ação, a mensagem do assistente aparece primeiro e, depois de ser exibida por completo, o cartão de confirmação aparece abaixo.

A conversa acompanha o mascote ao movê-lo, abre no espaço disponível perto das bordas e mantém ambos dentro da tela. O cabeçalho compacto permite abrir o histórico ou iniciar uma conversa; as sugestões preenchem a mensagem sem enviá-la automaticamente.

Mega Assistant é um assistente privado da conta com mascote móvel, redimensionável e acessível por teclado, e painel baseado no Copilot. Descobre operações da conta, responde com resultados de APIs autenticadas e propõe alterações para confirmação explícita. Contagens usam totais da API, não tamanhos de página. Não requer servidor MCP, token nem permissão de API pública.

Provedores são atribuídos independentemente ao Captain e ao Mega Assistant. Os cartões de modelos da conta no Super Admin selecionam chat, imagens/PDF e transcrição de áudio por conta. Aceita até cinco imagens, PDFs, documentos de texto ou áudios (20 MB cada) com o botão +, arrastando e soltando sobre a caixa de texto ou colando (por exemplo, uma captura de tela). Arquivos e históricos são privados para o proprietário. Ações confirmadas exibem o resultado real e não executam duas vezes. Se um servidor reinicia enquanto o assistente responde, a resposta é retomada sozinha em poucos minutos em vez de ficar travada. Inclui ditado e voz em tempo real (veja Voz); não inclui telefonia.

## Seu Centro de Comando para o Atendimento ao Cliente do Futuro

Os cards de provedores IA resumem quantidade de modelos, capacidades verificadas e avisos de saldo. Modelos e testes abre um modal com usos atribuídos, status e erros salvos de cada modelo, sem expandir a grade. As ações de testar, editar e excluir com suas proteções são mantidas.

Raciocínio e ferramentas funcionam juntos em todos os provedores: cada modelo recebe o raciocínio no formato que sua API aceita (um nível, um orçamento de raciocínio ou nada se não raciocina), e os modelos da OpenAI são chamados pela Responses API. Os provedores compatíveis com OpenAI escolhem um preset: OpenRouter, xAI, DeepSeek, Mistral, Perplexity, Ollama e GPUStack usam sua própria integração, enquanto Groq, Together, Fireworks, DeepInfra, Cerebras, SambaNova, Qwen, Z.ai, vLLM, LM Studio ou qualquer gateway personalizado se conectam como gateway genérico, e o teste de capacidades detecta por modelo qual API usam (Responses ou Chat Completions).

O formulário de provedores fica centralizado. Um botão visível de entrada em lote abre um modal para colar modelos e selecionar capacidades; Cancelar ou Escape fecha sem adicionar linhas.

Adicionar/editar provedor usa conexão em duas colunas e uma tabela compacta de modelos. A entrada em lote aceita nomes separados por linhas ou vírgulas e capacidades compartilhadas; nomes existentes são combinados sem duplicar linhas.

As seleções do catálogo antigo continuam disponíveis para suas funções originais ao editar um provedor importado. Novas seleções qualificadas por provedor exigem capacidades atribuídas e verificadas. PDF/áudio legado resolve as credenciais atuais da OpenAI nativa, recorrendo às configurações da instalação quando não existe provedor nativo ativo. Áudio prioriza a integração OpenAI da conta; o fallback do Captain exige a função habilitada e cota disponível. Gravações mantêm seu fluxo especializado.

Uma correção de atualização restaura uma única vez as entradas ausentes `whisper-1`, `gpt-4o-mini-transcribe` e `text-embedding-3-small` no provedor nativo com identificador `openai`. Preserva credenciais, modelos personalizados, atribuições existentes, resultados de testes e seleções das contas. As entradas restauradas ficam configuradas, não verificadas automaticamente; selecioná-las com identificador de provedor continua exigindo testes. A correção pode restaurar uma entrada base removida anteriormente, mas não a adiciona novamente ao salvar normalmente. Modelos marcados como futuros não são adicionados.

Os modelos que a OpenAI está aposentando (a série GPT-4.1, `gpt-4o`, `whisper-1`, `gpt-4o-mini-transcribe` e `gpt-4o-transcribe`) são substituídos pelo GPT-6 Luna para texto e pelo GPT Transcribe para áudio. As funcionalidades do Captain usam o Luna por padrão (o Copilot usa o GPT-5.1) e o executam sem raciocínio, a menos que o AI Providers defina outro esforço para o modelo. Uma migração passa para Luna ou GPT Transcribe as escolhas salvas em contas, planos e configurações da instalação; uma escolha com provedor só passa para o mesmo provedor quando ele já verificou o substituto, e o Mega Assistant mantém sua escolha até a verificação. Os provedores OpenAI recebem os dois modelos com preço (GPT Transcribe US$ 0,0045 por minuto) e sem verificação: é preciso testá-los no AI Providers. A transcrição de chamadas com diarização continua em `gpt-4o-transcribe-diarize` porque a OpenAI não publicou um substituto. As listas de modelos do Captain e de IA também oferecem o GPT-6 Sol e o GPT-6.1 Terra.

A regeneração de FAQ preserva as respostas existentes em caso de erros ou resultados vazios. Substitui apenas respostas não editadas quando há resultados válidos, em uma transação que reverte a substituição se alguma inserção falhar. Para PDF legado, verifica o arquivo remoto e, somente diante de um 404, envia novamente o original mantido usando as mesmas credenciais da geração. Erros de permissão, saldo ou conexão não provocam outro envio; se o original não estiver disponível, o conhecimento anterior é preservado.

O formulário mostra cada modelo uma única vez, com caixas de Chat, PDF, Áudio e Embeddings. Somente capacidades marcadas são testadas. Seleções e verificações existentes são preservadas; modelos sem capacidade mostram uma indicação para selecioná-la. Alterar credenciais ou endpoint exige nova verificação.

Os testes usam um PDF válido de uma página e um WAV PCM de um segundo. A amostra de áudio silenciosa verifica a aceitação do arquivo, não a precisão da transcrição.

Os testes de modelos mostram no card saldo insuficiente ou cota esgotada informados pelo provedor. Esses resultados não demonstram incompatibilidade do modelo; recarregue ou confira o faturamento e teste novamente.

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
- **Identidade social preservada** *(Mega)* - Caixas do Facebook, Instagram e TikTok guardam o nome da página ou usuário do provedor sem sobrescrever um nome personalizado da caixa ao reconectar o canal.

### WhatsApp Business

- **Contatos brasileiros sem duplicação** *(Mega)* - Cloud, coexistência, Twilio WhatsApp e chamadas Cloud reutilizam contatos móveis existentes quando o provedor omite o nono dígito; correspondências exatas têm prioridade e telefones fixos não geram alternativas móveis.

Conecte-se com seus clientes através do canal de mensagens mais popular do mundo.

- **WhatsApp Cloud API** - Integração oficial do Meta com todas as funcionalidades empresariais
- **Recuperação do cadastro do WhatsApp Cloud** *(Mega)* - Conclua a conexão na mesma caixa com etapas separadas para verificar o número por SMS ou ligação e registrar seu PIN de duas etapas. Se não houver PIN salvo, ele será solicitado; um PIN esquecido deve ser recuperado na Meta. O status da conexão reflete o estado do número informado pela Meta.
- **Conectividade premium para chamadas Cloud** *(Mega)* - Empresas com redes restritivas podem usar conectividade de relay STUN/TURN administrada nas chamadas WebRTC do WhatsApp Cloud
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
- **Reconfiguração do cadastro integrado** *(Mega)* - Administradores podem atualizar as credenciais e a configuração do WhatsApp Business de uma caixa Cloud existente conectada pelo cadastro integrado sem habilitar um recurso da conta; o recurso de criação permanece exigido apenas para novas caixas
- **Arquitetura multi-servidor** *(Mega)* - Configure vários servidores por provedor com resolução automática de credenciais
- **Capacidade por servidor** *(Mega)* - Defina limites por servidor para distribuir a carga operacional
- **Suporte BSUID** *(Mega)* - Identificação robusta do contato e envio confiável mesmo sem `wa_id` tradicional
- **Chamadas e anexos mais confiáveis no WhatsApp Cloud** - Os anexos são enviados à Meta antes do envio (menos falhas por limite de downloads), as chamadas também chegam a contatos que só têm BSUID, o Messenger recebe os botões de Get Started e a tag HUMAN_AGENT é usada só quando se aplica
- **Mensagens não suportadas por provedor** *(Mega)* - Distingue conteúdo incompatível de mensagens indisponíveis por coexistência; somente estas últimas orientam a verificar o WhatsApp Business
- **Mensagens de template** - Envie mensagens fora da janela de 24 horas com templates aprovados; as automações bloqueiam localmente o envio de texto livre nesse estado e orientam o uso de um template
- **Direct Send do WhatsApp Cloud (beta)** *(Mega)* - Com a caixa de entrada habilitada pela Meta na beta, o botão de WhatsApp da caixa de resposta e da nova conversa permite escolher entre template e Direct Send: um formulário para enviar uma mensagem de utilidade sem escolher template, também fora da janela de 24 horas, com até 3 botões de resposta, um botão de link ou um botão para ligar no WhatsApp, cabeçalho de texto, imagem, vídeo ou documento, rodapé opcional e prazo de entrega. A Meta cria os templates por conta própria. Pela API também dá para definir o nome do template e enviar códigos de verificação (mensagens de autenticação) quando a Meta os libera na conta. A Saúde da Conta indica se a caixa provavelmente se qualifica (limite de mensagens de 100.000 ou ilimitado); o switch só aparece nesse caso e o Direct Send se desliga se a caixa deixar de se qualificar. Texto livre continua precisando de template fora da janela. É ativado por caixa de entrada
- **Mensagens interativas do WhatsApp Cloud** *(Mega)* - Enquanto a janela de 24 horas está aberta, o botão de WhatsApp da caixa de resposta e do formulário de nova conversa oferece "Mensagem interativa": um formulário com prévia no estilo WhatsApp para enviar até 3 botões de resposta, uma lista de até 10 opções com descrição, um botão de link, um carrossel de 2 a 10 cartões com imagem ou vídeo, uma cobrança Pix (código copia e cola com valor) ou um pedido de localização, com cabeçalho de texto, imagem, vídeo ou documento e rodapé opcionais. Os arquivos são enviados no próprio formulário ou basta colar uma URL pública. Todos os campos aceitam as variáveis da plataforma (`{{contact.first_name}}`, atributos personalizados etc.). Na conversa elas aparecem como os templates, com cabeçalho, rodapé e botões, a lista pode ser expandida, o carrossel desliza e o Pix permite copiar o código. Também disponíveis pela API de mensagens, Outbound Messages (`type: interactive`), MCP e Mega Assistant, documentadas no Swagger/OpenAPI e no Postman.
- **Mensagens interativas do WAHA** *(Mega)* - As caixas WAHA enviam mensagens interativas a qualquer momento, sem janela de 24 horas: botões de resposta (até 3), botões de ação (abrir link, ligar ou copiar código, até 5), lista, carrossel com imagem por cartão, cobrança Pix (o cliente digita o valor), pedido com "Revisar e pagar" (itens, desconto, total e chave Pix), enquete (uma ou várias respostas), localização, evento com data e local, e resposta a uma mensagem de botões (só por API). O ícone do WhatsApp da caixa de resposta e da nova conversa abre o mesmo formulário com prévia do WhatsApp Cloud, no desktop e no celular, com cabeçalho de texto, imagem, vídeo ou documento. Carrossel, Pix, pedido e evento precisam do motor GOWS. Só em conversas diretas: em grupos a opção não aparece. Na conversa aparecem como os templates, e as respostas do cliente (botão tocado, opção da lista, voto da enquete ou resposta ao evento) chegam como mensagens. Habilitado por servidor WAHA no Super Admin → Provedores WA (interruptor *Mensagens interativas*) ou para toda a instalação com `WAHA_INTERACTIVE_MESSAGES=true`, e por conta com a feature *WAHA Interactive Messages*. Também pela API de mensagens, Outbound Messages e MCP, com os 10 exemplos no Swagger/OpenAPI, no Postman e na documentação da API do Super Admin.
- **Mensagens interativas da UazAPI** *(Mega)* - As caixas UazAPI enviam mensagens interativas a qualquer momento, sem janela de 24 horas, em conversas diretas e grupos: botões de resposta, botões de ação (abrir link, ligar ou copiar código), lista com seções, enquete, carrossel com imagem, vídeo ou documento por cartão, botão Pix, solicitação de pagamento com "Revisar e pagar" (valor, item, fatura, chave Pix, boleto, link de pagamento e PDF anexo), evento com data, local, link e lembrete, e pedido de localização. O ícone do WhatsApp da caixa de resposta e da nova conversa abre o mesmo formulário com prévia, no computador e no celular; os botões aceitam cabeçalho de imagem, vídeo ou documento. Na conversa aparecem como os templates; as respostas do cliente (botão tocado, opção da lista, voto da enquete, resposta ao evento) entram como mensagens que citam a original, e o agente pode enviar ao cliente o status do pedido (pagamento solicitado, em preparação, enviado, entregue, concluído ou cancelado, pago ou pendente) pelo balão da solicitação de pagamento. O adicional pode ser vendido para a conta inteira ou por caixa de entrada: nesse caso cada unidade ativa as mensagens interativas em uma caixa (chave *Mensagens interativas* nas configurações da caixa) e as demais aparecem bloqueadas até comprar outra unidade; o mesmo vale para as interativas do WAHA. Ativa-se por servidor UazAPI em Super Admin → Provedores WA (chave *Mensagens interativas*) ou para toda a instalação com `UAZAPI_INTERACTIVE_MESSAGES=true`, e por conta com a feature *UazAPI Interactive Messages*. Também pela API de mensagens, Outbound Messages, MCP da conta e Mega Assistant, com 11 exemplos no Swagger/OpenAPI, Postman e na documentação da API do Super Admin.
- **Marcar conversas como lidas no WhatsApp (UazAPI)** *(Mega)* - Opção por caixa UazAPI, desativada por padrão, no cartão *Chats* das configurações: quando um agente abre uma conversa com mensagens não lidas ou uma resposta é enviada ao cliente, a conversa fica como lida no celular da linha (o contador de não lidas é zerado). O contato vê os tiques azuis apenas se a conta do WhatsApp tiver as confirmações de leitura ativadas na privacidade.
- **Id da opção escolhida nas respostas do WhatsApp** *(Mega)* - Quando o cliente escolhe uma opção de lista ou toca um botão de resposta (WhatsApp Cloud, WAHA e UazAPI), a mensagem guarda o id com que essa opção foi enviada, além do texto. As integrações que enviam listas ou botões pela API ou por Outbound Messages recebem esse id no webhook e na API de mensagens e sabem exatamente qual opção foi escolhida. Documentado no Swagger/OpenAPI, no Postman e na documentação da API do Super Admin. Os botões de resposta também podem levar um id próprio (`{ id, title }`), não só as listas.
- **Sincronização de contatos** - Mantenha sua base de dados atualizada automaticamente
- **Compartilhar contatos** *(Mega)* - Envie um contato salvo como cartão de contato nativo do WhatsApp pela caixa de resposta (Cloud, WAHA, Uazapi, NotificaMe e Twilio WhatsApp); contatos recebidos são encaminhados com nome e telefone
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
- **Menções no grupo** - Use @ para mencionar membros específicos nas mensagens, inclusive ao editar mensagens de grupos WAHA
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
- **Nomes de contato fiéis** - Preserva o nome fornecido pelo Facebook sem inventar partes ausentes
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

### Comentários do Facebook e Instagram *(Mega)*

Atenda os comentários das suas publicações, reels e anúncios na mesma caixa de entrada onde você já responde as mensagens diretas.

**Funcionalidades principais:**

- **Comentários na conversa** - Cada comentário chega como uma mensagem na conversa de quem o escreveu, junto das mensagens diretas, com o card da publicação (foto, texto e link para abri-la, guardado na plataforma para não se perder), como os anúncios do WhatsApp
- **Resposta pública a partir do comentário** - Responda pelo menu da mensagem («Responder comentário») e a resposta é publicada abaixo dele, visível para todos
- **Mensagem privada** - Leve a conversa para o privado com uma mensagem direta para quem comentou (uma por comentário, em até 7 dias)
- **Moderação** - Oculte, mostre de novo ou exclua comentários sem sair da plataforma
- **API, MCP e Mega Assistant** - Responda em público ou no privado, oculte e exclua comentários pela API (também com `comment_reply` em Outbound Messages, só com o id do comentário), pelo servidor MCP da conta e com o Mega Assistant; tudo documentado em OpenAPI/Swagger e Postman, visível na documentação da API do Super Admin
- **Do comentário para a DM com o Flow Builder** - Um fluxo pode começar a cada comentário (por publicação ou por palavras-chave), e os fluxos de "Mensagem recebida" e os bots também podem atender os comentários; o fluxo pode responder em público, enviar a mensagem privada, ocultar ou excluir o comentário
- **Ativação por caixa** - Cada caixa do Facebook ou Instagram decide se recebe comentários com "Receber comentários de publicações e reels" (desativado por padrão; sem ele, os comentários não entram) e se considera só os comentários principais
- **Conversas para o bot ou para a equipe** - Uma conversa aberta por um comentário fica pendente quando o bot do Flow Builder da caixa inclui comentários; caso contrário, ela é aberta para os agentes

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

- **E-mail mais confiável** - Sem e-mails duplicados quando as buscas IMAP se sobrepõem, nomes de remetente com vírgulas não quebram mais o envio, SMTP sem precisar de IMAP (caixas por encaminhamento) e busca por assunto, que também aparece no cabeçalho da conversa
- **Caixa unificada** - Todos os emails aparecem como conversas junto com WhatsApp, redes sociais e mais
- **Respostas ricas** - Envie emails com formatação, imagens e anexos
- **Arquivos grandes por email** *(Mega)* - O Super Admin define o tamanho máximo de anexo nas respostas de email; o que passa de 20 MB no total chega ao cliente como link de download e o editor avisa o agente
- **Arquivos grandes ao iniciar uma conversa por email** *(Mega)* - A janela de nova conversa usa o mesmo tamanho máximo de anexo das respostas de email, envia os arquivos direto para o armazenamento quando o upload direto está ativo e avisa quando os anexos passam de 20 MB e chegarão como links de download; os anexos também podem ser arrastados e soltos na janela
- **Imagens inline redimensionáveis** - Insira imagens no corpo do email e ajuste o tamanho visualmente
- **Imagens dentro do email** *(Mega)* - As imagens do corpo e da assinatura do agente viajam dentro do email de resposta, então o Outlook e outros clientes que bloqueiam imagens remotas as mostram sem pedir permissão; as que passam do limite continuam como link
- **Tabelas em respostas de email** - Insira uma tabela pelo menu do editor, edite no lugar e envie como uma tabela com bordas que mantém a aparência no Gmail e no Outlook, claro ou escuro
- **Encaminhar por email** - De qualquer mensagem de uma conversa de email, encaminhe para novos destinatários (Para, Cc, Cco) com sua nota, o email original que você pode editar e os anexos que mantiver; sai como um email novo (Fwd:), o contato não recebe e as respostas de cada destinatário abrem a própria conversa. O Encaminhar para contatos de sempre continua igual
- **Assunto personalizado** - As respostas de email mostram um campo Assunto com "Re: <assunto>" (ou o último assunto que você mudou); edite para enviar essa resposta com outro assunto
- **Outros destinatários em CC** - Ao responder um email enviado para várias pessoas, os demais destinatários do campo Para desse email ficam em CC, assim ninguém sai da conversa
- **Assinaturas personalizadas** - Configure assinaturas profissionais por agente ou caixa de entrada
- **Qualquer provedor** - Conecte Gmail, Outlook, seu servidor próprio ou qualquer email
- **Configuração guiada** - Detecta Gmail ou Outlook pelo seu domínio para sugerir a integração correta
- **Verificação de conexão do Gmail** - Teste IMAP e SMTP em tempo real, consulte a atividade recente e reconecte a conta nas configurações da caixa de entrada
- **Exclusão permanente sincronizada com o Gmail** - Ao excluir um email ou conversa de uma caixa Gmail, ele também é excluído permanentemente no Gmail
- **Histórico completo** - Toda a sequência de emails visível em uma só conversa
- **Resposta citada** - Com as respostas citadas ativas na conta, cada resposta de email leva a conversa anterior atrás de uma prévia "…" recolhida sob o editor; remova em uma mensagem e recupere com Cmd/Ctrl+Z. O texto citado do cliente nunca é avaliado como variáveis
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

- **Widget mais leve e privado** - O pedido de e-mail não se duplica mais, crawlers não criam contatos, as páginas públicas não deixam cookie de sessão e o painel não aparece em buscadores
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
- **Dados do contato protegidos** - O widget não recebe o email, o nome nem o telefone salvos do contato: só sabe quais existem, para decidir o que o formulário pré-chat pede. As mensagens enviadas pelo visitante também não levam seus dados.
- **Contatos identificados protegidos** - Quando um visitante digita, no formulário pré-chat ou no pedido de email, um email ou telefone que pertence a um contato identificado pelo seu site, os contatos não são mesclados e o dado não é salvo: os agentes veem uma nota privada na conversa com o dado e um link para o contato correspondente. A mesclagem só acontece quando o visitante chega identificado com o mesmo identificador.
- **Transcrição por email** - Cliente pode solicitar o histórico da conversa; novos envios ficam temporariamente desabilitados após um envio bem-sucedido
- **Modo escuro** - Se adapta às preferências do visitante
- **Mensagens do visitante com formatação** - As listas que o visitante envia mostram seus marcadores e números
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
- **Webhooks do Twilio verificados** - As mensagens e os status que o Twilio envia para SMS e WhatsApp são conferidos com a assinatura do Twilio. Cada caixa de entrada começa apenas registrando e, a partir do primeiro aviso com assinatura válida, rejeita os que chegam sem ela; assim uma configuração que ainda não assina continua funcionando. Caixas conectadas com API Key sem o auth token da conta não são verificadas.
- **Saúde de caixas Twilio WhatsApp** - A saúde da conta também cobre as caixas Twilio WhatsApp: verifica os webhooks de mensagens e voz e mostra o status do remetente do WhatsApp, o nome de exibição, a classificação de qualidade e o limite de mensagens; registrar o webhook também funciona para elas
- **Bandwidth com OAuth** - As caixas de entrada SMS da Bandwidth se conectam com o Client ID e o Client Secret da Bandwidth, verificados antes de salvar. A Bandwidth deixa de aceitar as credenciais de usuário de API em 2 de dezembro de 2026: nas caixas existentes, um administrador deve salvar o Client ID e o Client Secret nas configurações da caixa antes dessa data.
- **Webhooks da Bandwidth protegidos** - A URL de callback de cada caixa da Bandwidth leva um token secreto. Um administrador a copia na aba Configuração da caixa de entrada e a cola na aplicação da Bandwidth. Até a Bandwidth chamar a URL com token pela primeira vez, os avisos sem token continuam sendo aceitos e ficam registrados; a partir daí são rejeitados.
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
- **Validação de identidade (HMAC)** - Nas caixas com validação de identidade obrigatória, cada chamada da API pública sobre um contato (o contato, suas conversas e suas mensagens) deve incluir o `identifier_hash` que assina o identificador desse contato; se faltar ou não corresponder, é rejeitada. Na API da conta, a verificação HMAC é calculada no servidor a partir de `identifier` e `identifier_hash`, e um `hmac_verified` enviado pelo cliente é ignorado.
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
- **Eventos assinados** - Só são aceitos os eventos do X que chegam com uma assinatura válida do app (`TWITTER_CONSUMER_SECRET`); o resto é rejeitado.

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
- **Números ocultos** - Chamadas com identificador de chamada oculto também são atendidas: cada uma cria um contato "Chamador desconhecido" com sua própria conversa, onde os botões de chamada ficam ocultos e só é possível escrever notas privadas
- **Histórico unificado** - Chamadas e mensagens na mesma timeline
- **Gestão de filas** - Gerencie alto volume de chamadas

**Experiência de quem liga e roteamento** *(Mega, aba Voz da caixa de entrada)*:

> **Opcional:** a saudação, o horário de atendimento, o limite de toque e o roteamento de um agente por vez vêm desligados em caixas de entrada existentes e novas; enquanto não forem ativados, as chamadas tocam para todos os agentes que podem vê-las, sem limite de tempo, como antes.

- **Saudação** - Quem liga ouve uma mensagem de boas-vindas, falada no idioma da conta, enquanto os agentes são chamados, e depois música de espera
- **Chamadas só no horário de atendimento** - Com o horário de atendimento da caixa de entrada ativado, uma chamada que chega com a caixa fechada ouve uma mensagem de fora do horário e termina sem tocar para ninguém; ela fica registrada como perdida com a marca "Fora do horário de atendimento". As exceções do horário de atendimento não valem para chamadas
- **Limite de tempo de toque** - Uma chamada não atendida termina depois dos segundos que você escolher (de 10 a 600), quem liga ouve uma mensagem opcional e a chamada fica registrada como perdida
- **Um agente por vez** - As chamadas tocam para um agente livre por vez com a mesma política das chamadas do WhatsApp Cloud: primeiro o responsável pela conversa, depois os agentes online da caixa de entrada em rodízio e por último os administradores que ativaram as notificações de chamadas. O tempo de escalonamento, as tentativas, o que fazer quando o responsável está em outra chamada e o tempo de toque do último agente usam as configurações de chamadas do WhatsApp. Se ninguém puder atender, a chamada termina com a mensagem de chamada não atendida e a marca "Sem agentes disponíveis". A conversa mantém o responsável: não há devolução ao fim da chamada
- **Ocupado em qualquer chamada** - Um agente em uma chamada do Twilio conta como ocupado para as chamadas do WhatsApp, e um agente em uma chamada do WhatsApp conta como ocupado para o roteamento do Twilio
- **Recusas que permanecem** - Cada chamada registra para quem toca. Um agente que recusa deixa de ouvi-la em todas as abas abertas e a chamada não volta ao recarregar; uma chamada que ainda toca para o agente aparece de novo ao recarregar a página (por até uma hora)

**Chamadas de Saída:**

- **Click-to-call** - Ligue para qualquer contato com um só clique
- **Do perfil do contato** - Sem discar números manualmente
- **Erros de chamada claros** - Quando uma chamada não pode começar, o agente vê o motivo, por exemplo um contato sem número de telefone
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
- **Espera e retomada** - O agente na chamada coloca quem liga em espera (ouve música de espera) e retoma a chamada; enquanto isso a chamada mostra "Em espera"
- **Teclado na chamada** - Envie tons do teclado durante uma chamada conectada, para menus telefônicos e ramais; também nas chamadas do WhatsApp Cloud
- **Conversas de chamada abrem em nota privada** - Uma conversa cuja última mensagem é uma chamada abre a caixa de resposta em Nota privada, para anotar sobre a chamada; se mudar para Responder, isso se mantém durante essa visita
- **Transferir chamadas** - Roteie para outro agente ou departamento
- **Só quem atende desliga** - Só o agente que aceitou a chamada pode encerrá-la; uma chamada recebida que ainda está tocando e ninguém aceitou pode ser recusada por qualquer agente da caixa de entrada.

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
- **Atribuição inteligente de agentes** - Chamadas roteadas, uma por vez, para os membros do inbox que estão online, mesmo com a atribuição automática desativada; administradores que ativaram as notificações de chamadas são usados apenas como alternativa
- **Auto-rejeição quando indisponível** - Comportamento configurável
- **Agente atribuído em outra chamada** - Configurável por inbox: a chamada toca para outro agente disponível (padrão) ou só para o agente atribuído. Se o mesmo contato ligar de novo durante uma chamada em andamento, essa chamada não é interrompida
- **Chamadas só no horário de atendimento** - Opcional por inbox nas configurações de chamadas: com o horário de atendimento da caixa de entrada ativo, o WhatsApp só permite que os clientes liguem dentro desse horário, no fuso horário da caixa, e a pausa do almoço fica fechada. Se a Meta rejeitar o horário, as configurações de chamadas são salvas mesmo assim e o motivo aparece abaixo da chave
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
- **Conectividade adaptativa** - Usa servidores STUN/TURN configurados para chamadas premium quando uma rede restrita impede uma conexão direta
- **Atribuição protegida** - Da aceitação até o encerramento da chamada, não é possível alterar o agente nem a equipe da conversa; enquanto ela apenas toca, a reatribuição continua disponível
- **Mute/Unmute** - Alterne o microfone durante chamadas
- **Teclado na chamada** - Envie tons do teclado durante a chamada, para menus telefônicos e ramais (WhatsApp Cloud e Twilio; não WAHA)
- **Duração da chamada** - Timer em tempo real visível
- **Só quem atende desliga** - Só o agente que fez ou atendeu a chamada pode encerrá-la; uma chamada recebida que ninguém atendeu pode ser encerrada por qualquer pessoa que vê a conversa.
- **Áudio no servidor (beta)** - Ativado por conta no Super Admin (feature "Voice Engine") quando a instalação tem o motor implantado; a conta não pode ativá-lo sozinha e, uma vez ativo, vale para as caixas do WhatsApp Cloud e WAHA: o motor de voz do Mega atende a chamada, então recarregar a página do agente não derruba mais o cliente e o agente volta para a chamada
- **Música de espera** - Com o áudio no servidor, cada caixa do WhatsApp Cloud escolhe o que o cliente ouve em espera: uma de cinco melodias incluídas ou um arquivo de áudio próprio (MP3, WAV, OGG ou M4A, até 10 MB e 10 minutos), com player de prévia nas configurações
- **Transferência de chamadas** - Com o áudio no servidor, o agente na chamada a passa para outro agente disponível da caixa (com busca por nome) sem derrubar o cliente: o cliente ouve a música de espera enquanto a chamada toca para o outro agente (em todas as suas abas e dispositivos, mostrando quem transfere). Se ele atender, a chamada e a conversa passam para ele; se recusar, não atender em 30 segundos ou o primeiro agente cancelar, o cliente volta para o primeiro agente
- **Transferência consultiva** - Antes de passar a chamada, o agente pode consultar outro agente: o cliente ouve a música de espera enquanto os dois agentes conversam, e depois o primeiro agente transfere a chamada ou volta para o cliente. Se o outro agente recusar, não atender em 30 segundos ou desligar a consulta, o cliente volta para o primeiro agente
- **Gravação de chamadas no servidor** - Com o áudio no servidor cada chamada atendida é gravada no servidor, com os dois lados (incluindo a música de espera e o agente para quem a chamada foi transferida), e fica na conversa como nota privada com o áudio, igual às outras gravações de chamadas. Recarregar a página ou transferir não a interrompe
- **Áudio no servidor no WAHA** - Com a feature ativa, as caixas WAHA também usam o áudio no servidor: as chamadas recebidas e efetuadas passam pelo motor de voz do Mega, então o agente volta para a chamada após recarregar e pode colocar o cliente em espera com a música da caixa e transferir a chamada (direta ou depois de consultar outro agente). Podem existir várias chamadas WAHA em andamento ao mesmo tempo. A gravação continua sendo feita pelo WAHA
- **Menu de chamadas (URA)** - Um fluxo do Flow Builder que começa com "Chamada recebida" atende as chamadas de WhatsApp (Cloud ou WAHA) de uma caixa com áudio no servidor como um menu telefônico: o cliente ouve áudios que a conta enviou (MP3, WAV, OGG ou M4A) ou gerou com IA a partir de um texto, escolhendo o modelo de fala e a voz entre os provedores de IA da conta (reutilizáveis entre fluxos; gerados uma vez ao salvar, e de novo se o texto, o modelo ou a voz mudar), digita uma tecla ("digite 1 para vendas, 2 para suporte") e o fluxo transfere a chamada para toda a caixa ou uma equipe, toca outro áudio ou desliga. Pergunta de novo após uma tecla errada ou silêncio, e as verificações de horário de atendimento e agentes disponíveis funcionam nesses fluxos. Se nenhum agente estiver livre, a chamada pode esperar numa fila com a música de espera e tocar para o primeiro agente que ficar livre, na ordem em que as chamadas chegaram, até uma espera máxima definida no bloco. Cada passo aparece nas execuções do fluxo As caixas de voz do Twilio também podem usar o menu: tocar áudios, pedir uma tecla, transferir para toda a caixa ou uma equipe e desligar (sem fila de espera nem IA por enquanto).
- **IA nas chamadas** - Em um fluxo de chamadas, "Atender com IA" coloca um agente de IA para conversar com o cliente em tempo real e resolver a chamada sozinho: mantém uma conversa natural, responde com o assistente do Captain da caixa (seu conhecimento e ferramentas) ou com instruções escritas no bloco, e passa para uma pessoa só quando o cliente pede ou não consegue ajudar. Na saudação avisa que é um assistente virtual (ativado por padrão). O que foi falado fica na conversa como nota privada. "Perguntar por voz" permite responder a um menu falando ("vendas ou suporte?") em vez de digitar teclas, que é como os menus funcionam no WAHA; responde à saudação e confirma a opção com uma frase gentil ("Claro, com prazer, um momento") antes de passar a chamada, e o agente de IA seguinte já atende no idioma em que o cliente falou. Cobrado em AI Actions a cada 5 minutos de conversa
- **Otimização VoIP** - Áudio otimizado para chamadas de voz

**Histórico de Chamadas:**

- **Registro completo** - Todas as chamadas registradas na conversa
- **Metadados detalhados** - Duração, status, timestamps
- **Indicador de direção** - Entrada vs saída claramente marcados
- **Rastreio de status** - Atendida, perdida, rejeitada, etc.
- **Retornar ligação** - A última chamada perdida ou com falha mostra a linha por onde entrou e um botão para retorná-la pelo chat

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

### Chamadas WhatsApp WAHA *(Mega)*

Receba e faça chamadas de voz do WhatsApp no MEGA com números conectados pelo WAHA, usando o mesmo widget de chamadas do WhatsApp Cloud.

**Disponibilidade:**

- Habilitado por instalação com `WAHA_VOICE_CALL=true` ou por servidor WAHA no Super Admin → Provedores WA (interruptor *Chamadas de voz*); servidores não compatíveis não mostram nada
- Depois é ativado por conta (feature *WAHA Voice Calls*) e por caixa nas configurações da sessão → Apps → *Chamadas de voz*

**Chamadas Recebidas:**

- **Mesmo widget do Cloud** - Aviso em tempo real, atender ou recusar pelo navegador e atribuição ao agente da conversa ou por round-robin
- **Mesmas configurações de chamada do Cloud** - Em Apps → *Chamadas de voz* → *Configurações de chamadas*: escalar para o próximo agente, o que fazer se o agente atribuído estiver em outra chamada (tocar para outro agente disponível ou só para o atribuído), auto-rejeição e mensagens de indisponibilidade
- **A conversa volta para o dono** - Quando uma chamada toca para outro agente porque o responsável está em outra chamada ou não atendeu, a conversa mostra para quem foi e por quê, e volta ao agente responsável ao terminar a chamada
- **Chamadas de grupo recusadas** - Só chamadas diretas chegam aos agentes
- **Histórico na conversa** - Cada chamada fica como mensagem: concluída com sua duração, não atendida ou recusada
- **Gravação automática** - O WAHA grava as chamadas atendidas (recebidas e realizadas) e a gravação é anexada à conversa como nota privada

**Chamadas Realizadas:**

- **Click-to-call** - Botão de chamada no painel do contato (ou no seletor de métodos quando a caixa tem vários)
- **Uma chamada por agente** - Não permite iniciar uma segunda chamada enquanto há uma ativa
- **Chamadas não atendidas terminam sozinhas** - Se o WAHA nunca avisar o fim de uma chamada não atendida, o Mega a encerra após 2 minutos e o agente pode fazer a próxima

**Segurança:**

- O navegador não recebe nenhuma credencial do WAHA: o Mega negocia o áudio com o WAHA e o agente só pode abrir o áudio da chamada que atendeu ou iniciou
- Só o agente que fez ou atendeu a chamada pode encerrá-la; uma chamada recebida que ninguém atendeu pode ser encerrada por qualquer pessoa que vê a conversa

**Requisitos:**

- Servidor WAHA com engine GOWS, app `voice-calls` e WebRTC habilitado (`WAHA_CALLS_WEBRTC_PUBLIC_IP` e a porta UDP aberta; no Docker Swarm, publicada com `mode: host`)
- Navegador moderno com suporte a WebRTC, em HTTPS

---

## 💬 Gestão de Conversas

### Caixa de Entrada Inteligente

- **Visão unificada** - Todas as conversas em um só lugar
- **Filtros avançados** - Por status, caixa de entrada, agente, equipe, etiquetas
- **Atributos numéricos** - Os atributos personalizados numéricos são filtrados por igual, diferente, presente, maior ou menor; se você escolher *Contém*, o filtro avisa em vez de falhar
- **Ordenar resultados filtrados** - Os resultados de filtros avançados e as pastas podem ser ordenados como a lista normal (mais recentes, mais antigas, prioridade, tempo de espera)
- **Filtros de data no seu horário local** - Os filtros por data de criação ou de última atividade usam o dia do seu fuso horário, como os relatórios, e os contadores de um filtro não voltam mais a mostrar os totais gerais
- **Indicador de anexos em e-mails** - Conversas de e-mail mostram um 📎 na lista quando o cliente enviou arquivos, com tooltip de quantidade e tipos (ex. "2 anexos: CDR, PDF"); imagens inline de assinatura não contam e o filtro **Anexos de e-mail** as segmenta
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
- **Uma conversa ativa por contato** - Se o contato já tem uma conversa aberta ou pendente no mesmo inbox, não é possível reabrir nem responder uma resolvida: o sistema indica a conversa ativa para continuar nela. A busca mostra o status de cada conversa com sua cor

### Priorização

- **Níveis de prioridade** - Urgente, Alta, Média, Baixa
- **Ordenação inteligente** - Por atividade recente, tempo de espera, prioridade
- **Ordenação por não lidas** - Priorize conversas com mensagens não lidas diretamente no seletor de ordenação
- **Indicadores visuais** - Identifique rapidamente conversas críticas
- **Contagem regressiva da janela de resposta** - No WhatsApp Cloud, 360dialog, NotificaMe e nos outros canais com janela de resposta (Messenger, Instagram, TikTok, WhatsApp via Twilio, API com tempo de resposta), o cabeçalho da conversa mostra "Janela aberta · fecha em 3 h 12 min" com o horário exato ao passar o mouse, e cada cartão da lista mostra o tempo restante: âmbar com menos de 2 horas, vermelho ao fechar. Se fechar com a conversa aberta, o editor passa sozinho para modelos de mensagem

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

### Atalhos do editor de resposta

- Os atalhos de envio não acumulam ações duplicadas ao alternar entre conversas. As preferências de Enter/Ctrl/Cmd+Enter e o fechamento de menções com Escape são preservados.
- Digitar "/" na caixa de resposta ou em qualquer outro campo de texto da página de busca fica nesse campo; "/" só pula para a caixa de busca quando nenhum campo de texto está em foco.
- Os seletores de respostas prontas e macros mantêm a opção destacada quando a lista é atualizada em segundo plano.

### Caixa de resposta recolhível

- No desktop e no tablet, a caixa de resposta pode ser recolhida para dar mais espaço à leitura da conversa: pelo botão de recolher ao lado do botão de expandir, ou arrastando a alça de redimensionamento abaixo da altura mínima.
- Uma barra fina fica embaixo com **Responder** e **Mensagem Privada** (Alt+L / Alt+P, ⌥ no Mac); ela mostra "Rascunho não enviado" quando há texto ou anexos pendentes. Responder a uma mensagem, inserir conteúdo, uma ação do Captain ou colar um arquivo também reabrem a caixa.
- O rascunho, os anexos e o modo escolhido são mantidos enquanto ela está recolhida. A escolha é lembrada para o agente em todas as conversas e dispositivos.
- No celular, o compositor flutuante de uma linha é mantido e nunca é recolhido.

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
- **Estado de leitura em lote** - Marque as conversas selecionadas como lidas ou não lidas, inclusive em seleções grandes
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

### Flow Builder *(Mega)*

Crie conversas automáticas com blocos que mostram o que o cliente vai receber, no estilo ManyChat.

- **Cartões com prévia** - Cada bloco mostra no canvas o conteúdo real: o texto com as variáveis como etiquetas, anexos, template e um botão por linha
- **Edição no painel lateral** - Ao tocar em um bloco, ele é editado em um painel à direita sem esconder o fluxo; sem seleção, o painel mostra a biblioteca de blocos com busca
- **Opções com saída própria** - Enviar mensagem aceita até 10 opções; cada uma abre seu próprio caminho e o cliente pode responder com o número ou o texto da opção. Uma resposta que não corresponde segue por "Outra resposta"
- **Se a resposta não for válida** - Uma mensagem com opções pode perguntar de novo quando o cliente responde algo que não é uma opção (texto, imagem, áudio ou uma localização não pedida): envia uma mensagem própria, se quiser reenvia as opções e espera de novo, de 1 a 5 vezes; depois segue por "Outra resposta". A resposta inválida não é salva no campo do contato
- **Voltar a um bloco** - Um caminho pode voltar a um bloco anterior (o menu, por exemplo) com uma conexão ou com o bloco "Voltar a um passo deste fluxo", que escolhe o passo em uma lista com busca e o destaca na tela, desde que passe por uma mensagem que espera a resposta do cliente; assim o fluxo nunca se repete sozinho
- **Três formas de enviar a mensagem** - No topo do painel escolhe-se "Texto", "Interativa" ou "Modelo". "Texto" (padrão, em qualquer canal) escreve as opções abaixo da mensagem como "🔷 1 - Consultórios Médicos", com marcador e numeração ("1 -", "1." ou "1)") à escolha. "Interativa" usa o mesmo formato e os mesmos campos do formulário de interativos da conversa, com todos os tipos: botões de resposta, lista, link, botões de ação, pedido de localização, carrossel, enquete, Pix, pedido, solicitação de pagamento, evento, localização e botão para ligar no WhatsApp (Direct Send), com o cabeçalho de texto ou arquivo e o rodapé que cada provedor oferece. Só aparece, e só com os tipos do seu provedor, onde alguma caixa do início pode enviar interativos (WhatsApp Cloud, ou WAHA/UazAPI com as mensagens interativas ativas no servidor, na conta e na caixa); com todas as caixas, enquanto alguma puder. Botões, linhas, respostas rápidas do carrossel e respostas da enquete abrem um caminho cada (a enquete segue com o primeiro voto do cliente), o pedido de localização sai por "Localização recebida" e os tipos que não esperam resposta seguem na hora. Um bloco interativo numa caixa sem interativos é sinalizado no painel e no cartão ("Será enviada como texto", com "Passar para texto") e sai como texto com o cabeçalho em negrito, as opções, o rodapé e o arquivo do cabeçalho. "Modelo" aparece onde o Reply Box oferece modelos em alguma caixa do início (modelos da Meta da caixa ou modelos de conteúdo do Twilio); se várias os oferecem, primeiro escolhe-se a caixa. Escolhe-se o modelo aprovado, o arquivo do cabeçalho, as variáveis e os parâmetros dos botões, e cada resposta rápida do modelo abre seu próprio caminho
- **O bot espera a resposta** - O fluxo para na mensagem e continua quando o cliente responde; pode salvar a resposta em um atributo personalizado do contato
- **Sem resposta** - Se o cliente não responder no tempo escolhido, o fluxo segue pela saída "Sem resposta"
- **As mesmas variáveis de toda a plataforma** - "+ Variável" oferece as variáveis de campanhas, respostas rápidas e Reply Box (`{{contact.first_name}}`, `{{contact.phone}}`, `{{agent.name}}`, `{{inbox.name}}`, atributos personalizados) com os mesmos valores, mais os dados do fluxo (última mensagem). Funcionam no texto, nas opções, em todos os campos do interativo e nas variáveis de modelo
- **Prévia ao vivo** - O topo do painel mostra a mensagem como o cliente vai recebê-la (texto com opções, balão interativo ou modelo) com as variáveis preenchidas com dados de exemplo, e no celular cada seção abre em sua própria tela
- **Gravar áudio** - O bloco grava uma mensagem de voz com o mesmo gravador do Reply Box e permite ouvi-la, gravar de novo ou removê-la. Se o bloco também tem texto, a mensagem de voz sai primeiro e o texto com as opções numa mensagem separada
- **Testar como chat** - Simula a conversa no painel tocando nos botões e escolhendo o caminho de cada condição; nada é enviado ao cliente. O teste com uma conversa real continua no menu
- **Blocos** - Enviar mensagem, Condição, Conforme o valor, Esperar, Dividir aleatoriamente, Percorrer uma lista, Voltar a um passo deste fluxo, Iniciar outro fluxo, Requisição HTTP, Ações, Kanban, Buscar cards, Tarefa, Evento, Avisar a equipe, Transferir para um agente, Responder com Captain, Encerrar e, em Avançado, Código. Encerrar termina o fluxo sem resolver a conversa: para resolvê-la, coloque antes a ação Resolver
- **Condições legíveis** - Lidas como uma frase ("Se as etiquetas da conversa incluem vip") e combinam várias regras com Todas ou Alguma, com saídas Sim e Não. O campo diz a que pertence ("Conversa · Status", e os atributos personalizados dizem se são do contato ou da conversa) e o valor é escolhido em uma lista com dados reais: status, prioridades, etiquetas da conta, equipes, agentes, etapas do funil com sua cor e as opções dos atributos de lista; o texto livre (ou uma variável) fica para os campos de texto, e os operadores mudam conforme o campo. Também perguntam se a caixa de entrada está no horário, quantos agentes estão online (na caixa ou em uma equipe), quais tarefas a conversa tem, em qual funil e etapa, status ou etiquetas está o card, e se a última mensagem traz um anexo
- **Ações em ordem** - Um bloco Ações organiza a conversa com uma ou várias ações de Automation (atribuir, etiquetar, prioridade, status, notas, aplicar um SLA quando a conta tem SLA ativo, enviar um e-mail para equipes, participantes, webhook), de cima para baixo. Kanban, enviar mensagens ou arquivos e responder comentários agora têm bloco próprio: as linhas salvas continuam funcionando e, quando são a única ação do bloco, o painel oferece convertê-las. Se uma ação falhar, as outras rodam do mesmo jeito e o bloco sai por "Se uma ação falhar" quando essa saída está conectada; buscar "esperar" ou "estado" no seletor indica o bloco Esperar e as ações de status
- **Aguardar** - Pausa o fluxo por minutos, horas ou dias antes de continuar
- **Dividir aleatoriamente** - Distribui os contatos entre caminhos por porcentagem
- **Conforme o valor** - Compara um valor (com variáveis) com vários casos em ordem, com os mesmos campos, listas de valores e operadores da Condição, e segue pelo primeiro que corresponde ou por "Nenhum corresponde"; cada caso pode ter nome e ser reordenado, e suas saídas mostram o nome da equipe, do agente ou da etapa
- **Blocos antigos que continuam funcionando** - Horário de atendimento, Agentes disponíveis, Etapa Kanban e Tem tarefa aberta? agora são linhas da Condição; Atualizar tarefa e Reagendar ou cancelar evento, opções de Tarefa e Evento; e Avisar no chat interno, a opção Sala do chat de Avisar a equipe. Eles não estão mais na biblioteca, mas os fluxos que os usam continuam funcionando igual. No painel, "Converter em Condição" (ou em Tarefa, Evento ou Avisar a equipe) passa o bloco para o novo mantendo suas conexões; nada é convertido sozinho
- **Percorrer uma lista** - Repete um caminho para cada item de uma lista (uma variável com uma lista ou texto separado por vírgulas ou linhas), com o item atual, seu número e o total como variáveis em mensagens, campos e condições; o caminho volta ao bloco e, ao terminar, segue por "Concluído". O painel oferece as listas dos blocos anteriores (os cards de Buscar cards, as assinaturas ou faturas do Stripe) e as etiquetas da conversa. Até 25 itens por volta, também em "Testar"
- **Código (JavaScript)** - No grupo Avançado da biblioteca, executa JavaScript com os dados do fluxo (contato, conversa, última mensagem, caixa de entrada, agente, item da lista e resultados anteriores) e guarda o objeto que ele retorna com um nome (por exemplo `codigo1`), lido depois como `{{ vars.codigo1.chave }}` em mensagens, campos e condições. Roda isolado, sem rede, arquivos nem temporizadores, com limites de 1 segundo, 32 MB, 10.000 caracteres e 32 KB de resultado; se falhar, segue por "Erro". Em "Testar" você escolhe se deu certo e digita um resultado de exemplo. Só aparece se o servidor tiver o motor de JavaScript instalado
- **Requisição HTTP** - Chama uma API: primeiro você escolhe o método (GET, POST, PUT, PATCH ou DELETE) e a URL e depois, se precisar, uma credencial salva, parâmetros, cabeçalhos e corpo JSON ou texto, todos com variáveis. Guarda a resposta com um nome (por exemplo `respuesta1`), lida depois como `{{ vars.respuesta1.status }}` ou `{{ vars.respuesta1.body.campo }}`; depois de "Testar requisição", os próximos blocos já podem escolher os campos da resposta. Segue por "Sucesso" com uma resposta 2xx e por "Erro" nos demais casos. Endereços de rede privada são bloqueados, espera até 30 segundos e aceita respostas de até 1 MB. "Testar requisição" a envia na hora com dados de exemplo; nos testes do fluxo só as GET são enviadas
- **Conexões** - Guardam uma vez a URL base, a autenticação (Bearer, Básica ou API key) e os cabeçalhos de uma API para qualquer bloco Requisição HTTP. Os segredos ficam criptografados e nunca são mostrados de novo; só administradores as gerenciam, pelo Flow Builder ou pelo próprio bloco. Uma conexão usada por algum fluxo não pode ser excluída
- **Respostas fora do histórico** - Com "Não guardar a resposta no histórico", os próximos blocos leem a resposta de uma Requisição HTTP durante a execução e, ao terminar, o corpo fica salvo como [redacted] no histórico de execuções. A instalação também pode definir por quantos dias as execuções terminadas são guardadas (por padrão, para sempre)
- **Responder com Captain** - Passa a conversa para o assistente do Captain da caixa de entrada e o fluxo termina; o painel avisa quando uma caixa do início não tem assistente
- **Transferir para um agente** - Em "Para quem?" você escolhe se a conversa fica para a caixa de entrada (com suas regras de atribuição), para uma equipe ou para um agente da caixa. Com "Encerrar o fluxo", ativo nos blocos novos, o fluxo termina ali; desativado, segue depois de transferir. Os blocos salvos antes continuam como estavam
- **Kanban** - Cria o card da conversa, move de etapa (executando as automações da etapa), marca como ganho, perdido ou aberto ou o exclui; também atribui um agente, adiciona uma nota e adiciona, remove ou substitui as etiquetas dele. "Sobre qual card?" escolhe o card da conversa (se quiser, o que ela tem em um funil, uma etapa, um status ou com algumas etiquetas), o card que iniciou o fluxo, o card do percurso ou, no modo avançado, outro card a partir de uma variável; sem card sai por "Sem card". Dentro de um percurso, excluir pede confirmação. Aparece só com Kanban ativo
- **Buscar cards** - Busca os cards da conta por funil, etapa, status, etiquetas, horas na etapa ou mudança de status recente, até 100 (20 por padrão), primeiro os que estão há mais tempo na etapa, e segue por "Com cards" ou "Sem cards". Com Percorrer uma lista cada card é trabalhado; não precisa de conversa, então serve em um fluxo Agendado
- **Iniciar outro fluxo** - Inicia outro fluxo publicado da conta na conversa de um card (por exemplo o do percurso) ou nesta, com dados de entrada que o outro fluxo lê como `{{ inputs.chave }}`, e segue sem esperar. O fluxo chamado começa no bloco depois do seu início, sem olhar as condições desse início. As execuções dizem se o outro fluxo foi pedido, pulado (não havia conversa ou o card não foi encontrado) ou recusado porque já havia fluxos demais chamando uns aos outros
- **Pergunta Sim/Não ao Captain** - No grupo Captain e IA, o Captain responde Sim ou Não a uma pergunta lendo a última mensagem e a conversa; usa créditos do Captain e tem saída própria quando não consegue responder. Em "Testar" a IA não é consultada: quem testa escolhe o ramo
- **Atualizar contato ou conversa** - Altera nome, email, telefone e atributos personalizados do contato ou da conversa, com variáveis
- **Executar macro** - Executa uma macro pública como o agente que a criou; "Criar macro" abre Configurações → Macros em outra aba e a lista recarrega ao voltar
- **Tarefa e Evento** - Tarefa cria uma atividade (com prazo e prioridade e, se quiser, vinculada ao card) ou conclui, cancela ou reabre uma; Evento agenda um evento de calendário (com duração e, com o Google Agenda conectado, link do Meet) daqui a um tempo, em uma data fixa ou na data de uma variável, ou o reagenda ou cancela. O que eles criam lembra do fluxo, então um bloco de uma execução posterior encontra a tarefa ou o evento que este fluxo deixou na conversa; se não houver, sai por "Não encontrada" ou "Não encontrado". São criados para um Responsável: o atribuído da conversa, um agente fixo ou um rodízio por equipe ou lista de agentes (opcionalmente só online), com um agente reserva
- **Agendar mensagem** - Deixa agendada uma mensagem da conversa, com arquivos e variáveis, para depois de um tempo ou para uma data e hora com seu fuso horário (escolhidas no calendário ou tiradas de uma variável), uma vez ou repetida como em Mensagens agendadas. É enviada em nome do agente escolhido (o atribuído da conversa, um fixo ou um rodízio, com reserva) e aparece em Mensagens agendadas, onde a equipe pode editá-la ou cancelá-la. Se a data não servir ou a mensagem não puder ser agendada, sai por "Erro" quando essa saída está conectada. Requer a função de mensagens agendadas
- **Cancelar mensagens agendadas** - Cancela as mensagens agendadas da conversa que ainda não foram enviadas, incluindo as que se repetem: "Só as deste fluxo" (assim começam os blocos novos) ou "Todas as pendentes", inclusive as que os agentes agendaram manualmente. Segue por "Canceladas" ou por "Nenhuma pendente". Requer a função de mensagens agendadas
- **Pedir CSAT** - Envia a pesquisa de satisfação da caixa de entrada com as mesmas regras (conversa resolvida, CSAT ativo, uma única vez por conversa, modelo ou janela de resposta) e segue por "Enviada" ou por "Não enviada" com o motivo, que uma Condição pode ler. Com "Resolver antes", primeiro resolve a conversa se ela ainda não estiver resolvida. Aparece só se a caixa do fluxo tiver o CSAT ativo
- **Adicionar participante** - Ação do bloco Ações: adiciona um agente como participante da conversa, como o painel de participantes (o agente recebe a notificação); um agente sem acesso à caixa fica como erro e as demais ações seguem
- **Nota do contato** - Ação do bloco Ações: adiciona uma nota ao contato, como o painel de notas do contato, com variáveis do fluxo e da plataforma; se o texto ficar vazio fica como erro e as demais ações seguem
- **Associar empresa** - Busca a empresa pelo domínio (ou pelo nome exato quando não há domínio), cria se não existir e associa o contato a ela, como o painel de contatos da empresa; o domínio pode vir de um site ou de um e-mail, com variáveis. Segue por "Encontrada" ou "Criada". Aparece só se a conta tiver Empresas ativo
- **Buscar contato** - Busca outro contato da conta por e-mail, telefone, identificador ou um atributo personalizado (valor fixo ou com variáveis), com as mesmas regras do filtro de Contatos. Segue por "Encontrado", com os dados no grupo "Resultados" do seletor de variáveis, ou por "Não encontrado"
- **Checklist do card** - O bloco Kanban adiciona um item ao checklist do card ou marca como feito o primeiro item aberto com esse texto, como o checklist do card, com variáveis; o painel oferece os itens que as etapas dos funis adicionam aos seus cards. Sem card sai por "Sem card"; sem esse item o fluxo segue. Aparece só com Kanban ativo
- **Escolher opção com IA** - O Captain lê a última mensagem e a conversa e escolhe entre 2 e 10 opções descritas em linguagem natural; cada opção tem sua saída, mais "Nenhuma" e "Não conseguiu responder" (também sem créditos). Usa créditos do Captain; em "Testar" a IA não é consultada: quem testa escolhe a opção
- **Sugerir etiquetas ou prioridade com IA** - O Captain lê a conversa e, como as sugestões da barra lateral, escolhe até 3 etiquetas da conversa ou do contato, ou a prioridade; o fluxo as aplica e segue, ou sai por "Não conseguiu responder" (também sem créditos). Em "Testar" a IA não é consultada
- **Resumir conversa** - O Captain escreve um resumo da conversa (como a opção Resumir do editor) que os próximos blocos leem como variável em "Resultados" e, se ativado, o adiciona como nota privada; sai por "Não conseguiu responder" sem créditos ou se o Captain falhar. Em "Testar" é usado um resumo de exemplo
- **Traduzir** - O Captain traduz um texto com variáveis (por exemplo a última mensagem) para o idioma escolhido ou para o idioma do contato (o detectado na conversa), como a ação Traduzir de uma mensagem, e os próximos blocos leem a tradução em "Resultados"; sai por "Não conseguiu responder" sem créditos ou se o Captain falhar. Só aparece quando a tradução automática está ativa e o Captain é o serviço de tradução da conta. Em "Testar" é usada uma tradução de exemplo
- **Ferramenta do Captain** - Chama uma ferramenta personalizada do Captain (endereço, autenticação e templates) com parâmetros fixos ou com variáveis e deixa a resposta em "Resultados"; segue por "Sucesso" ou "Erro". O painel marca os parâmetros obrigatórios e o tipo deles, e se um ficar vazio a ferramenta não é chamada e o bloco sai por "Erro". Só em caixas de entrada com assistente do Captain; não oferece ferramentas desligadas, com e-mail verificado nem de alto risco. Nos testes e em "Testar" não é chamada: quem testa escreve uma resposta de exemplo
- **Extrair dados do contato com IA** - O Captain lê o contato e a conversa com o assistente da caixa de entrada, como a memória dele faz: no modo Atributos sugere os dados que a conversa menciona e que o contato ainda não tem, e os próximos blocos os leem em "Resultados"; você pode limitá-los a uma lista fechada de atributos e, com "Salvar no contato", gravá-los no contato; no modo Notas escreve notas do contato. Sai por "Não conseguiu responder" sem créditos, sem assistente ou quando o Captain falha. "Testar" nunca pergunta à IA
- **Consultar cliente no Stripe** - Com o Stripe conectado em Integrações, procura o e-mail do contato no Stripe da conta, como a barra lateral da conversa, e os próximos blocos leem o nome, e-mail, telefone, id e status da última assinatura do cliente em "Resultados"; sai por "Encontrado", "Não encontrado" (sem e-mail ou sem cliente) ou "Erro" (o Stripe falhou ou a chave precisa ser reconectada). Os testes e o "Testar" nunca chamam o Stripe
- **Passar para Typebot / Dialogflow** - A conversa passa para um dos bots do Typebot da conta (atribuída como quando um agente atribui um bot, pendente, com a mensagem do cliente) ou para o agente do Dialogflow conectado à caixa de entrada (fica pendente, com a mensagem do cliente), e o fluxo termina: daí em diante o bot responde. Mostra só os bots que a conta tem ativos, e o painel nomeia as caixas do início que não têm Dialogflow. Os testes e o "Testar" não mudam nada
- **Avisar a equipe** - Em "Como avisar?" você escolhe Notificação ou Sala do chat. Notificação envia a um agente (por padrão o responsável da conversa, um agente escolhido ou um rodízio, com reserva) um aviso sobre a conversa com um texto com variáveis: aparece nas notificações dele e sai por push e e-mail conforme as configurações de notificação dele (preferência "Um fluxo envia um aviso para você", push ativo por padrão); o agente precisa poder ver a conversa, senão a etapa falha. Sala do chat publica a mensagem em uma das salas do chat da conta em nome desse agente, que precisa ser membro da sala. O fluxo continua logo em seguida. Os testes e o "Testar" não avisam ninguém
- **Videochamada Dyte** - Inicia uma videochamada do Dyte na conversa como o botão de videochamada da caixa de resposta, em nome de um agente (por padrão o responsável da conversa), e sai por "Erro" quando o Dyte não consegue criá-la. Só em caixas de entrada de site e API com o Dyte conectado; o painel nomeia as caixas do início onde não funciona. Os testes e o "Testar" não criam nenhuma reunião
- **Ler dados da conta (avançado)** - Lê o que nenhuma variável nem outro bloco traz (as conversas e notas de um contato, uma conversa, as mensagens dela com tipo, remetente e se são privadas, as etiquetas, as respostas prontas ou uma busca de empresas) em nome de um agente escolhido que pode usar o assistente Mega, e os próximos blocos leem a resposta em "Resultados". Em "De qual contato?" ou "De qual conversa?" você escolhe o do fluxo ou uma variável, sem digitar ids. Nada é alterado nem apagado, e os blocos salvos com outras leituras continuam funcionando. Só administradores editam fluxos. Os testes e o "Testar" não executam nada
- **Só blocos disponíveis** - A biblioteca mostra só os blocos cujo recurso está ativo na conta (Kanban, atividades, agenda, macros, Captain); se um recurso for desligado depois, o bloco avisa no painel e sua etapa falha sem repetir o que veio antes
- **Janela de 24 horas** - Fora da janela de atendimento do WhatsApp (e do Messenger e Instagram) uma mensagem que não é modelo não é enviada: o bloco sai por "Janela fechada" se estiver conectada ou o fluxo termina ali
- **Uma vez por conversa** - Um início por eventos pode ser limitado para que o fluxo não recomece a cada mensagem (ativo nos fluxos novos); no modo Agente bot o fluxo responde cada mensagem
- **Pausa quando uma pessoa intervém** - Se um agente responde ou a conversa é resolvida, o fluxo que estava aguardando é cancelado
- **Organizar** - Organiza o fluxo automaticamente da esquerda para a direita
- **No celular** - O fluxo é lido como uma lista de passos agrupada por botão ou condição, e cada bloco é editado em uma folha inferior
- **Rascunhos e publicação versionada** - Edite sem afetar a versão publicada; as conversas que estão aguardando seguem com a versão em que começaram
- **Ativação e pausa por switch** - Ative ou pause fluxos publicados na lista ou no editor; ao pausar, as conversas que estavam aguardando são canceladas
- **Validação antes de publicar** - Detecta ciclos que não esperam a resposta do cliente nem são o caminho de volta de Percorrer uma lista, conexões quebradas, botões com mais de 20 caracteres, divisões que não somam 100 e blocos incompletos. O aviso nomeia o bloco e "Ver bloco" o abre; os blocos com avisos ficam marcados na tela. Uma saída conectada a dois blocos é um erro (só o primeiro seria seguido); ao conectar uma saída que já tem destino, a conexão passa para o novo bloco. Avisa dos blocos que nenhum caminho a partir do Início alcança (contando Ir para bloco). Deixar "Outra resposta" de uma mensagem com opções em texto, ou "Sem resposta" de uma mensagem com tempo de espera, sem conexão é só uma sugestão no próprio bloco
- **Quatro tipos de início** - O Início é um Evento (começa quando algo acontece: uma mensagem, uma mudança na conversa, um comentário ou um card atualizado), um Agente bot (o fluxo é o bot das suas caixas de entrada e responde cada mensagem até passar a conversa para a equipe), Agendado (roda nos horários que você escolher, sem conversa) ou Webhook (roda quando um CRM ou formulário externo envia dados para a URL própria do fluxo). Cada tipo é explicado em uma linha com um exemplo, e os filtros finos ficam em uma Condição depois do início
- **Início Agendado** - Roda a cada tantos minutos (a partir de 5), horas, dias ou semanas em um horário, ou com uma expressão cron, no fuso horário de relatórios da conta, e mostra as próximas execuções enquanto você o configura. Um horário que não foi cumprido (o servidor estava fora do ar ou a execução anterior ainda estava em andamento) não é recuperado, mas fica registrado em Execuções. Como não há conversa, usa blocos que não precisam dela, como Requisição HTTP, Código, Condição, Conforme o valor, Percorrer uma lista, Buscar cards, Kanban sobre um card escolhido, Iniciar outro fluxo e Ler dados da conta. Ex. todo dia útil às 9:00, buscar os cards ganhos ontem e iniciar um fluxo de acompanhamento para cada um
- **Início Webhook** - O fluxo ganha uma URL própria com um segredo (na URL ou em um cabeçalho) que você pode copiar, ver com um exemplo de `curl` pronto para usar e trocar quando quiser. Um CRM ou formulário externo envia qualquer JSON ou campos de formulário, recebe resposta na hora e o fluxo roda em segundo plano; os dados enviados ficam disponíveis nos campos de expressão, ex. `{{ webhook.body.telefone }}`. Uma chave de idempotência opcional (ex. telefone + e-mail) evita que o mesmo lead, reenviado, rode o fluxo duas vezes. Cada chamada aparece em Execuções com o corpo recebido, para ver o que falhou
- **Mensagem de saída** - Escolhe a caixa de entrada, encontra ou cria o contato pelo telefone (com e sem o 9º dígito; no WAHA resolve o `@lid`), abre a conversa e envia um texto ou um template. Dali em diante o fluxo trabalha nessa conversa, então qualquer outro bloco pode seguir (etiquetas, atribuição, esperar a resposta). Até ele rodar, um fluxo Webhook ou Agendado só usa os blocos que não precisam de conversa. Ex. chega um lead do CRM, o fluxo o cumprimenta no WhatsApp e passa a conversa para a equipe de vendas
- **Card atualizado** - O fluxo começa na conversa do card quando o card é criado, muda de etapa ou de funil, ou passa para ganho, perdido ou aberto, e `{{ kanban.change }}` diz o que mudou. Um card sem conversa não inicia nada. Para seguir só com um funil, uma etapa ou um status, coloque uma Condição depois do início
- **Mensagem enviada pela equipe** - O fluxo começa quando um agente envia uma mensagem pública (não um bot, outro fluxo nem uma campanha) e os blocos leem essa mensagem em `{{ message.* }}`; nunca continua um fluxo que espera uma resposta
- **Mudanças de outros fluxos** - Com "Começa com mudanças de outros fluxos", o início também responde quando outro fluxo muda a conversa ou um card. Nunca com as próprias mudanças, e uma cadeia de fluxos para depois de 3 saltos
- **Uma execução por vez por contato** - Se o fluxo já está rodando para esse contato, o novo início espera a vez (até cerca de um minuto). Um início que não chega a rodar fica em Execuções como erro com o motivo, e uma resposta ou um temporizador que estavam esperando nunca se perdem
- **Início tipo AgentBot** - O início pode ser vinculado a uma ou mais caixas de entrada para atendê-las como bot nativo, com exclusividade frente a AgentBot, Dialogflow ou outros fluxos ativos em cada uma. O Major pode compartilhar a caixa de entrada com o fluxo: o fluxo responde primeiro e o bloco "Responder com Captain" passa a conversa para o Major; as conversas novas dessa caixa não são atribuídas ao Major
- **Ignorar contatos** - O início pode deixar de fora os grupos do WhatsApp e contatos específicos, buscados por nome, telefone ou e-mail: o fluxo não começa para eles e, quando atende a caixa como bot, a conversa fica aberta para os agentes.
- **Início por eventos em algumas caixas de entrada** - Um início por eventos roda em todas as caixas de entrada ou só nas escolhidas; "Testar" usa uma conversa de uma delas
- **Fluxo como AgentBot** - No modo AgentBot o fluxo atua como um Agent Bot da plataforma: tem seu próprio bot, com o nome do fluxo, e as conversas que atende ficam pendentes e atribuídas a esse bot, sem assumir as que já estão atribuídas a uma pessoa. Suas mensagens saem como esse bot e o bloco "Transferir para um agente" passa a conversa para a equipe da mesma forma que o handoff de um Agent Bot. O bot não aparece em Configurações → Bots nem nos seletores de bots, e permanece como histórico do que o fluxo fez quando ele é pausado, passa para eventos ou é excluído
- **Histórico visual de execuções ao vivo** - Reproduz cada execução no canvas, marca os blocos com sucesso, erro ou aguardando e abre cada bloco para revisar entrada, saída e erros
- **Painel mais amplo e biblioteca compacta** - Painel lateral mais amplo e claro: a biblioteca mostra os blocos em duas colunas com filtros por grupo (a descrição aparece embaixo ao passar o mouse), e cada bloco diz em uma frase o que faz e para onde segue cada saída. O bloco Ações busca e agrupa as ações no próprio painel
- **Testar com o percurso** - Testar mostra seu fluxo como um chat do WhatsApp. Cada etapa aparece marcada entre as mensagens e o percurso é destacado no canvas. Onde o fluxo decidiria com dados reais, você escolhe por onde segue
- **Lista de fluxos** - A lista de fluxos segue o design das páginas de configurações: toque em qualquer linha para abrir o fluxo e veja seu status, o gatilho, a caixa de entrada, quantos blocos tem e quantas vezes foi executado hoje. No celular, as linhas são maiores e um botão flutuante cria um fluxo
- **Execuções** - Cada percurso aparece nos mesmos cartões do editor: quais blocos foram executados, quanto tempo levaram e por qual saída o fluxo seguiu. Filtre por execuções com erro ou aguardando e leia cada passo em linguagem simples, com os dados técnicos a um toque. Nada se perde em silêncio: um início que não pôde rodar e um horário agendado que não foi cumprido ficam como execuções com erro ("Não iniciou") que dizem por quê, e os passos pulados aparecem separados dos que falharam. Pela API e pelo MCP, cada execução diz por que parou, quais passos falharam ou foram pulados, e qual fluxo a iniciou ou quais fluxos ela iniciou
- **Comentário recebido** - Um início dispara o fluxo a cada comentário do Facebook ou Instagram; o mesmo comentário nunca inicia o fluxo duas vezes. Para responder só alguns (uma plataforma, uma publicação, algumas palavras, sem respostas), adicione uma Condição depois do início com os campos de Comentário; um início que salvou esses filtros continua aplicando-os até você tocar em "Mover para uma Condição". Os blocos de comentários respondem em público, enviam a resposta privada (uma por comentário, em até 7 dias), ocultam ou excluem o comentário, e as mensagens leem `{{comment.text}}`, `{{comment.platform}}`, `{{comment.permalink}}`, `{{comment.post_caption}}`, `{{comment.is_ad}}` e `{{comment.username}}`. Enviar mensagem manda uma mensagem direta com sua janela de 24 horas, que um comentário não abre
- **Comentários em "Mensagem recebida" e nos bots** - Os inícios "Mensagem recebida" e AgentBot ganham a opção "Incluir comentários de publicações (Facebook/Instagram)" para que os comentários também iniciem o fluxo. Ela é ativada sozinha ao salvar ou publicar um fluxo que usa a condição Tipo, um bloco ou uma ação de comentários, ou um bloco Enviar mensagem que responde ao comentário, e nunca é desativada sozinha. Cada comentário inicia o fluxo uma única vez: "uma vez por conversa" continua valendo só para as mensagens diretas. Um comentário nunca continua um fluxo que espera uma resposta
- **Condição Tipo** - No bloco Condição, o grupo "Última mensagem" ganha "Tipo" (`{{ message.kind }}`), que distingue uma mensagem direta (`direct_message`) de um comentário (`comment`); o valor é escolhido em uma lista
- **Blocos de comentários** - A biblioteca ganha o grupo "Comentários (Facebook e Instagram)" com "Responder comentário", "Mensagem privada ao comentário", "Ocultar comentário" e "Excluir comentário", cada um pronto para usar
- **Enviar como** - Os blocos Enviar mensagem salvos como "Resposta pública ao comentário" ou "Mensagem privada ao comentário" continuam funcionando (só texto com variáveis, sem depender da janela de 24 horas; se a execução não começou com um comentário, seguem pela saída normal sem enviar) e o painel oferece "Converter em bloco de comentário". Os blocos novos enviam uma mensagem direta; os comentários são respondidos com os blocos de Comentários, e o painel avisa quando um deles está em um fluxo cujo início não recebe comentários
- **API, MCP e Mega Assistant** - Os administradores podem gerenciar os fluxos fora do editor: todos os endpoints do Flow Builder estão na documentação da API (Swagger/OpenAPI e a coleção do Postman, com exemplos, em Super Admin → Documentação API), e o servidor MCP da conta e o Mega Assistant podem listar, criar, editar, revisar, testar, publicar e pausar fluxos, ver suas execuções e gerenciar as conexões. Para montar um fluxo do zero, eles consultam uma referência com a configuração, as saídas e um exemplo de cada bloco. Só com o Flow Builder ativo na conta e só para administradores

### Macros

Execute múltiplas ações com um só clique:

- **Macros pessoais** - Visíveis apenas para você
- **Macros globais** - Disponíveis para toda a equipe
- **Ações em cadeia** - Combine múltiplas operações
- **Atalho no editor de resposta** - Digite `#` para buscar, visualizar e executar macros sem sair da conversa
- **Atalho na barra de comandos** - Abra `Cmd/Ctrl + K` em uma conversa para selecionar a mesma macro ordenada; os atributos obrigatórios usam o diálogo compartilhado de resolução
- **Macros em lote** - Selecione várias conversas na lista e execute uma macro em todas pela barra de seleção (no celular, **Mais** → **Executar macro**), após uma confirmação

### Agent Bots

- **Bots de webhook** - Conecte com lógica externa via HTTP
- **Integração Typebot** - Conecte com fluxos conversacionais do Typebot
- **Handover para humanos** - Transferência suave para agentes reais
- **Handover inteligente** - Se um humano responder em conversa pendente do bot, a transferência ocorre automaticamente
- **Respostas humanas no webhook** *(Mega)* - Opcional por bot Webhook: recebe também as respostas do atendente, pelo painel ou pelo celular no WhatsApp, para que o bot mantenha o contexto do atendimento humano. Desativado por padrão
- **Handover por expiração** - Quando uma sessão de Webhook expira, a conversa é aberta, libera o bot e tenta a atribuição automática a um agente elegível; se ninguém estiver disponível, permanece aberta e sem atribuição
- **Bots por caixa de entrada** - Configure bots específicos por canal
- **Propriedade explícita do bot** - Conversas tratadas por um Agent Bot conectado ficam pendentes e atribuídas ao bot; a abertura, o handover por uma pessoa ou a desconexão do bot libera essa propriedade sem substituir atribuições humanas explícitas
- **O bot se cala após a transferência** - Um Agent Bot Webhook só recebe as mensagens do cliente enquanto a conversa está pendente (ou atribuída a ele); quando é transferida para a equipe, deixa de recebê-las, então não pode continuar respondendo uma conversa que uma pessoa já assumiu. Continua sabendo quando a conversa é aberta, resolvida ou muda de status, mas não das alterações da equipe como etiquetas ou responsável, e os bots configurados para receber respostas humanas continuam acompanhando toda a conversa
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

- **Nome do assistente de IA com a sua marca** - O Captain aparece como **Major** por padrão, e cada instalação pode dar a ele o próprio nome pelo Super Admin (Configurações → Captain). O nome aparece em todo o painel, no servidor MCP para qualquer IA conectada e no Mega Assistant, sem mudar integrações, API nem ferramentas existentes.
- **Respostas do Captain mais seguras e assumir a conversa** - O Captain não envia mais texto técnico de ferramentas ao cliente: tenta de novo uma vez e, se continuar errado, transfere para um humano sem cobrar crédito. Os agentes podem assumir conversas do Captain com um clique e ficam atribuídos, sem que a atribuição automática passe a conversa para outra pessoa.
- **Sugestões de etiquetas e prioridade** - O Captain sugere até três etiquetas existentes para a conversa ou o contato, e uma prioridade com base nas mensagens públicas recentes. Agentes podem aceitar ou descartar as sugestões; solicitá-las novamente gera uma nova resposta do modelo. A barra lateral indica quando a prioridade recomendada já está aplicada; aceitar etiquetas descarta a sugestão anterior. Ative `captain_classifier` para a conta e selecione o modelo de classificação de conversas nas configurações do Captain da conta ou do plano; a solicitação não consome créditos de respostas do Captain. Funciona com o Captain Decision Router: a classificação pode usar um modelo de decisão como o Jev (via OpenRouter), que responde com probabilidades em milissegundos e com custo muito baixo, ou qualquer modelo de chat (OpenAI, Anthropic, Gemini ou compatíveis).
- **Roteamento inteligente do Captain e do Mega Assistant** - O Captain Decision Router pode escolher o cenário do Captain que atende cada mensagem, as ferramentas personalizadas mais úteis quando há muitas e, no Mega Assistant, os guias que o pedido precisa e se ele precisa do modelo de tarefas complexas. Entende o pedido mesmo sem as palavras exatas e decide de novo a cada mensagem: quando o cliente muda de assunto, a conversa passa para o cenário certo em vez de ficar no primeiro que respondeu. Configure na seção Captain Decision Router de cada conta no Super Admin: escolha um modelo (por exemplo o Jev ou qualquer modelo de chat) e um modo, Só medir para comparar sem mudar respostas ou Ativo para aplicar; desligado ou sem modelo, as regras por palavras-chave continuam valendo.

Assistente de IA avançado que transforma como sua equipe trabalha.

**Assistentes de IA:**

- **Capacidades por provedor** - Superadministradores declaram modelos de chat, embeddings, transcrição de áudio e PDF/documentos por provedor. O Gemini suporta os quatro fluxos nativos e o Anthropic suporta chat e PDF/documentos; endpoints compatíveis com OpenAI só podem ser selecionados para capacidades configuradas explicitamente. A capacidade Decisões marca os modelos que respondem na API System One (por exemplo `typesafe/jev-1.13` no OpenRouter).

Crie assistentes especializados para diferentes necessidades:

- **Múltiplos assistentes** - Configure assistentes diferentes por caixa de entrada
- **Contexto personalizado** - Cada assistente entende seu domínio específico
- **Personalidade configurável** - Defina tom, estilo e abordagem
- **Modelos por função** - Configure modelos separados para Assistant, Copilot, sugestões e geração de FAQs a partir de documentos e PDFs
- **Histórico do Copilot e aviso de créditos** - O Copilot guarda suas conversas anteriores para retomá-las, e os administradores recebem um e-mail quando a maior parte das AI Actions do período foi usada
- **Condições do Captain em automações** - Descreva com suas palavras o que uma regra deve detectar ("o cliente quer cancelar") e o Captain verifica cada conversa ou mensagem; cada verificação desconta as AI Actions do seu modelo, e só quando a resposta importa
- **Padrões de provedor** - Superadministradores configuram com segurança OpenAI, Anthropic e Gemini, escolhem o provedor/modelo padrão do Captain e cada conta pode herdá-lo ou selecionar um modelo disponível por funcionalidade; o Captain herda opções compatíveis salvas para o modelo selecionado
- **Roteamento de modelos internos** - Superadministradores podem configurar separadamente o avaliador de conversas inativas; o override da conta tem prioridade sobre o modelo de instalação em ambientes auto-hospedados, enquanto as preferências do Captain para clientes mantêm os recursos internos ocultos
- **Sugestões de FAQ por conversa** - Conversas resolvidas com respostas reutilizáveis de agentes humanos são agrupadas em sugestões de FAQ para revisão; agentes só revisam sugestões e conversas de origem às quais têm acesso e podem editar, aprovar ou descartar sugestões abertas para publicar FAQs confiáveis
- **Troca fácil** - Alterne entre assistentes conforme necessário
- **Avatar próprio** - Envie uma imagem para cada assistente, exibida ao lado das respostas dele no widget de chat; ao removê-la, volta o logo padrão
- **Configurações para administradores** - As páginas de configurações e cenários do assistente abrem só para administradores; os agentes continuam trabalhando com o Major nas conversas
- **Atribuição manual de conversas** - Contas com Captain habilitado podem selecionar o assistente configurado para o inbox da conversa; ao atribuí-lo a conversa fica pendente e, ao removê-lo ou atribuir uma pessoa, a conversa é reaberta. Reabrir uma conversa (manualmente, em massa, com uma macro ou ao fim de um adiamento) a tira do Major, e uma macro ou automação que atribui um agente a abre como uma atribuição direta. O Major só assume e responde conversas enquanto a conta tiver o Captain habilitado
- **Um bot por caixa de entrada** - Cada caixa de entrada é atendida por um único provedor de bots: um Agent Bot, o Dialogflow, um fluxo do Flow Builder no modo AgentBot ou o Major. Conectar um segundo é recusado com uma mensagem indicando qual desconectar primeiro; as caixas que já tinham dois continuam funcionando. A exceção é um fluxo com o Major: o fluxo responde primeiro e o bloco "Responder com Captain" passa a conversa para o Major. O Major não responde nem agenda resolução automática em caixas com um Agent Bot ou Dialogflow
- **Visão geral do assistente** - A visão geral do Captain combina insights do período com métricas de resultados, fluxo e tendência de resolução, CSAT do Captain, qualidade do runtime, uso e cobertura de conhecimento; filtre por dias, esta semana ou a passada, ou por mês, e clique em uma métrica, um motivo de transferência ou no fluxo de resolução para ver as conversas por trás (administradores)
- **Detalhes da geração** - Abra o indicador “Gerado pelo Captain” em uma resposta do assistente ou nota privada de transferência para ver as etapas de ferramentas e cenários, fontes da base de conhecimento e raciocínio; o modelo e os créditos ficam disponíveis apenas para superadministradores
- **Citações confiáveis** - O Captain V2 exibe somente links web públicos validados pelo servidor, registra as fontes realmente selecionadas e mantém as URLs renderizadas fora do histórico enviado ao modelo; sessões anteriores preservam suas fontes existentes
- **Runtime limitado** - Captain V2 limita o contexto da conversa e as capacidades ativas por execução, usa um resumo semântico compacto com fallback seguro quando o histórico é omitido, rejeita correspondências de conhecimento irrelevantes, registra métricas seguras de runtime e protege ferramentas de escrita contra execuções obsoletas ou repetidas. Os detalhes de geração expõem diagnósticos seguros por execução de contexto e resumo; o painel de qualidade mede latência e fallbacks do resumo, enquanto os casos golden configurados são executados diariamente sem executar ferramentas.
- **Runtime único** - Toda conta com Captain usa o Captain V2; o runtime anterior, sua verificação de falsas promessas e seu classificador de ações foram retirados, então os assistentes são configurados apenas por cenários, diretrizes e guardrails
- **Compreensão de imagens** - O assistente pode analisar imagens enviadas nas conversas
- **Suporte multimodal** - Processa texto e imagens simultaneamente para respostas contextuais
- **Ignorar grupos** - Configure o assistente para não responder em conversas de grupo
- **Alvos ignorados** - Defina conversas ou contatos específicos que o assistente deve pular
- **Público e horário** - Limite as respostas a contatos que atendem a condições configuráveis e escolha se o assistente responde sempre, durante ou fora do horário comercial; as conversas fora dessas regras vão para a fila humana. "Espera antes de responder" (até 10 segundos) permite que o assistente responda com uma única mensagem aos clientes que dividem um pedido em várias mensagens
- **Resolução por inatividade** - Com o Captain V2, cada assistente escolhe se o Captain revisa a conversa, sempre a resolve ou aguarda o cliente; os modos que resolvem usam um temporizador de 5 minutos a 24 horas e podem enviar uma mensagem de encerramento opcional. A revisão tem três resultados: a conversa está concluída, aguarda o cliente ou precisa de uma pessoa. Quando o próximo passo é do cliente, o Captain resolve a conversa em vez de transferi-la, com a mensagem de encerramento no idioma do cliente e sem pesquisa CSAT; se o cliente voltar a escrever, a conversa volta para pendente e uma resolução posterior envia a pesquisa normalmente

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
- **Verificação de e-mail para ferramentas sensíveis** - Uma ferramenta pode exigir que o cliente confirme o e-mail com um código de 6 dígitos antes de o Captain usá-la. O Captain envia o código por e-mail (com o nome da sua caixa de entrada), pede ao cliente que o digite no chat e só então executa a ferramenta. Um parâmetro "e-mail verificado" envia esse endereço confirmado para a sua API, então ninguém consegue consultar a conta de outra pessoa digitando o e-mail dela. Ferramentas novas que alteram dados começam com a opção ativada
- **Contexto dinâmico** - Busque informação em tempo real

**Servidores MCP (Model Context Protocol):**

Conecte servidores MCP para ampliar as capacidades do seu assistente:

- **MCP nativo por conta** - Crie servidores MCP por conta com endpoint dedicado
- **MCP pensado para agentes** *(Mega)* - Cada ferramenta informa seu módulo, sua intenção (buscar, ler, criar, enviar, agendar, diagnosticar), seus efeitos e o que precisa, e as ferramentas parecidas explicam quando usar cada uma; os erros trazem um código estável, se podem ser repetidos e um identificador da solicitação; envios e agendamentos aceitam uma chave de idempotência opcional: uma nova tentativa com a mesma chave não é enviada duas vezes, e uma chamada sem chave é enviada sempre, como antes (a proteção é opcional); `account_context` diz o que o servidor pode fazer e por que não; execuções e fluxos do Flow Builder são lidos sem o grafo completo (uma execução de 10 etapas: de 151 KB para 1,7 KB). Tudo é aditivo: os clientes existentes continuam funcionando igual
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
- **Configuração de teste do Playground** - Teste no Playground cenários salvos (mesmo desativados) ou temporários, diretrizes de resposta, limites e até 10.000 caracteres de conhecimento colado sem alterar o assistente; administradores podem salvar um item temporário ou o conhecimento colado (como documento Markdown) com um clique, e cada resposta mostra quem respondeu, as tools chamadas, as chamadas com falha e sua duração. As respostas do Playground usam créditos do Captain
- **Gestão centralizada** - Administre todos seus servidores MCP nas configurações

**Modo Auto-Resolve do Captain:**

Configure como o Captain gerencia a resolução automática de conversas:

- **Modo avaliado** - O Captain analisa o contexto, incluindo o status da conversa e os papéis dos participantes, e decide autonomamente se a conversa está concluída, aguarda o cliente (nos dois casos é resolvida; um encerramento aguardando o cliente não envia pesquisa CSAT) ou precisa de uma pessoa (é transferida); transferências e acompanhamentos pendentes permanecem em aberto
- **Mensagens no idioma do cliente** - Se o assistente não tem mensagem de transferência ou de resolução própria, o texto padrão chega no idioma em que o cliente escreve, não no da conta, e a transferência por inatividade também avisa o cliente
- **Modo legado** - Comportamento original: resolve automaticamente conversas pendentes com base no temporizador
- **Modo desativado** - O Captain não resolve conversas automaticamente
- **Por assistente** - Cada assistente salva sua própria política; assistentes sem política salva mantêm a configuração da conta como compatibilidade

**Copilot para Agentes:**

Assistência em tempo real enquanto os agentes trabalham:

- **Sugestões de resposta** - IA gera respostas sugeridas baseadas no contexto
- **Rascunhos orientados pelo assistente** - Ao sugerir uma resposta, o Copilot usa instruções, FAQs, citações e ferramentas GET do assistente selecionado; o agente revisa e edita o rascunho antes de enviar
- **Sugestões legíveis** - Sugestões longas expandem o editor de resposta até 350 px sem substituir o tamanho escolhido manualmente
- **Painel mais confortável** - O chat do Copilot acompanha a resposta enquanto ela chega, mas não move a tela se você rolou para cima para ler; você pode colar texto enquanto a mensagem anterior é enviada, e no celular o teclado não abre sozinho
- **Parar e expandir** - Um botão Parar na caixa de texto interrompe a resposta que o Copilot está preparando, sem cobrar uma AI Action por ela; um botão para expandir alarga o painel em telas grandes, e o painel também cabe ao lado da visão geral do Major
- **Limite de uso marcado como falha** - Quando as AI Actions acabam, o aviso do Copilot é salvo como mensagem com falha, para que as integrações não o tomem como resposta
- **Resumo de conversa** - Obtenha contexto rapidamente de conversas longas
- **Busca no Help Center** - Encontre artigos relevantes automaticamente
- **Melhoria de texto** - Corrija gramática e melhore tom
- **Tradução instantânea** - Traduza mensagens on-the-fly

**Fluxos de trabalho do Copilot *(premium, exige as flags `captain_integration` e `copilot_workflows`)*:**

O Copilot resolve pedidos de várias etapas sobre os dados da conta:

- **Trabalho em várias etapas** - O Copilot planeja e executa várias etapas para um pedido, mostra cada etapa no painel e continua trabalhando mesmo com o painel fechado; a resposta espera você voltar
- **Relatórios do dashboard** - Lê os mesmos números que as páginas de relatórios mostram (conversas, resoluções, tempos de primeira resposta, resolução e resposta, mensagens, resoluções e transferências de bots) por dia, semana, mês ou ano, por agente, caixa de entrada, time ou etiqueta, ordenados pela métrica pedida, com gráficos quando pedidos
- **Diretório e dados da conta** - Encontra agentes, caixas de entrada, times e etiquetas pelo nome, e conta, agrupa e filtra os registros da conta (conversas, contatos, mensagens, CSAT, artigos e uma lista permitida de outras tabelas da conta); colunas secretas, como tokens e credenciais, e chaves JSON com nome de segredo ficam fora do que o Copilot lê
- **Revisão de conversas em lote** - Revisa centenas de conversas em segundo plano conforme a pergunta do agente, com um card de progresso, a cobertura (revisadas, correspondentes, com falha, restantes) e um link para cada conversa citada; números e links que nenhuma ferramenta retornou são verificados e links desconhecidos são removidos
- **Mudanças com card de aprovação** - O Copilot propõe mudanças e um card de aprovação mostra o que vai mudar antes de qualquer ação; na aprovação, cada registro é verificado de novo com as permissões do agente que aprova. 17 ações: alterar status, prioridade, agente, time, etiquetas, atributos personalizados e SLA, adicionar participantes, notas privadas e respostas, silenciar ou reativar, e em contatos adicionar etiquetas, notas e atributos ou bloquear e desbloquear
- **Blocos visuais abaixo da resposta** - O Copilot pode mostrar tabelas, métricas em destaque, gráficos, cards, linhas do tempo, cards de contatos e conversas e botões de acompanhamento abaixo da resposta, com o mesmo visual do Mega Assistant; contatos e conversas só aparecem quando o agente pode abri-los, e um botão de acompanhamento envia sua pergunta como a próxima mensagem do agente, nunca uma mudança
- **Parar rejeita aprovações pendentes** - Ao clicar em Parar o fluxo termina e as mudanças que aguardavam aprovação são rejeitadas; uma aprovação sem resposta expira em 5 minutos
- **Modelos no Super Admin** - A rota de modelo `copilot_workflows` escolhe o modelo dos fluxos e `copilot_screening` o que filtra conversas antes de uma revisão; o filtro fica desligado até um modelo ser atribuído

**Funcionalidades de IA:**

- **Correção gramatical** - Conserte erros em um clique
- **Expansão de texto** - Amplie respostas curtas
- **Simplificação** - Torne respostas complexas mais claras
- **Mudança de tom** - Formal, amigável, profissional
- **Resumos** - Condense conversas longas

**Monitores de conversas** *(Enterprise/Mega)*:

Acompanhe os assuntos que importam nas suas conversas, descritos com suas palavras:

- **Condições em linguagem natural** - Descreva o que procurar (pedidos de reembolso, problemas de login, intenção de cancelar...) e o Captain revisa cada conversa com essa condição
- **Dez modelos** - Comece com monitores prontos para suporte, vendas, produto, finanças e operações
- **Prévia antes de salvar** - Teste uma condição em até cinco conversas recentes
- **Histórico e atualizações ao vivo** - Um monitor novo revisa as conversas dos últimos sete dias e depois cada mensagem nova de clientes ou agentes
- **Relatório por monitor** - Conversas que correspondem por hora, seis horas ou dia, com as conversas de cada barra para administradores; o relatório se atualiza sozinho
- **Pausar e retomar** - Pause sem perder resultados; retome revisando o período pausado ou a partir de agora
- **Automações** - O novo evento *Monitor encontra uma conversa* executa ações na primeira vez que um monitor encontra uma conversa com atividade nova
- **Alertas no Slack** - Escolha um canal do Slack por monitor para receber uma mensagem na primeira vez que ele encontra uma conversa por nova atividade ao vivo; desconectar o Slack desliga os alertas. Os alertas mantêm a verificação ao vivo ligada, o que pode usar mais AI Actions
- **Seu modelo, suas AI Actions** - O Super Admin escolhe o modelo (um modelo de decisão como o Jev ou qualquer modelo de chat); cada conversa revisada consome as AI Actions desse modelo e os monitores esperam enquanto a conta não tiver
- **Onde** - Configurações › Captain › Monitores, também no menu do Captain; desktop e celular

**Transcrição de Áudio:**

Transcreva automaticamente mensagens de áudio para texto:

- **Transcrição automática** - Converta notas de voz em texto legível
- **Controle de gravações de chamadas** - Ative ou desative a transcrição por provedor (WhatsApp Cloud e WaVoIP)
- **Diarização de chamadas** - Separa gravações por turno usando o nome do contato e do agente atribuído
- **Transcrição manual** - Enfileira a transcrição pelo menu contextual quando uma mensagem de áudio ainda não tem texto
- **O Major continua respondendo** - Se o provedor rejeitar uma nota de voz (arquivo inválido ou bloqueado pelos filtros de conteúdo), o Major responde sem essa transcrição em vez de tentar de novo ou ficar em silêncio
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
- **Tipo de contato** - Visitante, Lead, Cliente; um contato vira lead quando tem e-mail, telefone, identificador ou ID do WhatsApp, quando inicia uma conversa, ou quando é criado pelo painel, pela API ou por uma importação, e nunca volta a visitante
- **Histórico do contato na conversa** - No início de uma conversa, uma pílula abre a conversa anterior do contato; a próxima aparece em conversas resolvidas ou enquanto a lista mostra esse contato. **Ver todas as conversas** no painel de contato (**Histórico** no celular) limita a lista de conversas ao contato, da mais recente para a mais antiga, e o botão de limpar volta à lista completa
- **Modo leitura em conversas antigas** - Abrir uma conversa anterior pelo fio limita a lista ao contato; conversas antigas abrem com a caixa de resposta recolhida em **Responder a esta conversa antiga** (com **Ir para a conversa mais recente**), para ninguém responder um fio antigo por engano. A barra, um atalho de resposta ou qualquer ação de escrita abre o editor; a conversa mais recente mantém o editor normal e limpar o filtro volta para ela

### Atributos Personalizados

- **Campos flexíveis** - Crie atributos para contatos e conversas
- **Tipos de dados** - Texto, número, lista, data, checkbox, link
- **Integração com automações** - Use atributos como condições
- **Visibilidade configurável** *(Enterprise)* - Defina quais funções (roles) podem ver cada atributo; oculte campos sensíveis de agentes com nível inferior
- **Copiar como exibido** - Ao copiar um atributo de data, a data é copiada como aparece na tela

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
- **Enriquecimento de empresas** *(premium, desativado por padrão)* - Com a função Company Enrichment e a chave Context.dev da instalação, uma empresa nova com domínio recebe automaticamente descrição, setor, porte, localização, telefone e redes sociais (uma consulta por domínio); administradores podem atualizar pela página da empresa

### Notas

- **Notas por contato** - Documente informações importantes
- **Histórico interno** - Mantenha contexto entre interações
- **Notas longas pela conversa** - A caixa de notas do painel de contato da conversa não tem contador de caracteres, então dá para escrever notas longas ali

### Importação de Dados

- **Upload de CSV** - Importe contatos em massa
- **Mapeamento de campos** - Associe colunas com atributos
- **Importação histórica do Intercom e Freshdesk** - Administradores podem importar contatos, conversas e mensagens históricas do Intercom ou Freshdesk em segundo plano. As importações resistem a quedas de conexão com o banco de dados (três novas tentativas com espera crescente), e as do Freshdesk usam a versão em texto simples de cada mensagem e ignoram só a mensagem cujo HTML está aninhado demais, em vez de falhar a importação
- **Monitoramento da importação** - Consulte o progresso, registros ignorados, erros e baixe os registros de ignorados
- **Nova tentativa de importação interrompida** - Tente novamente uma importação do Intercom ou Freshdesk interrompida após 15 minutos sem perder o progresso
- **Validação automática** - Detecte erros antes de importar
- **Acesso controlado** - Importação e exportação disponíveis para administradores e gestores de contatos
- **Exportação segura** - Valores iniciados por caracteres de fórmula são exportados como texto para impedir sua execução em planilhas

### Bloqueio de Contatos

- **Bloqueio manual** - Evite mensagens de contatos problemáticos
- **Filtragem automática** - Não aparecem na caixa de entrada principal
- **Bloqueio ativo no WhatsApp** - Mensagens recebidas de contatos bloqueados são descartadas antes de abrir conversa

### Preferências de Mensagens por Contato *(Mega)*

- **Ignorar saudação** - O contato não recebe a mensagem de saudação da caixa de entrada
- **Ignorar CSAT** - O contato não recebe a pesquisa de satisfação ao resolver a conversa
- **Ignorar título do agente** - As mensagens enviadas ao contato não começam com o nome do agente
- **Salvas no contato** - Mantidas em novas conversas e reaberturas
- **Provedores** - Aplicam-se a caixas de entrada WhatsApp com Evolution, WAHA e UAZAPI; editáveis no painel da conversa ou na página do contato

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
- **Importação por CSV** - Em campanhas de WhatsApp e Channel API, envie um CSV com telefones (nome e email opcionais): os contatos novos são criados, todos recebem uma etiqueta e essa etiqueta entra no público. Contatos que já existiam (mesmo telefone, incluindo as variantes do Brasil, México e Argentina, ou mesmo email) mantêm os dados e etiquetas e só recebem as novas. Uma coluna opcional `etiquetas` (separadas por vírgulas) também dá a cada contato as próprias etiquetas, criadas se não existirem, para segmentar depois; o público da campanha continua sendo a etiqueta do painel. Aceita listas de até 50.000 linhas, roda em segundo plano e mostra o progresso e um resumo de novos, existentes, repetidos e rejeitados
- **Combinação** - Misture contatos diretos e etiquetas
- **Deduplicação automática** - Evite duplicados por número de telefone

**Filtragem inteligente:**

- Exclui contatos sem número de telefone
- Deduplicação por telefone (pega o primeiro contato)
- Contador de audiência pré-envio

### Na Conversa

- **Etiqueta de campanha** - Cada mensagem enviada por uma campanha mostra acima do balão um megafone com o nome da campanha e o balão fica violeta, para se diferenciar das mensagens de agentes, bots e automações; administradores clicam nele para abrir o relatório
- **Do relatório à mensagem** - No relatório da campanha, o nome de cada contato abre a conversa com a mensagem da campanha destacada

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
- **Edição do rodízio** - Em campanhas de WhatsApp com Evolution, WAHA ou Uazapi e do canal API, mantenha as caixas selecionadas, adicione ou remova caixas e desative o rodízio ao salvar uma campanha editável
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
- **Diagnóstico de entrega** *(Mega)* - Relatórios e exportações CSV incluem o código e o motivo do provedor; uma intervenção na caixa de entrada ou no modelo pausa a campanha sem marcar contatos não tentados como falhos
- **Funil de entrega** *(Mega)* - O relatório conta os contatos enviados, entregues, lidos e falhos com as taxas de envio, entrega e leitura, marca cada contato como Enviado, Entregue, Lida ou Falhou e filtra por etapa; entregues e lidos vêm das confirmações do provedor, então uma linha que nunca informa leituras não mostra nenhuma
- **Excluir uma campanha** - Remove a campanha e o relatório de envios; as mensagens que ela já enviou continuam nas conversas, sem a etiqueta da campanha

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

- **Slugs editáveis e sem duplicados** - Altere a URL de um artigo nas propriedades com validação, sem artigos duplicados ao criar e com um portal público mais organizado (idioma do logo, autores excluídos, tabelas nas prévias)
- **Múltiplos portais** - Crie bases de conhecimento por produto/marca
- **Domínio personalizado** - Hospede no seu próprio domínio
- **Design configurável** - Cores, logo, texto de cabeçalho
- **Integrações de análise** - Administradores podem conectar Google Analytics 4, Google Tag Manager, Microsoft Clarity, Hotjar, Plausible, Amplitude e Meta Pixel; os scripts são publicados apenas com um identificador válido
- **Layouts selecionáveis** - Escolha entre uma página inicial clássica ou navegação lateral em estilo documentação
- **Multi-idioma** - Artigos em múltiplos idiomas
- **Artigo original** - Cada tradução é vinculada ao artigo original nas propriedades do artigo; uma família tem um único artigo por idioma, e a tradução com IA não pode sobrescrever o idioma do original
- **Conteúdo recomendado por localidade** - Selecione e ordene até 3 categorias e 6 artigos em destaque por localidade; o conteúdo popular permanece como fallback quando nada é configurado
- **Remover um idioma com seu conteúdo** - Remover um idioma apaga seus artigos e categorias, após uma confirmação que mostra quantos são; o idioma padrão não pode ser removido
- **Norueguês** - O norueguês aparece com seu nome entre os idiomas da central de ajuda
- **Logo para modo escuro** - Adicione um segundo logo que a central de ajuda pública mostra no modo escuro
- **Gerenciado por administradores** - O menu da Central de ajuda aparece para administradores e funções que gerenciam a base de conhecimento; os agentes continuam inserindo artigos nas respostas
- **Embeds GuideJar** - Insira guias interativos do GuideJar no conteúdo da Central de Ajuda

### Organização de Conteúdo

- **Categorias** - Agrupe artigos por tema
- **Subpastas** - Organização hierárquica
- **Artigos** - Conteúdo rico com markdown
- **Filtrar por autor** - A lista de artigos filtra por qualquer colega (com busca) no lugar da aba "Meus artigos", e as contagens por status seguem o autor escolhido
- **Aviso de versão mais recente** - Se um colega ou outra aba alterar o artigo que você está editando, o editor oferece *Carregar a versão mais recente*
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
- **Arquivado** - Oculto mas preservado; a central de ajuda pública não o mostra, nem pelo link direto
- **Rascunho por idioma** - Cada tradução de um artigo pode estar em rascunho de forma independente; publique apenas os idiomas prontos sem afetar os demais
- **Edições não publicadas** - Alterações em um artigo publicado ficam em rascunho até serem revisadas e publicadas explicitamente; elas podem ser comparadas à versão visível ou descartadas

### SEO e Acesso

- **Meta descrições** - Otimize para buscadores
- **URLs amigáveis** - Slugs personalizáveis
- **Widget integrado** - Conecte portal com chat ao vivo
- **Ocultar dos buscadores** - Em Configurações › SEO uma central de ajuda pode ficar fora do Google e de outros buscadores enquanto continua funcionando para os visitantes; cada artigo também pode ser ocultado nas suas propriedades
- **Imagens no seu domínio** - As imagens dos artigos e as fotos dos autores seguem o domínio atual da central de ajuda, também com domínios próprios

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
- **Links reais dos artigos** - Quando o Major lê um artigo publicado, recebe o link público dele na central de ajuda, assim compartilha a URL correta

---

## 📊 Relatórios e Analytics

### Relatórios de Conversas

- **Volume** - Novas, resolvidas, pendentes
- **Tempo de resolução** - Média e distribuição
- **Primeira resposta** - Tempo de resposta inicial
- **Tendências** - Evolução temporal
- **Drilldown de barras** - Abra cada barra do gráfico para revisar as conversas ou mensagens que compõem a métrica, com navegação entre buckets e contagem de resultados; para a contagem de conversas, Ver todas abre uma lista filtrada em uma nova aba

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
- **Respostas do bot** - Conta só as mensagens públicas enviadas por bots (AgentBot, Captain e fluxos do Flow Builder que atuam como bot); respostas de agentes e notas privadas em conversas com bot não contam mais, então os totais podem ficar menores que antes

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
- **Tempo de espera** - Espera média até um agente atender a chamada recebida
- **Abandonadas** - Chamadas recebidas em que o contato desligou antes de ser atendido
- **Atendidas dentro do SLA** - Percentual atendido dentro do SLA da caixa de entrada (20 segundos por padrão, configurável por caixa)
- **Resolvidas no fluxo** - Chamadas que terminaram no fluxo de chamada sem pedir um agente
- **Gravações no relatório** - Chamadas com gravação (WAHA, WhatsApp Cloud ou Twilio) tocam em um player compacto com barra de posição, velocidade (1x, 1.5x, 2x) e download; chamadas sem gravação mostram "Sem gravação"
- **Largura total** - Os relatórios de chamadas e de atividades usam toda a largura da tela

**Análise por agente:**

- **Chamadas por agente** - Distribuição de carga
- **Duração por agente** - Tempo médio de cada agente
- **Taxa de resolução** - Efetividade por agente
- **Transferências por agente** - Quantas transferências chegaram a cada agente e quantas ele atendeu

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
- **Conversas, chamadas ou ambas** - No menu do perfil, cada agente escolhe por conta se recebe conversas, chamadas ou ambas (pelo menos uma fica ativada). A atribuição automática pula os agentes com conversas desligadas e as chamadas do WhatsApp e do Twilio não tocam para agentes com chamadas desligadas; a atribuição manual continua funcionando. Os interruptores aparecem quando uma caixa de entrada da conta recebe chamadas; ambos vêm ativados
- **Desligamento guiado de agentes** - Antes de remover um agente, escolha entre deixar as conversas sem atribuição ou reatribuir em lote
- **Convites protegidos** - Convites para novos agentes respeitam o limite diário de e-mails da conta sem bloquear a inclusão de usuários existentes
- **Configurações em painel lateral** - Agentes, equipes (com seus membros), etiquetas, macros, SLAs, papéis personalizados, políticas de atribuição, webhooks, apps do painel e integrações como Dialogflow são vistos, criados e editados no mesmo painel lateral, também no celular

### Equipes

- **Departamentos** - Vendas, Suporte, Faturamento, etc.
- **Atribuição automática** - Round-robin dentro da equipe
- **Restrição de visibilidade** - Membros veem apenas suas conversas
- **Identificação visual** - Configure um emoji ou ícone com cor por equipe para reconhecê-la em listas e seletores de atribuição

### Inboxes e Membros

- **Acesso por inbox** - Atribua agentes a canais específicos
- **Ver conversas** - Cada caixa em Configurações › Caixas de entrada, e o cabeçalho das suas configurações, tem um link que abre as conversas dela
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
- **Uma função por membro** - Dar uma função personalizada a um administrador o torna agente com essa função, e tornar um membro administrador remove a função personalizada. A conta sempre mantém pelo menos um administrador

### Horários de Trabalho

- **Disponibilidade por inbox** - Defina horários de atendimento
- **Fusos horários** - Suporte multi-região
- **Mensagens fora do horário** - Respostas automáticas
- **Exceções da mensagem fora do horário** *(Mega)* - Em Horário de atendimento, cada caixa pode deixar sem a mensagem de indisponibilidade os grupos do WhatsApp, números ou identificadores específicos e os contatos com certas etiquetas, com as mesmas regras dos robôs
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
- Conversa atribuída a você, inclusive quando está pendente
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
- **Retirar em vez de excluir** - Um tipo pode ser desativado para deixar de ser oferecido em tarefas novas enquanto as existentes o mantêm; ao tentar excluir um tipo com tarefas essa opção é oferecida, e excluir um tipo ou desativar Tarefas sempre pede confirmação
- **Paleta consistente** - Os tipos usam a mesma paleta visual de 22 cores do Google Agenda e mantêm a cor escolhida no calendário, detalhes e listas, sem que o status a substitua
- **Permissões por escopo** - Administradores controlam todas as tarefas; roles personalizadas podem receber separadamente gestão das próprias/atribuídas, leitura global e relatórios; agentes padrão só veem e gerenciam tarefas criadas por eles ou atribuídas a eles
- **Visualizações de calendário e lista** - O cabeçalho de Mensagens agendadas: busca, painel de filtros (folha em telefones), alternância calendário/lista, atualizar e Nova tarefa (botão flutuante em telefones). O mês usa o controle ‹ mês › e a grade do módulo Calendário, com até três tarefas por dia e o status como ícone (vencida, em andamento, riscada quando fechada); a lista é uma agenda agrupada por dia. Em telefones o mês mostra pontos e as tarefas do dia escolhido abaixo. Ambas abrem o mesmo detalhe
- **Filtros operacionais** - Busque por título, filtre por responsável —inclusive sem responsável—, tipo e hoje, esta semana ou próximos 30 dias; um único seletor de status começa em Todas as tarefas e oferece pendentes, em andamento, vencidas, concluídas ou canceladas; ordene a lista por início, vencimento, título, prioridade, status ou responsável
- **Tarefas de vários dias** - Uma tarefa aparece em cada dia do calendário que intersecta sua programação, inclusive quando começou antes do mês visível
- **Experiência mobile** - Em telas pequenas, os filtros se reorganizam sem comprimir o calendário mensal; formulários e detalhes mantêm as ações visíveis sem cobrir o conteúdo
- **Leitura antes de editar** - Ao abrir uma tarefa, seus detalhes são exibidos; concluir e cancelar ficam no cabeçalho com resumo obrigatório, enquanto editar e, somente para administradores, excluir com confirmação ficam no rodapé
- **Responsabilidade clara** - Atribua uma tarefa a um agente da conta ou deixe-a sem responsável
- **Histórico resiliente** - Excluir contato, conversa, item Kanban ou responsável preserva seus rótulos históricos, limpa referências ativas e resincroniza a projeção Google sem duplicar a cascata de exclusão
- **Estados operacionais** - Gerencie tarefas pendentes, em andamento, concluídas ou canceladas; vencimentos são detectados automaticamente após o prazo
- **Encerramento documentado** - Concluir ou cancelar exige um resumo do resultado para registrar o que ocorreu e os próximos passos
- **Aviso ao responsável** - Ao atingir o prazo, somente o agente responsável recebe um popup e uma notificação para abrir, concluir, cancelar ou editar a tarefa; ele pode marcar o aviso como visto ou adiá-lo para reaparecer automaticamente, e tarefas sem responsável não geram aviso. O aviso parece um cartão de evento do Google Calendar: cor e nome do tipo, há quanto tempo venceu, data, contato e conversa, prioridade alta ou urgente e o início da descrição, com um botão Adiar que adia em um clique; com vários avisos mostra quantos restam. O aviso de eventos do Calendário usa o mesmo design, com local e link do Google Meet
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
- **Mudanças de categoria da Meta** - Avisa quando a Meta recategoriza um template (por exemplo, de Utilidade para Marketing) ou anuncia que fará isso em 24 horas, com atalho para solicitar a revisão
- **Métricas de uso** - Veja quantas vezes cada template foi entregue e sua taxa de leitura
- **Filtros avançados** - Filtre por status, categoria, idioma, canal e intervalo de datas
- **Busca** - Encontre templates rapidamente por nome ou conteúdo
- **Excluir templates** - Exclua templates individuais ou em lote com confirmação
- **Ativar ou desativar templates** - Oculte um template dos agentes (resposta, nova conversa e mensagens agendadas) sem excluí-lo na Meta; campanhas e automações continuam podendo usá-lo. Útil para os templates de exemplo da Meta ou os feitos só para campanhas
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
- **Scripts de dashboard (Super Admin)** *(Mega)* - Publique personalizações globais sem alterar o código base. A lista mostra a ordem de carregamento de cada script, os domínios externos de onde carrega código, o tamanho e um interruptor para ativá-lo, com busca ao vivo e filtro por status; um único formulário cria e edita o script com números de linha, contador de tamanho e uma pré-visualização do painel real de uma conta que injeta o código não salvo e informa erros. No celular cada script é um cartão, com navegação compacta e editor ajustado à largura da tela
- **Agent Bots (Super Admin)** *(Mega)* - Gerencia os bots de agente de toda a instalação. A lista mostra quem pode conectar cada bot (global ou de uma conta), seu tipo, o domínio para onde envia eventos e quantas caixas de entrada o usam, com busca ao vivo por nome, URL ou conta e filtro por alcance; a página do bot reúne seus detalhes, as caixas de entrada conectadas com a conta e o status, a URL do webhook, o segredo de assinatura e o token de API ocultos com cópia, e a exclusão; o formulário escolhe a conta com uma busca (vazio = bot global). No celular cada bot é um cartão
- **Apps da plataforma (Super Admin)** *(Mega)* - Gerencia os apps que usam a API da plataforma. A lista mostra quantas contas cada app alcança e os usuários e bots que ele criou, com busca ao vivo; a página do app lista as contas com busca, filtro com/sem acesso e paginação para dar ou revogar acesso uma a uma ou dar acesso a todas, e reúne o token de API oculto com cópia, os registros que gerencia e a exclusão; o formulário tem um interruptor de acesso a todas as contas que nunca revoga acessos. Avisa que as contas criadas depois não são adicionadas sozinhas. No celular cada app é um cartão
- **Banners da plataforma (Super Admin)** *(Mega)* - A lista mostra cada banner na cor do seu tipo, quem o vê, quando e se está visível agora, agendado, encerrado ou desativado, com um interruptor por linha, busca ao vivo e filtro por status; a página do banner reúne a mensagem, o público e as datas, as contas escolhidas, a atividade (incluindo quantos agentes o fecharam) e a mesma pré-visualização do formulário, com aviso quando está agendado ou encerrado. No formulário o tipo é escolhido pela cor e a pré-visualização acompanha o tipo, o título, a mensagem e o status durante a edição, nas cores reais do painel. No celular cada banner é um cartão
- **Anúncios de novidades** *(Mega)* - O Super Admin anuncia uma funcionalidade nova com uma imagem ou um vídeo e um texto curto: um link do YouTube, Vimeo, Loom, Arcade, Bunny, Guidejar ou CodePen, o link de um arquivo ou um arquivo enviado pelo próprio formulário criando um banner do tipo Novidade, com as mesmas contas, papéis e datas dos outros banners. Ao entrar no painel os agentes o veem como uma janela sobre o dashboard; com vários anúncios ativos passam de um para outro pelas miniaturas, pelos pontos, pelas setas do teclado ou deslizando em telas sensíveis ao toque. Depois de fechado não aparece mais em nenhum dos seus dispositivos até o anúncio ser editado, e um anúncio novo ou editado aparece ao vivo sem recarregar. No formulário a imagem ou o vídeo só são pedidos para esse tipo e a pré-visualização mostra o painel com a imagem
- **Provedores de WhatsApp (Super Admin)** *(Mega)* - Os servidores de Evolution API, WAHA e Uazapi aparecem em uma grade de cartões com o provedor e o slot, o uso de caixas de entrada frente à capacidade, o host da API, a origem das credenciais (salvas, do ambiente ou ausentes), chamadas de voz e status, com busca ao vivo e filtro por provedor; a página do servidor mostra o uso, as caixas de entrada que hospeda com a conta, a conexão com as variáveis de ambiente que o slot lê e se estão definidas, as configurações e a exclusão (bloqueada para o slot legado ou enquanto hospeda caixas de entrada). O formulário por seções escolhe o provedor como opção e mostra ao vivo quais variáveis de ambiente o slot escolhido lê. No celular cada servidor é um cartão em largura total
- **Diagnóstico de push (Super Admin)** *(Mega)* - Ferramenta em três passos para verificar por que um usuário não recebe notificações: busca-se o usuário por nome, e-mail ou #id (cada resultado indica quantos dispositivos ele tem), escolhem-se as assinaturas, que mostram o navegador (Chrome, Firefox, Safari, Edge) ou o app móvel, o final do endpoint ou token e a última atualização, ou excluem-se as assinaturas quebradas. Ao lado, a mensagem de teste mostra uma prévia ao vivo da notificação com o ícone e o nome da instalação, contadores de tamanho para título e corpo, um texto padrão no idioma do Super Admin que pode ser restaurado e um botão que indica para quantos dispositivos será enviado. O push de teste pelo navegador agora inclui o corpo, não só o título. Os resultados mostram por dispositivo se o serviço de push aceitou, falhou ou ignorou, com a resposta bruta; as falhas abrem sozinhas. No celular cada dispositivo é um cartão
- **Páginas de configuração (Super Admin)** *(Mega)* - Cada página de Configurações (Geral, SAML SSO, Marca própria, Faturamento, Captain, E-mail, Messenger, Instagram, TikTok, Google, Microsoft, Linear, Notion, Slack, WhatsApp incorporado, Shopify, EvolutionAPI, QuepasaAPI, Mega Hub e Call ICE) mostra o ícone, o nome e a descrição da função, e agrupa seus valores em seções com título e explicação (por exemplo App, Webhooks e Opções nos canais, ou Imagens, Identidade, Cores, Legal e Web na marca). Cada valor mostra o nome da sua variável; os segredos ficam ocultos com opção de ver, as imagens mostram a prévia e podem ser enviadas, e as cores têm seletor. Salva-se pela barra fixa com um aviso traduzido. No celular as seções ficam em uma coluna com a barra de salvar embaixo
- **Provedores de IA (Super Admin)** *(Mega)* - A lista mostra cada provedor em um cartão com o tipo de conexão e o host, se está ativo, se é o padrão do Captain ou do Mega Assistant, quantos modelos tem e o estado de cada capacidade (verificada, com falhas ou não testada), além dos avisos de saldo ou cota do provedor. A página do provedor reúne a tabela de modelos com o resultado de cada capacidade, AI Actions, raciocínio e preços, os testes com falha e sua mensagem, a conexão, onde é usado (incluindo as contas que o escolheram) e a exclusão; os modelos são testados dali. O formulário é dividido em Conexão, Disponibilidade e Modelos: cada modelo é uma linha com seus usos como opções e o preço e o raciocínio recolhidos embaixo. No celular os cartões e as tabelas ficam em uma coluna
- **Funcionalidades dos planos (Super Admin)** *(Mega)* - Ao criar ou editar um plano, as funcionalidades aparecem como na aba de funcionalidades da conta: um cartão por categoria com quantas o plano inclui, cada funcionalidade com o nome, o interruptor e a etiqueta Premium, filtros Todas / Incluídas / Não incluídas com os totais e busca. As ações Usar padrão, Selecionar tudo e Limpar seleção continuam disponíveis e no celular ocupam a largura da tela.
- **Login do Super Admin** *(Mega)* - Um painel de marca na cor primária da instalação acompanha o formulário: o logo, o que o console cobre (contas e usuários, planos e cobrança, saúde da instância) e, no rodapé e em tom discreto, uma mensagem do Mega escolhida ao acaso, com o domínio e a versão. No celular fica só o formulário, com a mensagem acima dos seletores de idioma e tema. O login permite escolher idioma e tema antes de entrar, e o idioma escolhido é mantido ao entrar. Mostra o logo da instalação (`LOGO`, ou `LOGO_DARK` no painel e no tema escuro). E-mail ou senha incorretos são avisados no idioma do usuário, mantendo o e-mail e com o cursor na senha. O botão de mostrar senha troca de ícone, o de entrar indica que está entrando e não envia duas vezes, e ao entrar volta à página que foi pedida ou ao Dashboard.
- **Modo claro e escuro no Super Admin** *(Mega)* - O menu da conta, na barra lateral, tem um seletor de tema: Claro, Escuro ou Sistema (segue o sistema operacional). A escolha é a mesma do painel de agentes, então os dois mudam juntos, e vale para todas as páginas, o login (com o logo escuro quando configurado), os diálogos, os gráficos e a pré-visualização de scripts, sem piscar ao carregar.
- **Console Super Admin redesenhado** *(Mega)* - Menu lateral agrupado por seção (recolhe para ícones) e, no celular, menu deslizante com barra superior; formulários por seções, listas que viram cartões no celular, pré-visualização ao vivo dos banners globais e preços de adicionais por moeda com uma única ação para preencher a partir de USD. A lista de contas filtra por estado de cobrança com abas que mostram sua porcentagem e combina esse filtro com um de estado ou origem (ativas, suspensas, cortesia, pagamento manual, recentes…); ordena por nome, agentes ou data de criação, filtra enquanto se digita, também busca pelo e-mail dos usuários da conta e no celular mostra cartões com medidores de uso, modo de seleção para ações em massa e um painel inferior de filtros e ordem. Na ficha da conta, Assinatura e pagamentos é dividida em subabas (assinatura, faturas, consumo de IA, movimentos de AI Actions e histórico), as ações da assinatura ficam numa barra no rodapé do seu cartão e no celular faturas, usuários e funcionalidades aparecem em linhas que cabem na tela. Suspender ou reativar a conta é feito pelo Resumo (cartão Status da conta) ou pelo menu ⋯, com a categoria e o motivo que a suspensão pede, sem abrir Editar
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
- **Contexto de apps sincronizado** - Os apps incorporados recebem as definições de atributos personalizados e o tema claro/escuro efetivo; o contexto é atualizado quando esses dados mudam ou a aba é reaberta, e as solicitações de atualização recebem resposta apenas no iframe solicitante.
- **Gestão administrativa** - Os Dashboard Apps de toda a conta só podem ser criados, atualizados e excluídos por administradores; agentes autenticados mantêm acesso de leitura

**Recursos de API:**

- **API REST completa** - Acesso a todas as entidades
- **Webhooks** - Receba eventos em tempo real
- **Escopo respeitado** - Um app de plataforma só obtém usuários existentes que já gerencia, e só cria ou move bots para contas às quais tem acesso
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
- **Chave verificada** - A chave de conta de serviço do Google (`type: service_account`) é validada com o Google ao conectar a integração e sempre que for alterada

### Tradução automática *(Enterprise)*

Fale com cada cliente no idioma dele, independentemente dos idiomas da sua equipe:

- **Leia no seu idioma** - As mensagens do contato e as respostas de bots aparecem no idioma do painel de cada agente, com *Ver original* para ler o que o cliente escreveu
- **Responda no dele** - As respostas dos agentes, saudações, mensagens fora do horário e pesquisas CSAT saem no idioma do cliente; o texto original do agente fica a um clique, também para o cliente no widget web
- **Acompanha o cliente** - O idioma é detectado em cada mensagem, então um cliente que muda de idioma recebe as respostas no novo. Uma mensagem de uma ou duas palavras (o nome de uma cidade, um erro de digitação) não muda o idioma da conversa
- **Captain ou Google Translate** - Escolha o serviço em Configurações → Fluxo de conversa → Tradução; o Captain é o serviço recomendado, porque lê a conversa inteira e mantém respostas curtas como "ok" no idioma certo; o Google Translate fica em *Usar outros provedores* e é cobrado pelo Google na conta do Google Cloud. Contas com o Google Translate conectado continuam usando-o até escolherem, com um botão *Mudar para Captain*. Com o Captain cada tradução usa AI Actions (detectar o idioma é gratuito) e o modelo é escolhido nas configurações do Captain
- **Exatamente como escrito quando necessário** - Notas privadas, templates do WhatsApp, Direct Send, mensagens interativas, campanhas e mensagens encaminhadas nunca são traduzidas; uma resposta que não pode ser traduzida é enviada como foi escrita e marcada para o agente. Se o serviço de tradução falhar, a resposta é enviada mesmo assim
- **Desative em uma conversa** - No menu da conversa (*Desativar tradução automática*) um agente a desativa só naquela conversa: nem as mensagens nem as respostas são traduzidas até que seja reativada no mesmo menu. A conversa mostra quem a desativou ou reativou
- **Desativada por padrão** - Habilitada por conta (função *Auto Translate* no Super Admin) e ativada pelo administrador da conta

### Linear *(Enterprise)*

- **Gestão de tickets** - Crie issues a partir de conversas
- **Sincronização** - Mantenha status atualizados
- **Desvinculação segura** - A partir de uma conversa, só é possível desvincular issues vinculadas a essa mesma conversa

### Shopify *(Enterprise)*

- **Dados do cliente** - Visualize histórico de compras
- **Pedidos recentes** - Contexto de e-commerce

### WooCommerce *(Enterprise/Mega)*

Integração completa com WooCommerce:

- **Conexão de loja** - Vincule sua loja WooCommerce
- **Histórico de pedidos** - Veja pedidos do cliente em contexto
- **Busca por email e telefone** - Encontra pedidos por email e por telefone, mesmo quando a loja salvou o telefone no formato local
- **Webhooks do WooCommerce** - Receba eventos da loja
- **Painel de pedidos** - Visualização de pedidos na conversa

### Stripe no painel do contato

Visualização somente leitura do seu próprio faturamento no Stripe ao lado de cada conversa (separado do faturamento de assinaturas do Mega):

- **Sua própria conta Stripe** - Um administrador a conecta com uma chave de API restrita, salva criptografada
- **Cliente por e-mail** - O cliente do Stripe é encontrado pelo e-mail do contato; se houver vários, o agente escolhe um
- **Assinaturas** - As últimas cinco, com status, preço, quantidade, renovação, fim do teste e cancelamento agendado
- **Faturas recentes** - Número, data, valor e status das últimas cinco faturas
- **Controle de acesso** - Só os agentes que veem a conversa veem seus dados de faturamento; a chave é gerenciada por administradores
- **Desktop e celular** - Uma seção do painel do contato e uma página da folha do contato no celular

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
- **Criar automação** - Depois de criar um SLA, um atalho abre uma nova regra de automação que já o aplica (contas com automações)

### Logs de Auditoria

- **Registro completo** - Toda ação fica registrada
- **Quem, o quê, quando** - Rastreabilidade total
- **Conformidade** - Para requisitos regulatórios
- **Localização rápida de eventos** - Filtre por tipo de evento e intervalo de dias completos, busque pelo nome ou e-mail do usuário que realizou a ação e ordene por data; os filtros podem ser compartilhados pela URL
- **Evidências de exclusão (Super Admin)** *(Mega)* - Um relatório somente leitura filtra por conta as auditorias retidas de destruição de caixas de entrada, conversas, contatos e mensagens; as entradas de Message mantêm o conteúdo original como evidência, mas a API de logs omite esse conteúdo e o payload da mensagem nas listagens. A conta é escolhida com um buscador; uma busca ao vivo (nome, e-mail, telefone, IP ou ID) e um filtro por tipo de registro com contagens restringem a lista, agrupada por dia, e cada auditoria se expande para ver e copiar tudo o que reteve; no celular cada auditoria é um cartão

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
- **Isolamento por conta** - Um usuário que pertence a várias contas pode usar SAML somente se todas confiarem no mesmo provedor de identidade; caso contrário, o convite e o login por SAML são recusados
- **Mapeamento de grupos** - Sincronize grupos/equipes do IdP
- **Força SSO** - Exija SSO para todos os usuários da conta
- **Múltiplos domínios** - Configure SSO para diferentes domínios de email
- **Logout único** - Single Logout (SLO) suportado
- **URL de metadados do IdP** - Cole a URL de metadados do provedor de identidade em vez de copiar à mão a URL SSO, o ID da entidade e o certificado. O Mega lê esses dados da URL, pega o certificado novo quando o atual está para vencer e o botão Atualizar metadados lê tudo de novo quando você quiser. O formulário manual continua disponível

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
- **Telefone no cadastro** *(Mega)* - O formulário de criação de conta pede um telefone opcional (WhatsApp) para a equipe contatar o cliente durante a ativação; o Super Admin mostra o número no cabeçalho da conta com um link direto para o WhatsApp
- **URL do site normalizada** - Salve o endereço com protocolo para integrações e automações posteriores
- **Conexão guiada do Instagram** - Retome a configuração da caixa de entrada após autorizar o Instagram pelo onboarding

### 📅 Mensagens Programadas

Programe o envio automático de mensagens nas suas conversas:

- **Programação flexível** - Escolha data e hora exata para enviar a mensagem
- **Recorrência** - Programe mensagens recorrentes: diário, semanal, mensal ou anual
- **Séries que não param** - As séries semanais saem nos dias escolhidos no fuso horário da conta (Configurações → Geral). Se o próximo envio não puder ser criado, a mensagem enviada mostra o motivo em vez de a série parar em silêncio; os anexos passam para cada envio
- **Templates** - Use templates de mensagens predefinidos para envios programados
- **Anexos** - Inclua imagens, documentos e arquivos em mensagens programadas
- **Status de acompanhamento** - Monitore o status: pendente, enviado, falhou, cancelado
- **Cancelamento** - Cancele mensagens programadas antes de serem enviadas
- **Recuperação e novo envio** - Tente novamente ou reagende uma mensagem com falha, ou programe uma cópia editável de uma mensagem enviada preservando destinatário e anexos
- **API de programação universal** - Programe uma mensagem para telefone, e-mail ou identificador de provedor criando ou reutilizando o contato automaticamente
- **Múltiplas por conversa** - Programe várias mensagens na mesma conversa
- **Histórico** - Consulte o histórico de mensagens programadas e seu status
- **Calendário e lista** - Calendário mensal no horário local, com o horário e o título de cada envio, e lista agrupada por dia que mostra primeiro os próximos envios e abaixo os anteriores (ou um período escolhido). Busca e filtros por status, caixa de entrada e agente nas duas visões, no desktop e no celular
- **Anexos ao editar** - Ao editar uma mensagem pendente aparecem seus arquivos, que podem ser removidos, e é possível adicionar outros (até 15)
- **Detalhe com ações** - O detalhe mostra o erro do provedor e oferece as ações do status: cancelar ou editar uma pendente, tentar de novo ou reagendar uma com falha, enviar de novo uma enviada
- **Pela conversa e pelo Kanban** - O botão do painel do contato e a aba do Kanban listam as mensagens programadas daquela conversa com as mesmas ações e usam o mesmo formulário da página

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
- Apps do WAHA por sessão: interruptores para ativar ou desativar Números de telefone do Brasil, Argentina e México, e Chamadas de voz quando disponíveis, refletindo o estado atual de cada app
- Tela de configuração de sessão comum a WAHA, Evolution e Uazapi: status de conexão claro, vinculação por QR code ou código sem janelas pop-up, interruptores que salvam sozinhos e confirmação antes de recriar ou desconectar a sessão

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
- **Respostas pelo celular** - O que você responde pelo celular ou WhatsApp Web aparece na conversa como mensagem enviada

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
- **Progresso à vista** - Escolha origem e destino com busca, receba o aviso de que a migração não pode ser desfeita e acompanhe ao vivo os contatos, conversas e mensagens migrados

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
- **Sincronização** - Edições recebidas sincronizam automaticamente do WhatsApp Cloud e Notificame sem duplicar a mensagem original
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
- **Busca e filtros da lista em todo o funil** - Na visualização em lista, a busca e os filtros (inclusive a data) procuram em todos os cards do funil, não só nos já carregados, e continuam carregando resultados de 30 em 30
- **Visão em quadro e em lista** - Alterne entre pipeline visual e lista operacional conforme o fluxo da equipe
- **Filtros avançados por inbox/canal/atividade** - Segmente oportunidades por origem e movimentação recente
- **Filtros por etiquetas** - Filtre por etiquetas de conversa em quadro/lista e reflita nas métricas por etapa
- **Colunas configuráveis por usuário** - Mostre ou oculte colunas e mantenha preferências salvas localmente
- **Ficha 360 do item** - Inclui checklist, notas, anexos, agentes atribuídos, ofertas e atributos personalizados
- **Campos globais pela API** - Integrações podem criar ou atualizar atributos do funil com um array estruturado ou um objeto indexado por nome; o objeto usa somente campos configurados no funil
- **Notas longas legíveis** - Abra o texto formatado completo e os anexos em uma visualização com rolagem, com edição direta quando tiver permissão
- **Busca nas relações do item** - Encontre conversas vinculadas com busca remota ao gerenciar relações do item
- **Moeda padrão por conta** - A moeda base do quadro é definida nas configurações da conta (`default_currency`)
- **Fuso horário da conta** - Configurações → Geral escolhe o fuso horário da conta (`settings.reporting_timezone`, UTC quando vazio) usado por relatórios, tarefas, horários do Flow Builder e mensagens agendadas recorrentes
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
- **Mensagem rápida pelo card** - Com a chave *Mensagem rápida* do funil ativa, o menu do card (⋯), o painel do card e a tela de detalhe no celular oferecem *Mensagem rápida*: envia um dos modelos da etapa que se aplicam ao card, ou uma mensagem personalizada, para a conversa vinculada sem abri-la
- **Alertas Kanban** - Notifica membros das equipes selecionadas e agentes atribuídos por automações de etapa, e o agente responsável quando uma tarefa de checklist chega à data limite; alertas dispensados reaparecem após o intervalo configurado no funil apenas enquanto essa tarefa permanecer pendente. Agrupa alertas em um banner não bloqueante e não envia email
- **Consultas otimizadas** - Os contadores do seletor de funis usam consultas leves; as estatísticas preservam os totais por moeda e oferta, e buscas e relatórios reutilizam dados relacionados para reduzir consultas repetidas.
- **Vencimentos ao criar ou duplicar** - Tarefas de checklist com data limite e responsável agendam seu aviso ao serem salvas, inclusive ao serem copiadas para outro card; as cópias notificam a partir do card de destino.
- **Sincronização em tempo real** - Mudanças de etapa e dados do item refletem instantaneamente na lista de chats e no painel do contato
- **Negócios abertos do contato** - Cada funil pode habilitar na Configuração Avançada a exibição de seus itens Kanban abertos em todas as conversas do contato atual; a opção é desativada por padrão, preserva as regras de visibilidade e identifica as conversas relacionadas
- **Painéis autorizados** - O bloco Kanban do painel de conversa e a entrada do sidebar ficam ocultos quando o usuário não tem itens visíveis nem funis disponíveis para adicionar negócios
- **Detalhe Kanban pela conversa** - Os ícones de canal do cartão mostram cada tipo de inbox vinculado: abrem diretamente sua única conversa ou um seletor limitado a esse canal quando há várias, sem recarregar o quadro; no mobile, o detalhe mostra primeiro as informações comerciais e abre o perfil do item em um painel lateral. O painel de contato do drawer oculta conversas anteriores para manter o contexto do item
- **Mensagens não lidas no cartão** - Cada botão de canal mostra quantas mensagens recebidas não lidas suas conversas vinculadas têm, com o mesmo critério da lista de conversas e apenas para as conversas que o usuário pode ver. Quando várias conversas compartilham o canal (por exemplo duas caixas de WhatsApp), o botão soma os contadores e o seletor mostra o de cada uma, primeiro as não lidas. Os botões ficam alinhados com o menu de ações e continuam visíveis com o cartão recolhido. O contador sobe em tempo real a cada mensagem recebida e zera ao abrir a conversa pelo quadro. Cada funil pode desativá-lo em Configuração Avançada → Card
- **Acesso Kanban em tempo real** - Ao adicionar ou remover agentes do funil, o sidebar, a lista de funis e os itens visíveis atualizam sem recarregar
- **Múltiplas conversas vinculadas** - Um mesmo item Kanban pode se relacionar com várias conversas; a primeira permanece como vínculo principal e as adicionais aparecem na aba de relacionamentos, com seletor limitado aos inboxes do funil e ícones de canal
- **Histórico de vínculos por conversa** - Cada conversa vinculada ou desvinculada gera seu próprio evento; o vínculo mostra a caixa da mesma conta e o texto da ação respeita o idioma da interface
- **Uma oportunidade aberta por contato e funil** - A criação automática reutiliza o item aberto do contato e vincula nele novas conversas do Instagram, WhatsApp ou outros inboxes habilitados; cada funil é avaliado separadamente e uma oportunidade ganha ou perdida permite iniciar outra
- **Histórico sem vínculo quebrado** - Se uma conversa vinculada for excluída, o item Kanban permanece como histórico e o vínculo é limpo
- **Acesso Kanban por função e permissão** - Administradores gerenciam todos os funis e itens; agentes e funções com `kanban_view` trabalham os itens autorizados; `kanban_manage` também cria e edita os funis atribuídos, sem excluir, definir o padrão ou alterar a visibilidade
- **Autoatribuição administrativa** - O administrador pode se atribuir e se remover de qualquer item mesmo sem constar entre os agentes ou inboxes do funil; os demais usuários mantêm as regras normais de elegibilidade
- **Visibilidade controlada dos itens** - O criador sempre pode ver seu item; com uma conversa vinculada válida, o responsável só pode vê-lo se também estiver selecionado no funil, e os agentes atribuídos manualmente ao item podem vê-lo; um vínculo stale fica visível somente para administrador e criador. O modo `everyone` do funil permite que todos os seus agentes vejam todos os itens, enquanto `assigned_only` restringe a visibilidade aos agentes autorizados.
- **Agentes flexíveis por funil** - Qualquer membro da conta com acesso ao Kanban pode ser adicionado ao funil, com ou sem inboxes selecionadas; uma função personalizada requer `kanban_view` ou `kanban_manage`. Com inboxes configuradas, atribuições manuais de itens exigem acesso a pelo menos uma. Ao mover um item, seus responsáveis são incluídos automaticamente no funil de destino sem alterar permissões de inbox
- **Configuração e automações protegidas** - A configuração global é somente leitura para os atores Kanban; suas alterações e as automações globais são exclusivas de administradores. `kanban_manage` administra apenas os funis atribuídos ao usuário

---

### 💳 Assinaturas nativas (planos, adicionais e AI Actions)

O operador define e vende seus próprios planos no Super Admin, sem depender de um catálogo fixo. Funciona igual na nuvem e em instalações auto-hospedadas.

**Planos sob medida**

- Cada plano define agentes e caixas de entrada incluídos, recursos habilitados, AI Actions mensais e documentos do Captain.
- Preços mensais, semestrais e anuais por moeda (USD, BRL, EUR), cadastrados pelo operador; "Sugerir a partir de USD" preenche com o câmbio do dia.
- Teste grátis configurável por plano (15 dias por padrão), sem pedir cartão e com avisos 7, 3 e 1 dia antes do fim.
- **Duplicar plano** - No menu de um plano, "Duplicar" cria uma cópia independente com seus limites, preços, gateways, recursos, adicionais e modelos de IA, para montar variações sem configurar tudo de novo. A cópia é criada inativa, com o nome "(cópia)", "(cópia 2)"…, e abre para edição antes de ser ativada.
- Após o cadastro, o administrador vê uma tela de ativação com a conta, progresso de 3 passos e saída, um seletor mensal/semestral/anual (apenas com os intervalos que têm preço), cartões de planos e uma tabela comparativa por grupos (equipe, canais, IA, produtividade, plataforma). O plano padrão vem primeiro e em destaque, com suas formas de pagamento e 4 benefícios resumidos. Cada plano público com dias de teste oferece o seu: o cartão mostra os dias grátis e a data de fim, o botão para começar o teste antes de "Pagar agora" e as condições abaixo dos botões. A conta é suspensa se o teste terminar sem pagamento. Sem plano padrão, o catálogo público é exibido; se nenhum plano tem dias de teste, é preciso pagar para ativar a conta. O idioma do cadastro continua na Cobrança.

**Cobranças com Stripe e Asaas**

- Métodos de pagamento configurados no Super Admin: Stripe (internacional) e Asaas (Brasil, com NFS-e emitida pelo Asaas). As assinaturas do Asaas podem ser pagas com cartão, PIX ou boleto: o Super Admin escolhe quais o gateway oferece, o cliente escolhe ao assinar e pode trocar depois, e no PIX ou boleto paga cada cobrança, adicionais e upgrades incluídos, na página da fatura.
- **Método de pagamento personalizado** - Qualquer provedor com API HTTP é conectado pelo Super Admin sem esperar uma integração nativa: preencha como autenticar (chave de API ou OAuth com botão Conectar), a requisição que cria a cobrança com variáveis como `{{amount}}` ou `{{customer.tax_id}}`, onde vêm o id e o link de pagamento, e a URL de webhook que o Mega fornece para colar no provedor. Para provedores sem webhook, o Mega consulta o status a cada 10 minutos. Toda cobrança (assinatura, renovação, prorrateio, adicionais, AI Actions, cobranças de serviços) é um link de pagamento; o botão Testar envia uma cobrança real e mostra a resposta para configurar os campos.
- Cada moeda aponta para um gateway; o país escolhido no cadastro define a moeda da conta (Brasil em BRL, zona do euro em EUR e os demais na moeda padrão, USD), desde que um gateway a cobre e haja planos com preço nela; sem conversão na cobrança.
- Upgrade é cobrado na hora com prorrateio; downgrade vale a partir do fim do período e nunca exclui agentes ou caixas.
- **Planos exclusivos por conta** - O Super Admin reserva um plano para uma ou mais contas, por exemplo com um preço negociado: só essas contas o veem em Cobrança e assinam pelo gateway, com adicionais e trocas de plano. As outras contas não o veem nem conseguem assiná-lo chamando a API.

**Adicionais e pacotes de AI Actions**

- Os adicionais recorrentes são cobrados pelo preço cheio ao contratá-los, independentemente do que resta do período, e a partir da próxima renovação somam-se ao plano na mesma fatura.
- Ao remover um adicional ele continua ativo até o fim do período pago, sem reembolso; a tela de faturamento mostra "Cancelado em <data>" com um botão **Manter** que desfaz o cancelamento até lá. É recusado um cancelamento que deixe em uso mais agentes, caixas, chamadas ou caixas WAHA do que o que resta. Um adicional que a conta tem continua listado mesmo quando não é mais vendido, então sempre pode ser removido. O Super Admin vê os cancelamentos agendados na aba de faturamento da conta e pode cancelar ou manter um adicional por ali.
- Também não é possível remover um adicional do qual depende outro que continua contratado (WAHA enquanto restam chamadas WAHA): é preciso remover primeiro o dependente ou os dois juntos. Se a conta muda para um plano que já inclui a funcionalidade de um adicional, esse adicional é cancelado sozinho no fim do período e não é cobrado de novo.
- Os adicionais por unidades mostram quantas estão em uso ("Em uso: 1 de 2") na tela de faturamento e na página da conta no Super Admin.
- Catálogo único de adicionais que cada plano pode oferecer com um máximo opcional, com quatro tipos: agente extra, caixa extra, **funcionalidade** (ativa a funcionalidade escolhida ao criá-lo, é cobrado com a assinatura como os agentes adicionais e não é oferecido em planos que já a incluem) e **personalizado** (texto livre para qualquer serviço que o operador venda, cobrado mensalmente com a assinatura ou como pagamento único).
- Um adicional de funcionalidade também pode ser vendido por unidades: **por caixa de entrada** (chamadas WAHA: cada unidade ativa as chamadas em uma caixa; nas demais elas aparecem bloqueadas com "Comprar outra unidade") ou **com caixa incluída** (WhatsApp WAHA, Evolution ou Uazapi: cada unidade soma uma caixa que só esse provedor pode usar, além do limite do plano, e ativa o provedor). Um adicional pode exigir outra funcionalidade (as chamadas só são oferecidas a contas com WAHA), e as unidades em uso não podem ser removidas até liberar as caixas. Os planos, o limite normal de caixas e as exceções do Super Admin continuam funcionando como antes.
- Quando a conta não tem mais caixas de entrada, a tela de nova caixa mostra os canais bloqueados ("Sem caixas disponíveis") com um aviso para comprar uma caixa adicional; o WhatsApp continua aberto só para os provedores cujo adicional ainda tem uma caixa livre.
- Os adicionais personalizados de pagamento único são comprados na tela de faturamento escolhendo a quantidade; depois de pagos aparecem no Super Admin em "Entregas pendentes" e no painel de atenção do dashboard de faturamento até o operador marcá-los como entregues.
- Pacotes avulsos de AI Actions que somam ao saldo do mês, acumulam e vencem em 90 dias.
- **Um preço por modelo** - Cada modelo de IA tem um único preço em AI Actions, o que o operador define em AI Providers (ou o padrão do modelo). É o que a conta vê ao escolher o modelo no Captain, o que o formulário do plano mostra e o que é descontado: cada função cobra com o modelo que realmente usou.
- **Tarefas grandes cobram o que fazem** - Os fluxos de trabalho do Copilot cobram cada passo, cada conversa revisada e cada decisão do filtro prévio; as revisões de conversas do Mega Assistant, cada conversa revisada; a transcrição de chamadas, cada passada do modelo; os áudios, por minuto iniciado; a voz, por blocos de 5 minutos.
- **Saldo negativo visível** - O que já começou termina mesmo se o saldo acabar; se custar mais do que restava, o saldo fica negativo, aparece na tela de billing e no Super Admin, e é descontado primeiro do próximo plano, pacote ou ajuste. Com o saldo zerado ou negativo nenhum trabalho de IA novo começa, nem o que não cobra por si só (sugestões do classificador, voz gerada, FAQs, notas de contato, ditado).
- Os adicionais não somam AI Actions: as AI Actions vêm do plano, dos pacotes e dos ajustes do Super Admin.
- Em uma instalação própria, as contas sem plano nativo não descontam AI Actions e não veem créditos ao escolher o modelo.
- Medidor de consumo por origem (plano, pacotes e ajustes) na tela de cobrança.
- O histórico de pagamentos aparece antes do catálogo e mostra as quatro faturas mais recentes por página, com filtros combináveis por status e conceito.

**Administração**

- Atribuição manual de planos: cortesia, pagamento manual e teste, individual ou em massa com pré-visualização do impacto por conta.
- Contas existentes ficam em modo Legado: mantêm recursos e limites atuais até receberem um plano.
- Pagamento vencido: 7 dias de carência com aviso fixo para administradores e, ao fim, suspensão com reativação automática ao pagar.
- **Cobranças de serviços** - Na ficha da conta (ou pela Platform API), o Super Admin cria uma cobrança única do valor que precisar, como consultoria, implantação ou migração de dados, com descrição, vencimento opcional e nota interna. Os administradores da conta recebem um e-mail, veem um banner em todo o app e pagam pelo banner de Faturamento ou pelo histórico de pagamentos pelo gateway da sua moeda (Stripe, Asaas com cartão, PIX ou boleto, dLocal Go ou PayPal). Se não for paga, fica vencida sem suspender a conta; enquanto não for paga, pode ser anulada. A página de Faturamento e os banners se atualizam em tempo real quando uma cobrança é criada, paga ou anulada ou a assinatura muda.
- **Consumo de IA** - O Super Admin mostra as AI Actions cobradas, chamadas, tokens e custo do provedor por período, provedor, conta, modelo e recurso, incluindo projeção mensal e custo por ação.
- **Resultado de IA** - O dashboard de consumo, o de faturamento e a página de cada conta mostram o mesmo demonstrativo de resultados em USD: o cobrado por pacotes, o estimado dos planos, as cortesias à parte (sem somar à receita), o uso que não descontou AI Actions e o resultado final. Inclui a rentabilidade de cada pacote com seu preço mínimo, as AI Actions sugeridas por modelo segundo seu custo real (também ao lado de cada modelo em AI Providers) e o Mega Assistant detalhado por funcionalidade (Captain, relatórios, contatos, conversas etc.). Os dashboards de consumo de IA (Resumo, Rentabilidade, Contas e Detalhamento) e de faturamento (Resumo, Planos e IA) são organizados em abas. Faturamento explica quais números são atuais ou mensais, distingue as assinaturas pagas do total da instalação e mostra ações junto aos créditos usados. Sua aba IA oferece só o seletor de mês porque os resultados abrangem toda a instalação em USD. A lista de contas tem busca e paginação. Na página de cada conta, cada fatura diz o que cobrou (plano e intervalo, add-ons e quantidades, pacote de AI Actions ou para qual plano mudou um rateio), com filtros por conceito e status, e os movimentos de AI Actions têm busca, filtros por tipo, bolsa, função e datas, e paginação. O resumo de consumo de IA mostra primeiro resultado, receita e custo total do LLM, depois distingue ações cobradas, créditos usados e cortesias. Suas abas explicam quais valores seguem o período selecionado e quais usam preços atuais ou os últimos 30 dias.
- **Receita** - O Super Admin mostra o MRR por moeda (preços semestrais e anuais distribuídos em 6 e 12 meses), o recebido e o valor a receber, a tendência de recebimentos de 12 meses por assinaturas, adicionais, AI Actions e serviços, MRR por plano, assinaturas por status, recebimentos por gateway e tipo de fatura, entradas e saídas do período e as faturas vencidas mais antigas.

---

## 🔐 Segurança e Conformidade

- **Auditoria mais completa** - Logins e logouts mostram a localização por IP e o histórico de suspensões indica quem suspendeu cada conta
- **Conteúdo HTML seguro** - Mensagens Markdown, instruções do Captain e links dos termos de cadastro filtram conteúdo perigoso, preservando links internos de ferramentas e incorporações confiáveis de artigos.
- **Aviso de personificação** - Quando um Super Admin entra como outro usuário, o painel indica com um banner e permite sair com um clique
- **Conexão de canais só para administradores** - Só os administradores da conta podem conectar ou reconectar páginas do Facebook e números de WhatsApp (cadastro incorporado, WAHA e Evolution)
- **Nomes sempre como texto** - Os nomes de contatos (também ao mesclá-los), respostas prontas e macros, e o conteúdo das notificações são exibidos como texto e nunca interpretados como HTML

### Autenticação

- **2FA/MFA** - Autenticação de dois fatores
- **2FA no Super Admin** - Os super administradores com a autenticação de dois fatores ativada digitam o código do app depois da senha. A etapa do código expira em 5 minutos e é cancelada após 5 códigos errados. O console não tem páginas próprias de recuperação de senha, cadastro ou confirmação.
- **Links de redefinição com validade** - Os links para redefinir a senha expiram em 6 horas; os de convite, em 7 dias. Se a nova senha for rejeitada, o convite continua pendente.
- **Troca de email com senha** - Trocar o email do perfil pede a senha atual, assim como trocar a senha; o campo aparece ao editar o email.
- **2FA obrigatório por conta** - Em Configurações → Segurança (disponível em todos os tipos de instalação), os administradores podem exigir a autenticação de dois fatores de todos os membros. Quem não tiver a configura na própria tela de login (código QR, código e códigos de backup) no próximo acesso com senha; logins com Google e SAML ficam isentos, e ninguém pode desativar o próprio 2FA enquanto for obrigatório. Tokens de API, MCP e OAuth de membros que não ativaram deixam de funcionar nessa conta até que ativem
- **Verificação de novos dispositivos (Cloud)** - Quando ativada, a entrada com senha em um dispositivo desconhecido exige um código de seis dígitos por e-mail. Dispositivos verificados podem ser lembrados por 30 dias; alterar a senha ou o e-mail revoga essa confiança. SSO e 2FA mantêm seus próprios fluxos.
- **SAML/SSO** - Single Sign-On empresarial
- **Tokens de API** - Acesso programático seguro
- **Suporte para conta suspensa** - Usuários suspensos veem o aviso de política com uma ação direta para contatar o suporte; administradores no Cloud também podem abrir o faturamento para regularizar o pagamento e restaurar o acesso. Superadministradores registram uma categoria e um motivo para cada suspensão e podem consultar ou corrigir a entrada mais recente nos detalhes da conta.
- **Cancelamento programado da assinatura** - A Cobrança Cloud mostra a data em que uma assinatura Stripe será encerrada e mantém o plano ativo até o fim desse período.
- **Reenvio de confirmação** - Superadministradores podem reenviar o e-mail de confirmação de um usuário pendente pelos detalhes, sem expor links ou tokens.

### Privacidade

- **GDPR Ready** - Conformidade com regulamentações
- **Exclusão de dados** - Direito ao esquecimento
- **Exclusão de conta pelo Super Admin** - Remove usuários vinculados apenas àquela conta; preserva usuários compartilhados e Super Admins
- **Exportação** - Portabilidade de dados

### Infraestrutura

- **Criptografia em trânsito** - HTTPS obrigatório
- **Criptografia em repouso** - Dados protegidos
- **Backups automáticos** - Recuperação de desastres
- **Autoescalonamento de workers por fila** - Publicação opcional no CloudWatch de latência, profundidade, jobs enfileirados e utilização do Sidekiq para ajustar a capacidade conforme o backlog
- **Filas sem consumidor** - Alerta no Super Admin e erro em log/Sentry quando há jobs do Sidekiq esperando numa fila que nenhum worker lê, como uma fila nova que falta num Sidekiq dividido
- **Proteção de licença** *(Mega)* - Verificação de integridade para reforçar controle de deploy
- **Observabilidade de release** - Melhor rastreabilidade de erros por versão no monitoramento
- **Super Admin no seu idioma** *(Mega)* - Cada super administrador escolhe português (Brasil), espanhol ou inglês no menu lateral; a preferência é compartilhada com o perfil do painel de agentes

---

## 📱 Aplicativos

### Aplicativo Web Progressivo (PWA) *(Mega)*

MEGA funciona como um **Progressive Web App** completo: instale em qualquer dispositivo e tenha uma experiência idêntica a um app nativo, sem passar por lojas de aplicativos.

**Instalação e Experiência Nativa:**

- **Instalável com um toque** - Banner inteligente que aparece automaticamente em dispositivos móveis convidando a instalar o app
- **Desktop e celular** - Funciona no Chrome, Edge, Safari (iOS/macOS) e qualquer navegador compatível com PWA
- **Tela cheia** - Executa em modo standalone, sem a barra de endereços do navegador
- **Gestos na lista de conversas** - No celular, deslizar uma conversa para a esquerda mostra Atribuir (primeiro se escolhe agente ou equipe), Etapa quando há um negócio aberto, Adiar quando está aberta e Resolver; deslizá-la para a direita mostra Excluir (somente administradores), que pede confirmação antes de excluí-la; mantê-la pressionada a seleciona, como no WhatsApp, e no topo aparecem Fixar/Desafixar e Excluir (somente administradores, com confirmação) junto às ações da barra inferior
- **Splash screen personalizada e ágil** - Tela de carregamento com sua marca que desaparece assim que o Vue pinta a interface, com limite de segurança se a inicialização falhar
- **Esqueletos de carregamento em toda parte** - Em qualquer largura de tela, cada página mostra a forma do seu conteúdo enquanto carrega; a tela de conversas (lista, chat e painel de contato) aparece toda de uma vez quando tudo está pronto, e a inicialização lembra se o painel de contato estava aberto
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

- **Alertas de transferência do bot** - Uma conversa pendente transferida para atendimento humano ativa o som e o indicador da aba após uma breve espera. Respeita os filtros de atribuição e visibilidade dos alertas de áudio; notas privadas do Captain não geram um segundo aviso.
