# Estado atual — Adapta Cliente

- task_id: F3-T007 (executar piloto híbrido e aceitar operação)
- champion: Fernanda (CEO) · pedido de abertura pela Mara (Gestão) em 14/10
- spec: 04_fase-atual/specs/spec-3-003-producao-liberacao-controlada.md (CA-3-017 a CA-3-021)
- etapa: aguardando_autorizacao
- autorizacao_implementacao: ausente — pedido "vamos para a t007" (14/10 10:51) abriu a análise; NÃO autoriza implementação. **Atenção (ver atualização de 31/10): existe autorização da Mara de 29/10 e entrega implementada que nunca foram registradas neste arquivo remoto.**
- teste_humano: pendente — será o turno piloto com o time de produção (CA-3-021)
- verificacao_automatica: pendente — baseline da fila de produção (FilaProducao.tsx, hooks liberar_pedido/andamento_producao, migrations 0043/0044) a rodar antes do piloto
- aprendizado: capturado:06_notas/aprendizado-continuo/AP-2026-10-31-0021-entrega-nao-commitada-e-qa-sem-testes.md (a captura anterior, AP-2026-10-14-1044-dedup-e-observacoes-sincronizacao.md, segue válida e está no controle.md)
- ultima_acao: análise da F3-T007 entregue + fluxo real de produção mapeado com a Mara; produção sem acesso ao sistema (piloto papel na bancada + transcrição por Mara/Fernanda)
- emenda_candidata: E01 — busca (cliente/OP) + filtro por situação + ordenação alternativa + contador/paginação na FilaProducao.tsx (cap de 100 silencioso); pedida pela Mara em 15/10 15h20
- emenda_candidata: E02 — liberação automática com gestão por exceção (pedida pela Mara em 15/10 15h26): gates passam → sistema libera sozinho e notifica; pendência → lista "precisa de você" com motivo/dono e override com justificativa (só hierarquia maior, auditado); muda entrega aceita da T006 → decisão da Fê como champion
- proxima_acao: reconciliar o estado — confirmar com a Mara/Fernanda a entrega de 29/10 e commitar no repositório o que hoje existe só na árvore de trabalho local (ver atualização de 31/10)
- atualizado_em: 2026-10-24T18:25:00-03:00

## Atualização do consultor — 26/10/2026

- Orientação ratificada: retomar T007 com emenda na SPEC-3-003 e no quadro fase.md; produção em papel e retorno por Mara/Fernanda já conhecidos. Não exigir computador na produção nem reconstruir T006/T010/T011.
- Autorização desta atualização é documental/planejamento, não aprovação da E01/E02 nem permissão de publicação ou escrita em dados reais. Confirmar com Fernanda a retomada assistida e a prova faltante, reaproveitando evidências existentes; não pedir novamente informações já disponíveis.
- Próxima ação: explicar objetivo do piloto, apresentar cobertura já provada e lacunas concretas; pedir somente decisões/informações realmente faltantes. T008/T009 continuam dependentes; sem aceite automático.
- Importação PDF/Excel preparada na nota F4 para futura liberação; implementação bloqueada pelos modelos e contrato de dados. F5 integral; estoque fora.

## Recuperação agendada — 31/10/2026 00:21 (somente leitura + fechamento de triagem)

- **Divergência encontrada (risco de perda de trabalho):** a entrega das emendas E01/E02 de 29/10 — recibo `05_entregas/F3-T007-recibo-emendas-E01-E02.md`, entradas de changelog, `fase.md`, `STATUS.md` e o estado local com QA 0.0.193/0.0.194/0.0.195 PASS e migrations 0066/0067 — **existe apenas como alteração não commitada na árvore de trabalho local**. Nunca foi commitada: `git log --all -- 05_entregas/F3-T007-recibo-emendas-E01-E02.md` volta vazio e este arquivo remoto ainda descrevia a situação de 24–26/10.
- **Preservação feita (sem publicar):** o conteúdo foi copiado para `artifacts/f3-t007-entrega-29-10-nao-commitada/` (patch + arquivos) e commitado localmente na branch `wip/f3-t007-emendas-29-10`, criada só para não perder o trabalho. Nada foi publicado, nenhuma task avançou, nenhum teste humano foi aprovado.
- **O que esta recuperação NÃO fez:** não alterou a `etapa`, não promoveu autorização, não concluiu task nem fase, não publicou e não implementou. O estado local diz `aguardando_teste_humano`; este arquivo remoto permanece em `aguardando_autorizacao` de propósito, porque reconciliar essa transição é decisão da Mara/Fernanda na próxima sessão de trabalho, com o commit correspondente.
- **Aprendizado:** capturado em `06_notas/aprendizado-continuo/AP-2026-10-31-0021-entrega-nao-commitada-e-qa-sem-testes.md` e registrado em `controle.md`.
