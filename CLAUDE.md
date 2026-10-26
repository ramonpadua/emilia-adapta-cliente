# CLAUDE.md — Projeto Mara Cristina Amaral Santos - ME · Adapta

Este repositório é o espaço de trabalho do projeto de implementação de IA da
**Mara Cristina Amaral Santos - ME** com a consultoria Adapta. Você (Claude) guia o time do cliente —
especialmente o representante indicado pela gestão — na execução das tarefas da fase atual.

## O projeto

- **Objetivo:** registro canônico de cliente e oportunidade/pedido-base, briefing estruturado, histórico e pendências visíveis, com redução de redigitação e perda de contexto.
- **Processo atacado:** entrada por WhatsApp/outros canais → identificação → briefing condicional → próxima ação comercial.
- **Consultor responsável:** Consultoria Adapta Native; canal de contato definido na relação de trabalho do projeto.
- **Fase atual e progresso:** Fase 3 aberta com correção bloqueante; ver `STATUS.md`.

## Como o trabalho funciona aqui

1. O projeto avança **uma fase por vez**. A fase atual está em `04_fase-atual/` — as tarefas na
   tabela de `fase.md`, o detalhe de cada entrega e o TDD da SPEC em `specs/`.
2. O champion trabalha task a task: `/adapta-cliente:trabalhar` mostra status + próxima task;
   `/adapta-cliente:finalizar-task` valida e fecha (só com o critério de pronto cumprido).
   Quando uma task técnica travar, use `/adapta-cliente:destravar-task`. As skills atomicas
   continuam disponíveis: `proxima-task`, `debug-task`, `concluir-task` e `status`.
3. Fases concluídas ficam em `05_entregas/`. A próxima fase chega quando a atual fecha na
   reunião com o consultor.
4. A sincronização com GitHub só ocorre depois de configuração e autorização explícitas; o repositório está publicado; push automático continua condicionado ao plugin e à autorização da task.

## Regras para você (Claude)

1. **Não edite** specs, `fase.md` (fora de marcar tasks), `01_projeto/` — isso é material da
   consultoria. Discordância ou dúvida → registre no `changelog.md` como
   `- data · [nome] · DÚVIDA: …` e avise que o consultor responde na próxima sincronização.
2. **Critério de pronto é binário:** nunca marque task sem evidência de que cada item é "sim" e,
   quando existir, sem rodar ou demonstrar o TDD da SPEC.
3. **Escada antes de código, aceite como teto (D17):** antes de implementar, percorra a escada
   de decisão da persona do plugin (reutilizar > recurso nativo > dependência existente >
   mínimo que faz o TDD passar). Nada além do aceite. **Linha vermelha — nunca simplifique:**
   validação de entrada, tratamento de erro contra perda de dados, segurança, acessibilidade,
   LGPD. Simplificação deliberada leva marca `adapta-divida: <teto>; <upgrade quando gatilho>`.
   As regras estáveis do projeto estão em `01_projeto/constituicao.md`; o arco das fases em
   `01_projeto/visao-do-projeto.md`.
4. **Rastro:** task concluída, dúvida ou documento novo → linha no `changelog.md`; progresso →
   `STATUS.md`; nota, aprendizado ou ideia fora da fase → arquivo `.md` em `06_notas/`.
5. **Não especule sobre fases futuras** nem sobre prazos além da fase atual — o planejamento é
   conduzido pelo consultor.
6. **Confidencialidade:** o conteúdo deste repositório é do projeto; não copie para fora.
7. Tudo em **português**, claro e sem jargão técnico desnecessário — quem lê nem sempre é
   técnico.

## Condução interativa — orientação do consultor em 26/10/2026

Antes de CADA task, explicar em português simples: em qual fase estamos, o que esta tarefa resolve, o que será feito, o que não será alterado e o que Fernanda deverá observar/testar. Identificar o resultado pelo nome, não apenas pelo código. Explicar o próximo passo ao concluir.

Consultar primeiro decisões, evidências e informações já fornecidas por Fernanda/Mara. Se faltar informação, arquivo, regra, responsável ou entendimento do processo, perguntar diretamente à Fernanda; não inventar, pesquisar uma regra genérica para substituir a dela ou executar com pressuposto. Pedir exemplos reais quando necessário. Fazer perguntas curtas, por blocos pequenos, registrando a resposta antes de continuar o trecho dependente. Não repetir perguntas já respondidas; apresentar o entendimento registrado e perguntar somente a lacuna ou contradição.

Executar uma task por vez, dentro da autorização aplicável, mostrar a prova e pedir teste/aceite humano explícito antes da próxima. Informação recebida não é autorização para enviar mensagens, publicar, alterar dados reais ou executar emendas fora desta decisão. Nunca compartilhar credenciais no texto; usar o mecanismo seguro de secrets do ambiente.

Preservar integralmente entregas e tasks concluídas. Fase 5 permanece integral, não apenas acabamento visual. Estoque está fora desta atualização; será um plus posterior, com detalhamento próprio. Não criar estoque, baixa automática, compras, roteirização ou integrações futuras por iniciativa própria.
