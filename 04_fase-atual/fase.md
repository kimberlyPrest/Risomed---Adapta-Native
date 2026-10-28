# Fase 1 — Fundação manual (sem integração, sem LP)

**Status:** em execução · **Dependências externas:** nenhuma credencial/token · **Construção:** consultora (Kim) · **Operação:** SDR/comercial do cliente

> Registro de execução da fase atual. O escopo canônico permanece em `fases/fase-1.md`; aqui ficam as tasks, seus donos e o estado real.

## Resultado da fase

A operação comercial da Risomed rodando em uma fila estruturada, com régua de baseline congelada e toda a preparação documentada para a integração da Fase 2 — sem depender de credenciais, token ou qualquer acesso técnico do cliente.

## Tasks da fase

| ID | Task | Dono | SPEC | Critério | Estado | Data |
|---|---|---|---|---|---|---|
| TASK-1-001 | Fila manual estruturada de leads | Alexandre (champion) | SPEC-1-001 | CA-1-01, 01a, 01b, 01c, 01d | 🔶 bloqueada | 2026-10-28 |
| — | E-mail institucional | — | SPEC-1-002 | CA-1-02, 01-02a | ⏳ não iniciada | — |
| — | Roteiro SPIN + checklist | — | SPEC-1-003 | CA-1-03a, 01-03b | ⏳ não iniciada | — |
| — | Baseline congelado | — | SPEC-1-004 | CA-1-03, 01-03c | ⏳ não iniciada | — |
| — | Preparação de integração | — | SPEC-1-005 | CA-1-04, 01-05, 01-05a | ⏳ não iniciada | — |
| — | Governança da F1 | — | SPEC-1-006 | CA-1-06, 01-06a | ⏳ não iniciada | — |

## TASK-1-001 — detalhe

**Implementação entregue:** aplicação web no Skip Cloud (projeto "Jornada Comercial Risomed", id 57599), coleção `fila_leads` + tela Fila Manual.
**Preview:** https://jornada-comercial-risomed-0b95a--preview.goskip.app

**Verificação de 2026-10-28:**

| Critério | Descrição | Resultado |
|---|---|---|
| CA-1-01 | 100% dos leads da semana na fila com estágio, tag ICP e próxima ação com data | ⏳ estrutura e obrigatoriedades presentes e aplicadas pelo servidor; auditoria de 1 semana de operação real não executada |
| CA-1-01a | "data de origem" = data de submissão, nunca de digitação | ⏳ campo presente e obrigatório; comparação com 3 e-mails originais não executada |
| CA-1-01b | exatamente uma tag ICP válida, impedida por lista | ✅ PASSOU — tag e estágio inválidos rejeitados (HTTP 400) |
| CA-1-01c | prova negativa de acesso por conta não autorizada | ✅ PASSOU — sem autenticação a fila devolve 0 registros e não aceita escrita; sem chave de convite o cadastro é recusado; `created_by` não pode ser forjado |
| CA-1-01d | prova de restauração da fonte única de verdade | ❌ NÃO SATISFATÓRIO — export CSV existe; não há backup nem restauração ponto-no-tempo acessível (403) |

**Bloqueios:**
1. Divergência de plataforma entre SPEC-1-001 (Google Sheets) e a implementação (Skip) — exige emenda aprovada pela consultora.
2. CA-1-01d não é fechável na plataforma atual.

**Risco de segurança registrado (não bloqueia CA-1-01c):** não há segregação por usuário ou papel dentro da fila — qualquer conta com a chave de convite apaga leads de outra pessoa.

**Estado:** a task **não** está concluída. O reteste humano de 22/10 aprovou o fluxo funcional; a verificação de fechamento de 28/10 encontrou o bloqueio de escopo e a lacuna de recuperação.
