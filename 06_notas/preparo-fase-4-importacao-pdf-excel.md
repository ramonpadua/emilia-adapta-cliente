# SPEC-F4-IMP — Importação assistida de pedidos por PDF ou Excel

**Status:** planejada por autorização do consultor em 26/10/2026; não liberada para implementação.
**Fase:** 4, somente depois de F3 aceita e liberação expressa do consultor.
**Origem:** 3ª call (08:22–10:42) e decisões do Ramon nesta conversa de 26/10.
**Resultado:** Fernanda pode usar o aplicativo para importar pedidos por PDF OU Excel, com conferência, sem depender do chat e sem duplicar pedidos quando a API voltar. É incremento novo, não reabertura da F3-T010.

## Fronteira e degrau

Reutilizar os registros canônicos, permissões e mecanismo de importação já existentes quando comprovadamente adequados; adicionar a entrada de arquivos no aplicativo. Não presumir que a importação assistida por chat já é uma interface pronta. Não substituir ERP, reescrever dados aceitos, alterar políticas comerciais, liberar produção, publicar ou implementar estoque.

## F4-IMP-001 — Fechar modelos e contrato com Fernanda

**Dono:** Fernanda (decisão) com apoio do Maestro. **Status:** aguardando liberação F4; após liberação, elegível para levantamento interativo, sem implementação.
Antes de agir, explicar o objetivo das três tasks e o resultado desta: modelos e regras aprovados, não botão implementado. Procurar exemplos já fornecidos; pedir apenas o que falta:
- PDF representativo do GestãoClick e Excel representativo do formato que ela usará, incluindo um caso de alteração. Se algum formato ainda não existir, perguntar como ela o obterá; não inventar colunas/layout nem declarar suporte pronto.
- Confirmar se PDF é textual ou digitalizado, páginas, arquivos por lote, planilhas/abas/cabeçalhos, datas/números/unidades e campos obrigatórios por transição. PDF ilegível, digitalizado sem extração validada ou layout não suportado não pode gerar dados por palpite; informar a limitação e pedir arquivo compatível ou ajuste autorizado.
- Confirmar mapeamento com exemplos: identificação OP/cliente, composição/sabores/papel/fita/acessórios/observações, quantidade, prazo e situação quando presentes. Ausência ou ambiguidade é pendência, nunca valor inventado.
- Identificar o campo externo estável no mesmo tenant e o contrato usado pela futura API. Confirmar regra de duplicidade, versão e precedência PDF/Excel/resumo/API. Preservar decisões existentes (resumo da Champion prevalece no conflito já documentado), mas não extrapolar para conflitos de API sem decisão. Registrar divergências; nenhuma sobrescrita silenciosa.
- Confirmar quem importa/confere/aprova, volume/tamanho necessário, destino e retenção dos arquivos, tratamento de dados pessoais e procedimento de recuperação de lote parcial. Validar estruturas e mecanismo de transação/reversão existentes antes de especificar comportamento. Não enviar arquivos a serviços externos não autorizados.
**Aceite IMP-01:** modelos PDF/Excel identificados, mapeamento por campo, chave, perfis, limites, conflitos e recuperação documentados e aprovados explicitamente pela Fernanda, com revisão do consultor se mudar regra. Registrar fixtures de teste sem dados pessoais reais.
**Ponto de parada:** qualquer regra material ou acesso faltante mantém implementação bloqueada; perguntar à Fernanda. Não selecionar tecnologia ou parser por pressuposto. Completar/revisar a SPEC antes da task seguinte.

## F4-IMP-002 — Implementar botão e fluxo de conferência

**Dono:** responsável técnico. **Status:** bloqueada por IMP-001, SPEC complementada/revisada e autorização de implementação.
Exibir “Importar dados” com opções “PDF” e “Excel”. Validar arquivo no servidor (tipo real, tamanho e autorização), extrair para uma prévia temporária, mostrar pedidos/itens e pendências, exigir conferência explícita antes de persistir. Arquivo inválido ou leitura incerta deve falhar de modo explicado e sem gravação canônica. Corrigir mapeamento só conforme contrato aprovado; nunca preencher regra faltante por IA.
Usar a mesma identidade externa da API para inserir/conciliar no tenant. Reenvio do mesmo arquivo, OP já existente, formatos distintos e repetição posterior da API não podem criar duplicidade. Conflitos exigem resolução autorizada; preserve aprovações, pagamentos, versões e histórico. Garantir composição/quantidade e observações conforme contrato; erro de uma linha é visível e não pode desaparecer num sucesso global. Persistência, lote parcial e recuperação seguem IMP-001; se o backend não puder cumprir, parar e devolver ao consultor.
Manter auditoria com ator, origem, lote, resultado e IDs, sem segredos. Não expor dados entre perfis/tenants. Integração externa só sob prova e autorização própria; não conectar API durante esta task por inferência. Ambiente de teste deve ser validado: preview e produção compartilham backend no projeto, logo preview NÃO é isolamento; sem base segura/fixtures autorizadas, parar antes de gravar.
**Aceites IMP-02 a IMP-05:** PDF e Excel aprovados percorrem arquivo→prévia→confirmação→registro correto; negar sem permissão/tenant; rejeitar inválido/incompleto sem gravação indevida; repetição/conflito sem duplicidade ou perda. Evidência: testes executados, fixtures, logs minimizados, capturas e instrução de teste à Fernanda.
**Ponto de parada:** não publicar nem gravar em base real sem autorização específica; não fechar sem teste humano explícito.

## F4-IMP-003 — Teste humano, recuperação e reconciliação com API

**Dono:** Fernanda com apoio técnico. **Status:** bloqueada por IMP-002 aceita; cenário real de API depende da conexão F4 comprovada.
Explicar o teste em linguagem simples. Demonstrar PDF e Excel, prévia/cancelamento, arquivo repetido, OP alterada, campos faltantes, perfil indevido e falha/interrupção de lote segundo contrato. Conferir totais e composição. Provar que o mesmo pedido vindo depois pela API usa o vínculo canônico; enquanto API não estiver disponível, fixture prova o contrato, mas o cenário real fica explicitamente pendente e não é declarado validado.
**Aceite IMP-06:** Fernanda testa e confirma explicitamente; resultado e conflitos registrados; recuperação comprovada sem apagar histórico; reconciliação real com API comprovada antes do aceite integrado. Falhas retornam à task de origem com autorização, sem corrigir silenciosamente entregas anteriores.

## TDD e rastreabilidade

RED: arquivo inválido, campo ambíguo, reenvio duplicando OP, upload sem permissão, conflito sobrescrevendo aprovação ou falha parcial sem recuperação. GREEN: um PDF e um Excel nos modelos aprovados após conferência. REGRESSÃO: importação/API concorrentes ou repetidas, tenant/perfil indevido, alteração preservando versão, cancelamento de prévia e recuperação de lote.
CA IMP-01 → F4-IMP-001; CA IMP-02–05 → F4-IMP-002; CA IMP-06 → F4-IMP-003. Evidências/testes só são marcados após execução; nenhum executado nesta atualização documental.

## Tasks vinculadas

| ID | Ação | Dono | Critério | Evidência | Pré-condição | Status |
|---|---|---|---|---|---|---|
| F4-IMP-001 | Validar modelos e contrato de importação com Fernanda | Fernanda + Maestro | IMP-01 | modelos, mapeamento e decisões aprovados | F4 liberada pelo consultor | Aguardando liberação F4 |
| F4-IMP-002 | Implementar botão PDF/Excel, prévia e importação segura | Responsável técnico | IMP-02–05 | testes, capturas e aceite humano | IMP-001; SPEC completa/revisada; ambiente e implementação autorizados | Bloqueada |
| F4-IMP-003 | Testar importação e reconciliação com a API | Fernanda + técnico | IMP-06 | roteiro e aceite explícito; prova API | IMP-002 aceita; API comprovada para cenário real | Bloqueada |

## Condução interativa

## Condução interativa — orientação do consultor em 26/10/2026

Antes de CADA task, explicar em português simples: em qual fase estamos, o que esta tarefa resolve, o que será feito, o que não será alterado e o que Fernanda deverá observar/testar. Identificar o resultado pelo nome, não apenas pelo código. Explicar o próximo passo ao concluir.

Consultar primeiro decisões, evidências e informações já fornecidas por Fernanda/Mara. Se faltar informação, arquivo, regra, responsável ou entendimento do processo, perguntar diretamente à Fernanda; não inventar, pesquisar uma regra genérica para substituir a dela ou executar com pressuposto. Pedir exemplos reais quando necessário. Fazer perguntas curtas, por blocos pequenos, registrando a resposta antes de continuar o trecho dependente. Não repetir perguntas já respondidas; apresentar o entendimento registrado e perguntar somente a lacuna ou contradição.

Executar uma task por vez, dentro da autorização aplicável, mostrar a prova e pedir teste/aceite humano explícito antes da próxima. Informação recebida não é autorização para enviar mensagens, publicar, alterar dados reais ou executar emendas fora desta decisão. Nunca compartilhar credenciais no texto; usar o mecanismo seguro de secrets do ambiente.

Preservar integralmente entregas e tasks concluídas. Fase 5 permanece integral, não apenas acabamento visual. Estoque está fora desta atualização; será um plus posterior, com detalhamento próprio. Não criar estoque, baixa automática, compras, roteirização ou integrações futuras por iniciativa própria.
