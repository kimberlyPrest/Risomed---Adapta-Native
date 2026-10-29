# STATUS — Risomed · Adapta Native

**Cliente:** Risomed (Plataforma Multibenefícios em Saúde Corporativa)
**Consultora:** Kim (Adapta Native)
**Fase atual:** 1 — Fundação manual
**Atualizado em:** 2026-10-29

## Estado por etapa

| Etapa | Estado |
|---|---|
| Escopo definitivo | ✅ Aprovado (check-escopo 10/09) |
| SPECs Fase 1 | ✅ Geradas, revisadas e **emendadas (Emenda 01/2026, 29/10)** |
| Check-cliente/CSM | ⏳ Pendente |
| Tasks Fase 1 | 🔶 TASK-1-001 com 3 de 6 critérios fechados — bloqueio restante: segregação de acesso |

## Tasks da Fase 1

| Task | SPEC | Estado | Observação |
|---|---|---|---|
| TASK-1-001 — Fila manual de leads | SPEC-1-001 | 🔶 **em execução** | Divergência de plataforma resolvida (Emenda 01/2026). CA-1-01b, 01c e 01d fechados. Faltam CA-1-01/01a (dependem de 1 semana de operação) e CA-1-01e |
| TASK-1-001a — Segregação de acesso por papel | SPEC-1-001 | ⏳ não iniciada | **Único bloqueio técnico.** Isolada para não travar a fila inteira |
| TASK-1-002 a 006 | SPEC-1-002..006 | ⏳ não iniciadas | Não dependem do fechamento da 1-001 para começar |

## Progresso da TASK-1-001

| Critério | Estado |
|---|---|
| CA-1-01b — tag ICP e estágio | ✅ PASSOU |
| CA-1-01c — acesso não autorizado | ✅ PASSOU |
| CA-1-01d — recuperação da fonte única de verdade | ✅ **PASSOU em 28/10** (export + restauração campo a campo + backup diário) |
| CA-1-01e — segregação por papel (novo) | ⏳ TASK-1-001a |
| CA-1-01 / 01a — operação real | ⏳ exige 1 semana de uso do SDR |

## Decisão tomada pelo champion

**Manter o Skip e fazer o sistema funcionar** (28/10). Não se volta para Google Sheets. **Formalizada pela Emenda 01/2026 (29/10)**, que reescreveu os critérios que citavam recursos do Sheets.

## Bloqueios abertos

1. **Segregação de acesso na fila (único bloqueio técnico)** — qualquer conta criada com a chave de convite lê, altera e apaga todos os leads; não há papel só-leitura. A correção está em migração versionada (`pocketbase/migrations/0004_create_fila_leads.js`), não no painel — exige uma migração `0006_*` com as novas regras. Ver seção 6 da Emenda 01/2026.
2. **Conta de teste ativa** — `probe.qa.1793223729@example.com` não pode ser removida sem superusuário (403).
3. **Check-cliente/CSM** — nunca executado.

## Entregas de infraestrutura

- **Backup/restauração da fila** — `scripts/jornada-backup/` com export CSV+JSON, verificação de integridade, restauração por filtro com proteção contra duplicata e prova automatizada. Automação diária às 22h (job `cc627d297a64934c`). Documentado em `05_entregas/TASK-1-001/backup-restauracao.md`.

## Próxima ação

Obter acesso ao Skip Cloud para aplicar a migração de segregação (CA-1-01e); em paralelo, iniciar a operação real do SDR (acumula CA-1-01/01a) e as entregas 1-002 e 1-006, que não dependem disso.
