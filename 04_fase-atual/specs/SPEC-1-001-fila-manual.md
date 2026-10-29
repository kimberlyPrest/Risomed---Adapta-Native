# SPEC-1-001 — Fila manual estruturada de leads

**Fase:** 1
**Status:** emendada — **Emenda 01/2026 (29/10/2026)** · operativa
**Dono:** Consultora (Kim) — desenho e emenda; Alexandre (champion) — construção no Skip; SDR/comercial Risomed — operação
**Origem no escopo:** RF-01, Fase 1 (escopo definitivo 10/09), RN-04, RN-07
**Degrau da solução:** **aplicação web no Skip Cloud (PocketBase)** — tela "Fila Manual" sobre a coleção `fila_leads`. Decisão do champion (12/10) formalizada pela Emenda 01/2026 (29/10). A restrição da F1 permanece: **sem integração automática com o Agendor e sem disparo automático de e-mail**; a captação continua manual.

## Resultado observável

O SDR da Risomed abre uma única fila (tela "Fila Manual") e vê todo lead B2B da semana com estágio do funil, tag ICP e próxima ação com data — sem depender de memória, e-mail ou CRM. O cliente consegue demonstrar: "todo lead que entra está aqui, com o que fazer a seguir".

## Limites e dependências

- **Inclui:** estrutura da fila (campos, estágios, tags, regras de preenchimento aplicadas no servidor), documento de uso de 1 página, rotina de captação manual (quem monitora formulário/e-mail e com que frequência).
- **Fora de escopo:** automação de qualquer etapa; integração com Agendor; disparo de e-mail (SPEC-1-002); baseline (SPEC-1-004).
- **Entradas e pré-condições:** leads chegam por formulário do site (e-mail) e indicações; acesso de leitura aos e-mails pelo SDR; **pré-condição LGPD da 1ª semana de operação:** segregação de acesso por papel aplicada na coleção `fila_leads` (CA-1-01e) e política provisória de acesso/retenção de PII registrada por escrito (mesmo provisória, com prazo — SPEC-1-006). Nenhum registro com PII real antes disso.
- **Saídas/artefatos:** aplicação operando (tela "Fila Manual") + documento de uso + rotina de captação definida.
- **Dependências e responsáveis:** adoção diária pelo SDR (dono operacional definido com Alexandre — CA-1-06); Alexandre constrói e evolui a aplicação; consultora desenha, revisa e aprova os critérios.
- **Risco e plano B:** SDR não adotar a fila → reunião de alinhamento com Alexandre; fila simplificada (menos campos) como fallback. Plataforma não suportar um critério → emenda registrada, nunca critério abandonado em silêncio.
- **Rollback ou reversão:** a fila é fonte única de verdade na F1 — export automatizado diário (CSV 15 campos + JSON, retenção de 90 dias) + prova de restauração a partir do arquivo (CA-1-01d) são obrigatórios; perda de dados da fila corromperia o baseline (SPEC-1-004).

## Fluxo e regras

1. SDR (ou rotina definida) verifica formulário/e-mail nos horários definidos na rotina de captação.
2. Para cada lead novo, cria o registro na fila: data de ORIGEM (submissão do formulário/recebimento do e-mail — nunca a data de digitação), empresa, solicitante, contato, nº de vidas, cidade, origem.
3. Aplica tag ICP: `ICP Principal` (10–100 vidas na praça), `Fora ICP` (<10 ou >100 vidas, ou fora da praça), `Incompleto` (sem campos para calcular) — RN-04/RN-07.
4. Define estágio inicial: Prospecção.
5. A cada contato, atualiza estágio (Prospecção → Contato → Apresentação → Proposta → Fechamento → Perdido), registra resultado (data, canal, resumo) e define próxima ação com data.
6. Lead perdido: motivo registrado obrigatório.
7. Registro criado fica vinculado ao autor (`created_by`); alteração e exclusão exigem ser o autor ou ter papel de consultora; papel só-leitura não cria, não altera e não apaga.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Lead novo chega pelo formulário | Registro criado no mesmo dia com origem, tag ICP e próxima ação | Se faltar dado, tag `Incompleto` e registro criado mesmo assim |
| Limite | Lead com 8 vidas fora da praça | Tag `Fora ICP`, prioridade baixa, permanece na fila | Nunca descartado sem registro |
| Falha | SDR esquece de registrar lead | Rotina de captação define dupla checagem diária; violação aparece na revisão semanal | Consultora revisa aderência semanalmente |
| Falha | Conta sem papel tenta apagar registro de outro | Operação recusada pelo servidor (não só oculta na tela) | Registro do erro na trilha; autoria preservada |

## Checklist de execução

- [ ] Coleção `fila_leads` com os 15 campos: data de origem, empresa, solicitante, e-mail, telefone, CNPJ, vidas, cidade, origem, tag ICP, estágio, resultado do contato, próxima ação, data da próxima ação, motivo de perda
- [ ] Estágio e tag ICP restritos à lista **no servidor** (não apenas na tela) e campos obrigatórios rejeitados quando ausentes
- [ ] Documento de uso de 1 página escrito
- [ ] Rotina de captação definida (horários, responsável) e validada com o cliente
- [ ] Treinamento do SDR realizado (sessão gravada ou ao vivo)
- [ ] Regra de fonte única de verdade definida e registrada (fila substitui vs. espelha o Agendor durante a F1) — registro ÚNICO na SPEC-1-006 (governança); aqui apenas referência
- [ ] **Acesso restrito:** cadastro só por chave de convite; chave guardada em cofre de segredos e rotacionada; **papéis só-leitura × editor × dona definidos e aplicados na coleção** (CA-1-01e)
- [ ] Export automatizado diário da fila (CSV + JSON, retenção definida) ativo + prova de restauração a partir do arquivo executada 1 vez

## Critérios de aceite

- [ ] **CA-1-01:** 100% dos leads da semana registrados na fila com estágio, tag ICP e próxima ação com data (auditoria semanal da consultora sobre 1 semana de operação).
- [ ] **CA-1-01a:** campo "data de origem" preenchido com a data de submissão/recebimento — nunca com a data de digitação (prova: comparar 3 leads com o e-mail original).
- [ ] **CA-1-01b:** todo registro tem exatamente uma tag ICP válida e um estágio válido — valores fora da lista são rejeitados **pelo servidor**, não apenas pela interface.
- [ ] **CA-1-01c:** prova negativa de acesso em duas frentes: (a) sem autenticação, a API não devolve nenhum registro da fila nem permite leitura, criação ou alteração; (b) sem a chave de convite o cadastro é recusado, de modo que não existe conta "não autorizada" com acesso; (c) autoria (`created_by`) não pode ser forjada por outro usuário.
- [ ] **CA-1-01d:** prova de recuperação da fonte única de verdade: (a) export completo da fila em CSV com os 15 campos, gerado pela própria aplicação; (b) restauração a partir do arquivo reproduzindo os registros com os campos-chave íntegros (prova campo a campo) e proteção contra duplicata; (c) rotina de backup automatizada com frequência, retenção e responsável registrados por escrito.
- [ ] **CA-1-01e:** prova de segregação por papel, com **duas contas distintas** (champion + conta de teste descartável): conta com papel só-leitura não cria, não altera e não apaga; conta de editor não altera nem apaga registro de outro autor; operações recusadas pelo servidor, não ocultas apenas na interface.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Fila inexistente: coleção nova sem estrutura | Conferir campos obrigatórios e restrições ausentes | Falha: campos/validação não existem | Print da coleção vazia |
| GREEN | Estrutura mínima operando | Criar 3 leads de teste (1 ICP, 1 Fora ICP, 1 Incompleto) com validação ativa | Registros aceitos, tags restritas à lista, estágios válidos | Print da fila com 3 leads |
| REFACTOR/REGRESSÃO | Uso real por 1 semana | Auditoria semanal: cruzar e-mails da semana × registros da fila | 100% dos leads presentes com tag e próxima ação | Registro de auditoria |
| REFACTOR/REGRESSÃO | Prova negativa de acesso (CA-1-01c) | Requisições sem token e cadastro sem chave de convite; tentativa de forjar `created_by` | Leitura vazia, escrita recusada, cadastro recusado, autoria não forjável | Log das requisições com códigos HTTP |
| REFACTOR/REGRESSÃO | Prova de restauração (CA-1-01d) | Criar sonda → exportar → apagar → restaurar do arquivo → conferir campo a campo | Campos íntegros, sem duplicata | Log do script de prova |
| REFACTOR/REGRESSÃO | Segregação por papel (CA-1-01e) | Com 2 contas: só-leitura tenta criar/editar/apagar; editor tenta apagar registro de outro autor | Operações recusadas pelo servidor | Log das requisições (códigos HTTP) por papel |

**Dados/fixtures:** 3 leads de teste (empresa real fictícia: 45 vidas Campinas = ICP; 5 vidas Recife = Fora ICP; lead sem nº de vidas = Incompleto) + 2 contas (champion e conta de teste descartável).
**Caminhos de erro obrigatórios:** lead sem dados (tag Incompleto), lead duplicado (nota no registro existente, nunca registro novo), lead sem origem identificável (perguntar ao cliente antes de registrar).
**Quando não houver código:** cenário verificável acima — condição inicial (fila vazia), ação (criar leads), resultado esperado (estrutura respeitada), evidência (log/auditoria).

**Evidência exigida:** link da aplicação + log das provas negativas por critério + print da auditoria semanal + documento de uso.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| TASK-1-001 | Fila manual estruturada de leads | Alexandre (champion) | SPEC-1-001 | CA-1-01, 01a, 01b, 01c, 01d, 01e | Estrutura + provas negativas | Logs HTTP + auditoria | — | 🔶 em execução |
| TASK-1-001a | Segregação de acesso por papel em `fila_leads` | Alexandre (champion) | SPEC-1-001 | CA-1-01e | Prova com 2 contas | Log HTTP das recusas | Acesso ao Skip Cloud + migração aplicada | ⏳ não iniciada |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| 2026-10-29 | Verificação de fechamento de 28/10 (champion) — divergência entre SPEC (Google Sheets) e sistema (Skip) | **Emenda 01/2026** · TASK-1-001a | Plataforma migrada de planilha para aplicação Skip por decisão do champion; CA-1-01c e CA-1-01d citavam recursos exclusivos do Sheets (link de planilha, histórico de versões). CA-1-01d reescrito para export + restauração por arquivo (capacidade real do provedor); segregação por papel separada em CA-1-01e para leitura inequívoca do status. Detalhe completo em `04_fase-atual/specs/EMENDA-01-2026-SPEC-1-001.md`. |
