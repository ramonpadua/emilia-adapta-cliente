# SPEC-3-003 — Fila e liberação controlada de produção

**Fase:** 3
**Status:** bloqueada por SPEC-3-001/002 e gate G4
**Dono:** Líder de produção
**Origem (fontes internas da consultoria — não acompanham este pacote):** RQ-003, RQ-006, RQ-009, RQ-011, RQ-012; AC-008; G4
**Degrau:** construção mínima sobre o pedido existente.

## Contexto e decisões fechadas

O pedido possui composição, quantidade e estados financeiro/comercial. A fila operacional deve usar esses snapshots. Somente o Líder libera; Produção atualiza andamento. Pagamento/definição/prazo inválidos impedem liberação. Papel e digital coexistem no piloto.

**Bloqueios:** SPEC-3-001/002 aceitas; líder nominal; dispositivo/acesso; critérios de pagamento/definição; capacidade/janela do piloto; política de urgência.

## Resultado observável

Pedidos aptos entram em `Pronto para produção`; o líder libera e a Produção registra início, andamento, conclusão, falta de material ou impossibilidade. A impressão reproduz composição, quantidade e prazo sem divergência.

## Limites

- Inclui fila, RLS, estados, instrução canônica, impressão e ocorrência operacional.
- Fora: baixa de estoque, compras, planejamento integral, promessa emergencial, remoção do papel.
- Rollback: devolução auditada para pendência/ocorrência; nunca apagar execução.

## Regras

| ID | Condição | Resultado | Exceção |
|---|---|---|---|
| RN-3-201 | pagamento/definição/prazo válidos | apto para avaliação do líder | qualquer gate ausente → pendência |
| RN-3-202 | liberação | somente Líder de produção | demais perfis → 403 auditado |
| RN-3-203 | alteração após liberação | ocorrência + nova versão/instrução | não sobrescrever snapshot |
| RN-3-204 | falta/impossibilidade | ocorrência com dono e próxima ação | não marcar concluído |
| RN-3-205 | liberação repetida/concorrente | reutilizar o mesmo evento/estado | nunca duplicar fila nem prioridade |
| RN-3-206 | impressão | gerar visão imprimível/PDF com ID e versão do pedido | hash/campos devem equivaler à fila digital |

## Fluxo

Pedido apto → Pronto para produção → líder libera → Em produção → Pronto para expedição, ou Ocorrência. Fila impressa carrega ID/versão para reconciliação.

## Instruções Ethos

Alterar somente coleções/hooks/telas da operação. Usar migrations aditivas. Não publicar em produção. Parar se líder/gates/piloto não estiverem aprovados.

## Critérios de aceite

- [ ] **CA-3-015:** pedido sem gate aplicável não aparece como liberado e mostra motivo/dono.
- [ ] **CA-3-016:** somente Líder libera/altera prioridade; tentativa indevida é negada/auditada.
- [ ] **CA-3-017:** fila mostra composição, quantidade, prazo, prioridade, versão e pendências do pedido.
- [ ] **CA-3-018:** Produção registra início, andamento, conclusão, falta ou impossibilidade sem alterar preço/pagamento.
- [ ] **CA-3-019:** alteração tardia preserva versão anterior e gera ocorrência/reconfirmação.
- [ ] **CA-3-020:** impressão e digital do mesmo pedido não divergem nos campos canônicos.
- [ ] **CA-3-021:** turno piloto termina com cada item em Pronto para expedição ou Ocorrência atribuída.

## TDD

RED: usuário indevido libera; pedido incompleto aparece apto; impressão divergente. GREEN: caso apto pelo líder. REGRESSÃO: alteração tardia, falta de material, reimpressão e turno piloto. Evidência: logs RLS, capturas, PDF/print hash e aceite do líder.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte | Evidência | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| F3-T006 | Construir fila, gates, RLS e instrução de produção | Responsável técnico | 3-003 | CA-3-015–020 | RED/GREEN | migration, testes, capturas | F3-T005; G4 fechado | Bloqueada |
| F3-T007 | Executar piloto híbrido e aceitar operação | Líder + Champion | 3-003 | CA-3-017–021 | REGRESSÃO/turno | relatório, hashes, aceite | F3-T006 aceita | Bloqueada |

## Emendas

| Data | Origem | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |

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

## Condução interativa — orientação do consultor em 26/10/2026

Antes de CADA task, explicar em português simples: em qual fase estamos, o que esta tarefa resolve, o que será feito, o que não será alterado e o que Fernanda deverá observar/testar. Identificar o resultado pelo nome, não apenas pelo código. Explicar o próximo passo ao concluir.

Consultar primeiro decisões, evidências e informações já fornecidas por Fernanda/Mara. Se faltar informação, arquivo, regra, responsável ou entendimento do processo, perguntar diretamente à Fernanda; não inventar, pesquisar uma regra genérica para substituir a dela ou executar com pressuposto. Pedir exemplos reais quando necessário. Fazer perguntas curtas, por blocos pequenos, registrando a resposta antes de continuar o trecho dependente. Não repetir perguntas já respondidas; apresentar o entendimento registrado e perguntar somente a lacuna ou contradição.

Executar uma task por vez, dentro da autorização aplicável, mostrar a prova e pedir teste/aceite humano explícito antes da próxima. Informação recebida não é autorização para enviar mensagens, publicar, alterar dados reais ou executar emendas fora desta decisão. Nunca compartilhar credenciais no texto; usar o mecanismo seguro de secrets do ambiente.

Preservar integralmente entregas e tasks concluídas. Fase 5 permanece integral, não apenas acabamento visual. Estoque está fora desta atualização; será um plus posterior, com detalhamento próprio. Não criar estoque, baixa automática, compras, roteirização ou integrações futuras por iniciativa própria.
