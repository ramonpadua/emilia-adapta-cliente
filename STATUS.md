# STATUS — Projeto Mara Cristina Amaral Santos - ME

> **Atualizado em:** 2026-10-14 · **Por:** ETHOS (Bia)

## Onde estamos

- **Fase atual:** 3 — jornadas especiais, produção, expedição e entrega.
- **Progresso:** 8/11 tasks concluídas (F3-T001 a F3-T006, F3-T010 e F3-T011).
- **Task elegível:** F3-T007 — executar piloto híbrido e aceitar operação (SPEC-3-003).
- **Tasks bloqueadas:** F3-T008–T009 (dependem do piloto F3-T007).
- **Produção:** não autorizada nesta abertura (backend compartilhado já recebeu as migrations, conforme aceite B3-ENV-01 da Champion).

## Gate atual

**F3-T010 (relatórios operacionais + importação de OPs) e F3-T011 (embrulho por papel + planejamento semanal) CONCLUÍDAS — teste humano aprovado pela Champion em 06/10 ("tudo testado e funcionando").** **Manutenção pós-aceite (09–10/10, a pedido da Mara/Gestão, testada e aprovada em produção prática):** auditoria completa das composições da semana 05/10–11/10 (migration 0062 — 151 pedidos reescritos do PDF; tabela de sabores confere 100%, 16.491 un), dedup de itens duplicados de re-sincronização (migration 0063 — 60 pedidos dos lotes 1–5), importação das observações dos PDFs (migration 0064 — 72 OPs, ex.: "EMBALAR SEPARADOS") e correção da ordenação dos relatórios (situação primeiro, nome/OP dentro da situação). Atualizações do dia 10/10 (migration 0065): 3 novos (42084/42106/42121), 4 alterados (42066 Reserva→Entrega, 35173 residência, 42008/42009 anexos+obs) e OP 42072 movida para degustação 09/10 — dia 10/10 fecha em 33 pedidos / 6.306 un (Entrega 25/5.742 · Reserva 3/540 · Degustação 5/24), 100% conforme resumo da Mara. QA Skip 0.0.192 PASS. Recibos: `05_entregas/F3-T010-recibo-relatorios-operacionais.md` e `05_entregas/F3-T011-recibo-embrulho-planejamento.md`. Próxima: F3-T007 (piloto híbrido com o time de produção, turno real + aceite).

## Decisões incorporadas

- Correções identificadas na auditoria entram na SPEC-3-001 e são pré-condição das demais SPECs.
- Cancelamento até 100 unidades: reembolso integral quando faltarem pelo menos 7 dias; depois, somente Administrador com retenção de 20%.
- Sem data, quantidade ou total confiável: bloquear e criar pendência; não inferir.
- B3-ENV-01: Preview e produção compartilham backend único (nexus-emilia-49529.shrd00); aceite explícito da Champion registrado em 14/09.
- Degustação não é tipo de evento: marcador `solicitou_degustacao` vale para qualquer evento (decisão da Champion em 14/09).
- Parâmetros das jornadas aprovados em 14/09: cortesia presencial/retirada, frete no envio, adicional cobrado na própria degustação, sem limite semanal; revendedor com preço pela data do pedido; bem-nascido com SLA manual + pendência; equipe de vendas acompanha o cliente ponta a ponta.
- Modalidade da degustação: seletor com Presencial (showroom) como padrão, Entrega (envio) e Retirada.
- Parâmetros G3-OPS-01 (produção, 14/09): fila natural = data de entrega; urgência = pedido novo com entrega em até 7 dias; falta de material = ocorrência (RN-3-204); verificação automática de estoque fora do escopo (melhoria futura); sinal/entrada basta para liberar, total pago até a entrega; revendedores/CNPJ com política de recebimento individual.
- Relatórios impressos são para uso operacional: funcional > bonito (Champion, 27/09).
- Sincronização de OPs: em divergência PDF × resumo, o resumo da Champion é a fonte da verdade e a divergência fica registrada no histórico do pedido (lote 5, 01/10).
- Auditoria de composições (09/10, Mara): descrições de embalagem vêm SEMPRE do PDF real, nunca de texto genérico; após cada lote, validar "soma dos itens = quantidade do pedido" em todos os importados (09/10).

## Referências

- `04_fase-atual/fase.md`
- `04_fase-atual/specs/00-INDICE.md`
- `05_entregas/F3-T001-recibo-estabilizacao-repo-tecnico.md`
- `05_entregas/F3-T002-recibo-migrations-seguranca.md`
- `05_entregas/F3-T003-relatorio-recertificacao.md`
- `05_entregas/F3-T004-recibo-jornadas-especiais.md`
- `05_entregas/F3-T005-roteiro-aceite-jornadas.md`
- `05_entregas/F3-T006-recibo-fila-producao.md`
- `05_entregas/F3-T010-recibo-relatorios-operacionais.md`

## Orientação de continuidade — 26/10/2026

T007 permanece a próxima elegível, com roteiro aditivo na SPEC-3-003: papel na produção, retorno por responsável autorizado e aproveitamento das provas já executadas. Nenhuma nova task concluída nesta atualização; 8/11 preservadas. T008/T009 mantêm dependências e aceite humano. E01/E02 não autorizadas por esta atualização. Importação PDF/Excel preparada, não implementada, para a fase 4 após liberação do consultor e fechamento das lacunas pela Fernanda. F5 preservada integralmente; estoque não incluído. Toda task deve começar com explicação simples e perguntas sobre lacunas reais.
