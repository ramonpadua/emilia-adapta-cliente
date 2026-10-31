# AP-2026-10-31-0021 — Entrega só na árvore de trabalho (nunca commitada) e QA PASS sem testes executados

- Status: candidato
- Escopo: projeto do cliente (Emília Bem-casados — Nexus, repo fnavaar/emilia-adapta-cliente)
- Task/SPEC: F3-T007 (emendas E01/E02) · SPEC-3-003
- Sinal: (1) A entrega das emendas E01/E02 de 29/10 existe apenas como modificação não commitada na árvore de trabalho local: `git log --all -- 05_entregas/F3-T007-recibo-emendas-E01-E02.md` volta vazio e `origin/main` (5d1e473) não contém o recibo nem as entradas de changelog de 29/10. O estado local dizia `aguardando_teste_humano` com QA 0.0.193/194/195 PASS, enquanto o remoto dizia `aguardando_autorizacao`. (2) O QA do Skip reporta PASS em setup/análise estática/build/integrações mesmo sem rodar a suíte de testes do projeto (`qa.test.ran: false`).
- Evidência: `git rev-parse HEAD` = c56ef44 (24/10) contra `origin/main` = 5d1e473; `git show --stat 5d1e473` lista só documentação (`estado-atual.md`, `fase.md`, spec-3-003, nota F4, CLAUDE.md, STATUS.md, changelog.md) e nenhum arquivo de entrega; `git cat-file -e origin/main:05_entregas/F3-T007-recibo-emendas-E01-E02.md` → ausente; recibo `05_entregas/F3-T007-recibo-emendas-E01-E02.md` registra "Invariantes executadas: NÃO — o QA do Skip não roda a suíte (`qa.test.ran: false`)".
- Regra reutilizável: entrega só conta como registrada quando existe no remoto — provar com `git cat-file -e origin/main:<arquivo>` (ou lendo a versão remota) antes de dizer "gravado/entregue"; árvore de trabalho com alteração não commitada é risco de perda, não registro. E ao relatar verificação automática, separar o que a plataforma executou do que apenas foi escrito: build/QA PASS não é prova de teste executado.
- Quando aplicar: qualquer fechamento de task/debug que dependa de gravar no repositório do cliente ou de declarar verificação automática aprovada; qualquer retomada em que o estado local e o remoto divergirem.
- Quando não aplicar: quando o QA do projeto efetivamente roda a suíte (`qa.test.ran: true`) ou quando a presença remota foi comprovada no mesmo turno.
- Confiança: alta — divergência local/remoto medida por comando, e a ausência de testes está escrita no próprio recibo da entrega.
- Privacidade: sem segredo, dado pessoal ou conteúdo bruto.
