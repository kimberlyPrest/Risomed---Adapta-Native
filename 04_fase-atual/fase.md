# Fase 1 — Fundação manual (sem integração, sem LP)

**Status:** em execução · **Dependências externas:** nenhuma credencial/token · **Desenho e revisão:** consultora (Kim) · **Construção:** Alexandre (champion) · **Operação:** SDR/comercial do cliente

> Registro de execução da fase atual. O escopo canônico permanece em `fases/fase-1.md`; aqui ficam as tasks, seus donos e o estado real.

## Resultado da fase

A operação comercial da Risomed rodando em uma fila estruturada, com régua de baseline congelada e toda a preparação documentada para a integração da Fase 2 — sem depender de credenciais, token ou qualquer acesso técnico do cliente.

## Tasks da fase

| ID | Task | Dono | SPEC | Critério | Estado | Data |
|---|---|---|---|---|---|---|
| TASK-1-001 | Fila manual estruturada de leads | Alexandre (champion) | SPEC-1-001 | CA-1-01, 01a, 01b, 01c, 01d, 01e | 🔶 em execução — 3 de 6 critérios fechados | 2026-10-29 |
| TASK-1-001a | Segregação de acesso por papel em `fila_leads` | Alexandre (champion) | SPEC-1-001 | CA-1-01e | ⏳ não iniciada | — |
| — | E-mail institucional | — | SPEC-1-002 | CA-1-02, 01-02a | ⏳ não iniciada | — |
| — | Roteiro SPIN + checklist | — | SPEC-1-003 | CA-1-03a, 01-03b | ⏳ não iniciada | — |
| — | Baseline congelado | — | SPEC-1-004 | CA-1-03, 01-03c | ⏳ não iniciada | — |
| — | Preparação de integração | — | SPEC-1-005 | CA-1-04, 01-05, 01-05a | ⏳ não iniciada | — |
| — | Governança da F1 | — | SPEC-1-006 | CA-1-06, 01-06a | ⏳ não iniciada | — |

## TASK-1-001 — detalhe

**Implementação entregue:** aplicação web no Skip Cloud (projeto "Jornada Comercial Risomed", id 57599), coleção `fila_leads` + tela Fila Manual.
**Preview:** https://jornada-comercial-risomed-0b95a--preview.goskip.app

**Emenda 01/2026 (29/10) — aprovada e aplicada.** Formaliza a plataforma Skip em lugar do Google Sheets e reescreve os critérios que citavam recursos exclusivos do Sheets. Documento completo em `04_fase-atual/specs/EMENDA-01-2026-SPEC-1-001.md`. SPEC-1-001 atualizada (status "emendada").

**Verificação de 2026-10-28 (champion) + leitura da consultora em 2026-10-29:**

| Critério | Descrição | Resultado |
|---|---|---|
| CA-1-01 | 100% dos leads da semana na fila com estágio, tag ICP e próxima ação com data | ⏳ estrutura e obrigatoriedades aplicadas pelo servidor; auditoria de 1 semana de operação real não executada |
| CA-1-01a | "data de origem" = data de submissão, nunca de digitação | ⏳ campo presente e obrigatório; comparação com 3 e-mails originais não executada |
| CA-1-01b | exatamente uma tag ICP válida, impedida pelo servidor | ✅ PASSOU — tag e estágio inválidos rejeitados (HTTP 400) |
| CA-1-01c | prova negativa de acesso | ✅ PASSOU — sem autenticação a fila devolve 0 registros e não aceita escrita; sem chave de convite o cadastro é recusado; `created_by` não pode ser forjado |
| CA-1-01d | prova de recuperação da fonte única de verdade | ✅ **PASSOU — 28/10** — export CSV (15 campos) + restauração a partir do arquivo com prova campo a campo e proteção contra duplicata; backup diário automatizado às 22h. Evidência em `05_entregas/TASK-1-001/backup-restauracao.md` |
| CA-1-01e | segregação por papel com 2 contas | ⏳ **novo critério (Emenda 01/2026)** — sem papéis, qualquer conta com a chave de convite lê, altera e apaga todos os leads. Bloqueia o uso com dados reais |

**Estado:** a task **não** está concluída. Não há mais bloqueio de decisão da consultora: a divergência de plataforma foi resolvida pela emenda e o CA-1-01d foi provado. O único bloqueio técnico restante é a **segregação por papel (CA-1-01e)**, isolada em TASK-1-001a para poder ser fechada sem arrastar a fila inteira.

## TASK-1-001a — detalhe

**Objetivo:** aplicar segregação de acesso por papel na coleção `fila_leads` e provar com duas contas.

**Caminho técnico (não depende de painel administrativo):** as regras estão em migração versionada (`pocketbase/migrations/0004_create_fila_leads.js`) — hoje todas as cinco operações usam `@request.auth.id != ''`. Uma migração nova (`0006_*`) substitui as regras: `create` exige `created_by` igual ao usuário autenticado; `update`/`delete` exigem ser o autor ou ter papel de consultora; `list`/`view` seguem abertas a autenticados (a fila é compartilhada por desenho). Detalhe na seção 6 da Emenda 01/2026.

**Pendência administrativa que acompanha:** a conta de teste `probe.qa.1793223729@example.com` não é removível pela API pública (403) — só superusuário remove. A prova de papel deve usar conta descartável.

**Pré-condição:** acesso ao Skip Cloud para aplicar a migração.

## Entregas de infraestrutura

- **Backup/restauração da fila** — `scripts/jornada-backup/` com export CSV+JSON, verificação de integridade, restauração por filtro com proteção contra duplicata e prova automatizada. Automação diária às 22h (job `cc627d297a64934c`). Documentado em `05_entregas/TASK-1-001/backup-restauracao.md`.

## Próxima ação

1. Alexandre aplica a migração de segregação por papel e executa a prova com duas contas (CA-1-01e) — fecha TASK-1-001a.
2. Em paralelo, SDR começa a operação real para acumular a semana de auditoria (CA-1-01 e 01a).
3. Consultora inicia TASK-1-002 (e-mail institucional) e TASK-1-006 (governança), que não dependem da fila fechar.
