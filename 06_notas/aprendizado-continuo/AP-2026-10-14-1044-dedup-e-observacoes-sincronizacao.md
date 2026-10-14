# AP-2026-10-14-1044 — Bug de duplicação por limite/offset e observações não importadas na sincronização de OPs

- Status: candidato
- Escopo: projeto do cliente (Emília Bem-casados — Nexus)
- Task/SPEC: F3-T010 (manutenção pós-aceite, lotes 6d/6f/6g, 09–14/10)
- Sinal: (1) O caminho de ATUALIZAÇÃO das migrations de sincronização (0046–0061) usava `findRecordsByFilter(col, filtro, sort, 1, 200)` acreditando ser "página 1 com 200" — a assinatura real é (coleção, filtro, sort, LIMITE, OFFSET), então limite 1/offset 200 nunca deletava os itens antigos e cada re-sincronização anexava cópias (soma dos itens = K × quantidade). (2) As observações da seção "OBSERVAÇÕES" dos PDFs nunca foram importadas — os relatórios operacionais mostram `pedidos.obs_embalagem`, que ficava vazio ("EMBALAR SEPARADOS" etc. invisíveis). (3) Ao agrupar por situação, os grupos seguiam a ordem da lista (nome) em vez da ordem de situação.
- Evidência: QA 0.0.177/0.0.178 (migrations 0062/0063), 0.0.180 (fix RelatoriosOperacionais.tsx), 0.0.191 (migration 0065, dia 10/10 = 33 pedidos/6.306 un — 100% conforme resumo da Mara); conferência item a item contra os 157 PDFs; aceite da Mara em 14/10 ("tudo já foi testado na produção em prática").
- Regra reutilizável: em toda migration/hook, `findRecordsByFilter` = (coleção, filtro, sort, LIMITE, OFFSET) — nunca (1, N) achando que é página; a importação de OPs deve trazer composição E observações do PDF na mesma passada; após cada lote, validar "soma dos itens = quantidade_snapshot" em todos os pedidos importados; ao agrupar por uma chave (situação), ordenar os grupos pela chave do grupo e os itens de cada grupo pela ordenação escolhida.
- Quando aplicar: qualquer sincronização/importação de OPs (lotes 5, 6, 7...) e qualquer agrupamento em relatórios.
- Quando não aplicar: listagens simples sem deduplicação; relatórios sem agrupamento.
- Confiança: alta — reproduzido, corrigido e aceito em produção prática; causa raiz confirmada no código das migrations.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto (nomes de clientes citados apenas como exemplos operacionais já presentes no changelog).
