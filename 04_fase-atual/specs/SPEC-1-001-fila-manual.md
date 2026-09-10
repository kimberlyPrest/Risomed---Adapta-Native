# SPEC-1-001 — Fila manual estruturada de leads

**Fase:** 1
**Status:** planejada
**Dono:** Consultora (Kim) — construção; SDR/comercial Risomed — operação
**Origem no escopo:** RF-01, Fase 1 (escopo definitivo 10/09), RN-04, RN-07
**Degrau da solução:** construção mínima — planilha/kanban estruturado (Google Sheets) porque a F1 veda integração e o volume atual (poucos leads/semana) não justifica sistema próprio ainda.

## Resultado observável

O SDR da Risomed abre uma única fila (planilha/kanban) e vê todo lead B2B da semana com estágio do funil, tag ICP e próxima ação com data — sem depender de memória, e-mail ou CRM. O cliente consegue demonstrar: "todo lead que entra está aqui, com o que fazer a seguir".

## Limites e dependências

- **Inclui:** estrutura da fila (colunas, estágios, tags, regras de preenchimento), documento de uso de 1 página, rotina de captação manual (quem monitora formulário/e-mail e com que frequência).
- **Fora de escopo:** automação de qualquer etapa; integração com Agendor; disparo de e-mail (SPEC-1-002); baseline (SPEC-1-004).
- **Entradas e pré-condições:** leads chegam por formulário do site (e-mail) e indicações; acesso de leitura aos e-mails pelo SDR; **pré-condição LGPD da 1ª semana de operação:** permissões da planilha aplicadas (CA-1-01c) e política provisória de acesso/retenção de PII registrada por escrito (mesmo provisória, com prazo — SPEC-1-006). Nenhuma linha com PII real antes disso.
- **Saídas/artefatos:** planilha operando + documento de uso + rotina de captação definida.
- **Dependências e responsáveis:** adoção diária pelo SDR (dono operacional definido com Alexandre — CA-1-06); consultora constrói e treina. **Fallback de viagem (11–25/09):** decisões coletadas por escrito com prazo 25/09; fila opera com regras provisórias da consultora registradas como tal (mesmo padrão da SPEC-1-006).
- **Risco e plano B:** SDR não adotar a fila → reunião de alinhamento com Alexandre na volta da viagem (25/09); fila simplificada (menos colunas) como fallback.
- **Rollback ou reversão:** a fila é fonte única de verdade na F1 — export semanal (CSV/XLSX) + prova de restauração de versão (CA-1-01d) são obrigatórios; perda de dados da fila corromperia o baseline (SPEC-1-004).

## Fluxo e regras

1. SDR (ou rotina definida) verifica formulário/e-mail nos horários definidos na rotina de captação.
2. Para cada lead novo, cria linha na fila: data de ORIGEM (submissão do formulário/recebimento do e-mail — nunca a data de digitação), empresa, solicitante, contato, nº de vidas, cidade, origem.
3. Aplica tag ICP: `ICP Principal` (10–100 vidas na praça), `Fora ICP` (<10 ou >100 vidas, ou fora da praça), `Incompleto` (sem campos para calcular) — RN-04/RN-07.
4. Define estágio inicial: Prospecção.
5. A cada contato, atualiza estágio (Prospecção → Contato → Apresentação → Proposta → Fechamento → Perdido), registra resultado (data, canal, resumo) e define próxima ação com data.
6. Lead perdido: motivo registrado obrigatório.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Lead novo chega pelo formulário | Linha criada no mesmo dia com origem, tag ICP e próxima ação | Se faltar dado, tag `Incompleto` e linha criada mesmo assim |
| Limite | Lead com 8 vidas fora da praça | Tag `Fora ICP`, prioridade baixa, permanece na fila | Nunca descartado sem registro |
| Falha | SDR esquece de registrar lead | Rotina de captação define dupla checagem diária; violação aparece na revisão semanal | Consultora revisa aderência semanalmente |

## Checklist de execução

- [ ] Planilha criada com colunas: data de origem, empresa, solicitante, e-mail, telefone, CNPJ, vidas, cidade, origem, tag ICP, estágio, resultado do contato, próxima ação, data da próxima ação, motivo de perda
- [ ] Validação de dados nas colunas de estágio e tag ICP (lista suspensa)
- [ ] Documento de uso de 1 página escrito
- [ ] Rotina de captação definida (horários, responsável) e validada com o cliente
- [ ] Treinamento do SDR realizado (sessão gravada ou ao vivo)
- [ ] Regra de fonte única de verdade definida e registrada (fila substitui vs. espelha o Agendor durante a F1) — registro ÚNICO na SPEC-1-006 (governança); aqui apenas referência
- [ ] **Permissões da planilha restritas:** compartilhamento por convite apenas (comercial + consultora), NUNCA por link público; prova negativa executada (acesso de conta não autorizada falha)
- [ ] Export semanal da fila (CSV/XLSX) agendado + prova de restauração de versão anterior (histórico do Sheets) executada 1 vez

## Critérios de aceite

- [ ] **CA-1-01:** 100% dos leads da semana registrados na fila com estágio, tag ICP e próxima ação com data (auditoria semanal da consultora sobre 1 semana de operação).
- [ ] **CA-1-01a:** coluna "data de origem" preenchida com a data de submissão/recebimento — nunca com a data de digitação (prova: comparar 3 leads com o e-mail original).
- [ ] **CA-1-01b:** toda linha tem exatamente uma tag ICP válida (validação por lista suspensa impede valor fora da lista).
- [ ] **CA-1-01c:** prova negativa de acesso: abertura da planilha a partir de conta NÃO autorizada falha ou exige solicitação de acesso (RNF-03 — PII só comercial + consultora).
- [ ] **CA-1-01d:** prova de restauração: versão anterior da planilha restaurada via histórico do Sheets com colunas-chave íntegras (backup da fonte única de verdade).

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Fila inexistente: abrir planilha nova sem estrutura | Conferir colunas obrigatórias ausentes | Falha: colunas/validação não existem | Print da planilha vazia |
| GREEN | Estrutura mínima operando | Criar 3 leads de teste (1 ICP, 1 Fora ICP, 1 Incompleto) com validação ativa | Linhas aceitas, tags restritas à lista, estágios válidos | Print da fila com 3 leads |
| REFACTOR/REGRESSÃO | Uso real por 1 semana | Auditoria semanal: cruzar e-mails da semana × linhas da fila | 100% dos leads presentes com tag e próxima ação | Planilha de auditoria |
| REFACTOR/REGRESSÃO | Prova negativa de acesso (CA-1-01c) | Abrir o link da planilha de conta não autorizada (ex.: conta de teste da consultora fora do domínio) | Acesso negado ou solicitação exigida | Print da tela de acesso negado |
| REFACTOR/REGRESSÃO | Prova de restauração (CA-1-01d) | Restaurar versão anterior via histórico do Sheets e conferir colunas-chave | Colunas e dados íntegros | Print do histórico + planilha restaurada |

**Dados/fixtures:** 3 leads de teste (empresa real fictícia: 45 vidas Campinas = ICP; 5 vidas Recife = Fora ICP; lead sem nº de vidas = Incompleto).
**Caminhos de erro obrigatórios:** lead sem dados (tag Incompleto), lead duplicado (nota na linha existente, nunca linha nova), lead sem origem identificável (perguntar ao cliente antes de registrar).
**Quando não houver código:** cenário verificável acima — condição inicial (planilha vazia), ação (criar leads), resultado esperado (estrutura respeitada), evidência (print/auditoria).

**Evidência exigida:** link da planilha + print da auditoria semanal + documento de uso.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| — | *preenchido por gerar-tasks* | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
