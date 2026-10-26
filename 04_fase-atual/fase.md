# Fase 3 — Jornadas especiais, produção, expedição e entrega

**Estado:** recertificação, jornadas especiais, fila de produção, relatórios operacionais e planejamento concluídos. F3-T001 a F3-T006, F3-T010 e F3-T011 concluídas; F3-T007 é a próxima elegível.

## Regra de execução

Uma task por vez. Teste humano obrigatório após cada task. Nenhuma task publica produção.

## Tasks

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status | Leva |
|---|---|---|---|---|---|---|---|---|---|
| F3-T001 | Materializar repo técnico e implementar correções | Responsável técnico | SPEC-3-001 | CA-3-001/003/007 no código | RED/GREEN local; sem apply Skip | commit técnico, logs e scan | repo Git e patch versionado | concluída (2026-09-13) | 1 |
| F3-T002 | Aplicar migrations e provar segurança na instância autorizada | Responsável técnico | SPEC-3-001 | CA-3-001–006/029 | P1–P7/P11 | ledger de migrations e provas | F3-T001 aceita; B3-ENV-01; secrets; Skip acessível | concluída (2026-09-14) | 2 |
| F3-T003 | Regressão F2 e aceite humano da recertificação | Champion + responsável técnico | SPEC-3-001 | CA-3-007/008/030 | P8–P10/P12 + 11 CAs F2 | relatório e aceite humano | F3-T002 aceita | concluída (2026-09-14) | 3 |
| F3-T004 | Configurar variantes e mínimos das quatro jornadas | Atendimento/Gestão | SPEC-3-002 | CA-3-009–014/031 | RED/GREEN das quatro fixtures | matriz, configuração e fixtures | F3-T003; parâmetros aprovados | concluída (2026-09-14) | 4 |
| F3-T005 | Provar bordas e aceitar jornadas especiais | Champion | SPEC-3-002 | CA-3-009–014/031 | REGRESSÃO de tipo/data/urgência | roteiro, capturas e aceite | F3-T004 aceita | concluída (2026-09-14) | 5 |
| F3-T006 | Construir fila, gates, RLS e instrução de produção | Responsável técnico | SPEC-3-003 | CA-3-015–020 | RED/GREEN de fila e alçada | migration, testes e capturas | F3-T005; G3-OPS-01 | concluída (2026-09-14) | 6 |
| F3-T007 | Executar piloto híbrido e aceitar operação | Líder + Champion | SPEC-3-003 | CA-3-017–021 | REGRESSÃO e turno piloto | evidências existentes + prova faltante, relatório e aceite explícito; piloto em papel | F3-T006 aceita; consultar emenda de 26/10 na SPEC-3-003 | Elegível | 7 |
| F3-T008 | Construir fila, protocolo e ocorrências de entrega | Responsável técnico | SPEC-3-004 | CA-3-022–027 | RED/GREEN expedição | migration, testes e capturas | F3-T007; G3-ENT-01 | Bloqueada | 8 |
| F3-T009 | Executar piloto ponta a ponta e aceitar Fase 3 | Expedição + Champion | SPEC-3-004 | CA-3-022–028 | REGRESSÃO/e2e | relatório e aceite humano | F3-T008 aceita | Bloqueada | 9 |
| F3-T010 | Relatórios operacionais + importação de OPs reais (lotes 1–5) | Responsável técnico + Champion | Recibo F3-T010 | 4 relatórios + importação idempotente + previsões fora do total | QA 0.0.134→0.0.192; totais conferidos com GestãoClick/resumo | recibos, totais, aceite humano | F3-T006 | concluída (2026-10-06) · manutenção pós-aceite: lotes 6d/6f/6g (09–10/10) validados pela Mara | 10 |
| F3-T011 | Embrulho por papel + planejamento semanal (modelo da planilha) | Responsável técnico + Champion | Recibo F3-T011 | lista por sabor/cor + planejamento com RLS admin | QA 0.0.137→0.0.165; persistência validada | recibo, aceite humano | F3-T010 | concluída (2026-10-06) | 11 |

## Handoff

Encerrar somente com CA-3-001–028 provados, gates G3 fechados, piloto híbrido e aceite humano. Falha corretiva mantém a base aberta e bloqueia as demais SPECs.

## Condução interativa — orientação do consultor em 26/10/2026

Antes de CADA task, explicar em português simples: em qual fase estamos, o que esta tarefa resolve, o que será feito, o que não será alterado e o que Fernanda deverá observar/testar. Identificar o resultado pelo nome, não apenas pelo código. Explicar o próximo passo ao concluir.

Consultar primeiro decisões, evidências e informações já fornecidas por Fernanda/Mara. Se faltar informação, arquivo, regra, responsável ou entendimento do processo, perguntar diretamente à Fernanda; não inventar, pesquisar uma regra genérica para substituir a dela ou executar com pressuposto. Pedir exemplos reais quando necessário. Fazer perguntas curtas, por blocos pequenos, registrando a resposta antes de continuar o trecho dependente. Não repetir perguntas já respondidas; apresentar o entendimento registrado e perguntar somente a lacuna ou contradição.

Executar uma task por vez, dentro da autorização aplicável, mostrar a prova e pedir teste/aceite humano explícito antes da próxima. Informação recebida não é autorização para enviar mensagens, publicar, alterar dados reais ou executar emendas fora desta decisão. Nunca compartilhar credenciais no texto; usar o mecanismo seguro de secrets do ambiente.

Preservar integralmente entregas e tasks concluídas. Fase 5 permanece integral, não apenas acabamento visual. Estoque está fora desta atualização; será um plus posterior, com detalhamento próprio. Não criar estoque, baixa automática, compras, roteirização ou integrações futuras por iniciativa própria.

## Emenda de 26/10/2026 — somente F3-T007 pendente

Autorização: Ramon, após a 3ª call com Fernanda. Esta emenda não altera código, regras, critérios ou recibos das tasks concluídas F3-T001–006, T010 e T011; os trechos anteriores permanecem como histórico. O quadro atual é fase.md/STATUS.md: T007 elegível; T008/T009 dependentes. Estados históricos desta SPEC não autorizam reexecutar tasks concluídas.

### Roteiro da F3-T007

1. Explicar: “Vamos conferir, com os relatórios que vocês já usam, se o pedido percorre a produção corretamente. Não vamos reconstruir as entregas já aprovadas nem exigir computador na bancada.”
2. Produção NÃO tem computador/acesso ao sistema. A operação é relatório/papel na bancada, com retorno registrado por Mara/Fernanda ou pessoa autorizada já definida. O dispositivo é do responsável pela transcrição, não pré-condição de computador na produção. Preservar perfis/alçadas existentes; se o retorno exigir outra permissão, parar e pedir decisão, sem ampliar acesso.
3. Reaproveitar nome do líder, fluxo e testes já informados. Ler recibos T010/T011, estado atual e evidências antes de cobrar novo piloto. Comparar a cobertura com CA-3-017–021; executar somente a prova ainda não demonstrada, sem dar aceite global por inferência. Se faltar responsável, janela ou prova, perguntar à Fernanda de forma objetiva.
4. Conferir com ela a operação já descrita: programação por quantidade/sabor → embrulho por tipo/cor de papel → separação por pedido/amarração → acessórios, conferência e embalagem. Essa sequência é roteiro de validação das entregas existentes, NÃO autorização para novos módulos ou reconstrução. Perguntar como ocorre cada retorno apenas se não constar dos registros.
5. Validar instrução vigente, composição/quantidade/prazo, versão do impresso, alteração tardia, falta de material e destino de cada pedido. Aplicar os mesmos CA-3-017–021, preservando histórico e perfis; registrar quem transcreveu e a origem física da informação. Uma lacuna funcional vira ocorrência/dúvida para o consultor, não implementação escondida na T007.
6. Registrar evidências reaproveitadas, prova faltante executada, divergências e veredito explícito da Champion/líder. Parar sem aceite. T008 só avança após T007 aceita; T009 só após T008 e aceite correspondente. Fechar F3 não libera F4 automaticamente: solicitar liberação ao consultor.

E01 (busca/filtros/paginação da fila) e E02 (liberação automática), mencionadas no estado de 24/10, NÃO são autorizadas por esta emenda. Não alterar a T006 concluída nem implementar essas sugestões; perguntar à Fernanda apenas se a decisão pendente bloquear o piloto mínimo e devolver ao consultor a mudança de regra.
