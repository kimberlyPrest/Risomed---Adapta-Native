# NT-2026-10-29 — Resposta da consultora à verificação de fechamento da TASK-1-001

**Data:** 2026-10-29
**Origem:** verificação de 28/10 do champion + pergunta "qual encaminhamento você prefere que eu registre para resolver a divergência com a consultora?"
**Autora:** Kim (consultora Adapta Native)
**Decisão registrada:** Emenda 01/2026 **aprovada e aplicada**

## Resposta direta

**A divergência está resolvida — não é para voltar ao Google Sheets.** A aplicação Skip foi aceita como a plataforma da F1. A Emenda 01/2026 está em `04_fase-atual/specs/EMENDA-01-2026-SPEC-1-001.md` e a SPEC-1-001 já foi reescrita.

## O que mudou nos critérios

| Critério | Antes | Depois |
|---|---|---|
| CA-1-01b | lista suspensa na planilha | rejeição **pelo servidor** (já atende) |
| CA-1-01c | abrir link da planilha com conta não autorizada | 3 frentes: sem token, sem chave de convite, autoria não forjável (já atende) |
| CA-1-01d | restaurar via histórico do Sheets | export CSV 15 campos + restauração por arquivo com prova campo a campo + backup automatizado (**fechado em 28/10**) |
| CA-1-01e | não existia | **novo** — segregação por papel com 2 contas |

## Sobre o bloqueio de acesso ao Skip Cloud

O bloqueio de 28/10 ("falta acesso administrativo") estava **parcialmente equivocado**: as regras da coleção estão na migração versionada `pocketbase/migrations/0004_create_fila_leads.js`, no repo do próprio projeto. Não é necessário painel administrativo para corrigir — é necessário uma migração `0006_*` com as regras novas, o que está no fluxo normal de construção. O único item que realmente exige superusuário é remover a conta de teste `probe.qa.*`.

Desenho mínimo (detalhado na seção 6 da emenda):

| Operação | Regra |
|---|---|
| list / view | qualquer autenticado (a fila é compartilhada por desenho) |
| create | autenticado + `created_by` = próprio usuário |
| update / delete | autor do registro **ou** papel de consultora |

Requer campo/coleção de papel (`role`) na coleção de usuários.

## Estado da TASK-1-001

Não está concluída, mas **deixou de estar bloqueada por decisão da consultora**:

- ✅ CA-1-01b, CA-1-01c, CA-1-01d
- ⏳ CA-1-01 e CA-1-01a — exigem 1 semana de operação real do SDR (não são testáveis tecnicamente)
- ⏳ CA-1-01e — TASK-1-001a

## Revisão do próprio veredito "NÃO PRONTA"

O veredito de 28/10 estava correto **naquele momento**. Dois ajustes de leitura:

1. **A pendência de registro já não existe**: o próprio champion criou `STATUS.md`, `changelog.md`, `04_fase-atual/fase.md` e `.adapta-cliente/estado-atual.md` no commit `3c3c6ba` (28/10 21:48), e `05_entregas/` + `06_notas/` no commit `96b5084` (22:14). A mensagem que apontava ausência desses arquivos é anterior a esses commits.
2. **CA-1-01d foi fechado depois do veredito**, no mesmo dia: o script de backup/restauração com prova campo a campo está em `05_entregas/TASK-1-001/backup-restauracao.md`.

## Método: o que a consultora espera daqui pra frente

- **Sinal vira registro, sempre.** O achado de 22/10 (registros canônicos ausentes) ficou 6 dias sem resposta da consultoria. Este é o segundo ciclo em que um sinal legítimo do champion espera decisão. Fica valendo: todo sinal registrado em `06_notas/` recebe resposta datada em até 1 dia útil.
- **Não parar a fase por um critério isolado.** Quando um critério trava e os outros podem andar, ele é isolado em task própria (foi o que se fez com CA-1-01e) em vez de congelar a task inteira.
- **Critério inexequível na plataforma não vira "não pronta" indefinida** — vira emenda com decisão datada.

## Próximos passos do champion

1. Migração `0006_*` com as regras de segregação + campo de papel; prova com duas contas (champion + conta descartável). Fecha TASK-1-001a / CA-1-01e.
2. Iniciar a operação real do SDR, registrando `data_origem` = data de submissão, para acumular a semana de auditoria (CA-1-01/01a).
3. Não é preciso esperar nada da consultora para começar 1 e 2.
