# STATUS — Risomed · Adapta Native

**Cliente:** Risomed (Plataforma Multibenefícios em Saúde Corporativa)
**Consultora:** Kim (Adapta Native)
**Fase atual:** 1 — Fundação manual
**Atualizado em:** 2026-10-28

## Estado por etapa

| Etapa | Estado |
|---|---|
| Escopo definitivo | ✅ Aprovado (check-escopo 10/09) |
| SPECs Fase 1 | ✅ Geradas e revisadas (painel 4 lentes) |
| Check-cliente/CSM | ⏳ Pendente |
| Tasks Fase 1 | 🔶 TASK-1-001 com 4 de 5 critérios fechados — bloqueio restante: segregação de acesso |

## Tasks da Fase 1

| Task | SPEC | Estado | Observação |
|---|---|---|---|
| TASK-1-001 — Fila manual de leads | SPEC-1-001 | 🔶 **bloqueada** | Reteste humano aprovado 22/10. CA-1-01b e CA-1-01d fechados. Falta a segregação de acesso e a emenda da SPEC |
| TASK-1-002 a 006 | SPEC-1-002..006 | ⏳ não iniciadas | Aguardam o fechamento da 1-001 |

## Progresso da TASK-1-001

| Critério | Estado |
|---|---|
| CA-1-01b — tag ICP e estágio | ✅ PASSOU |
| CA-1-01c — acesso não autorizado | ✅ PASSOU |
| CA-1-01d — restauração | ✅ **PASSOU em 28/10** (script + prova campo a campo) |
| CA-1-01 / 01a — operação real | ⏳ exige 1 semana de uso do SDR |

## Decisão tomada pelo champion

**Manter o Skip e fazer o sistema funcionar** (28/10). Não se volta para Google Sheets. Consequência: emenda da SPEC-1-001 necessária; proposta pronta em `05_entregas/TASK-1-001/emenda-spec-1-001-proposta.md`.

## Bloqueios abertos

1. **Segregação de acesso na fila (único bloqueio técnico)** — qualquer conta criada com a chave de convite lê, altera e apaga todos os leads; não há papel só-leitura. Exige alteração das regras da coleção no Skip Cloud; a API de usuário responde 403 e a criação de superusuário é bloqueada. **Falta acesso administrativo ao Skip Cloud.**
2. **Emenda da SPEC-1-001** — decisão da consultora Kim, não do agente.
3. **Conta de teste ativa** — `probe.qa.1793223729@example.com` não pode ser removida sem superusuário (403).

## Entregas de infraestrutura

- **Backup/restauração da fila** — `scripts/jornada-backup/` com export CSV+JSON, verificação de integridade, restauração por filtro com proteção contra duplicata e prova automatizada. Automação diária às 22h (job `cc627d297a64934c`). Documentado em `05_entregas/TASK-1-001/backup-restauracao.md`.

## Próxima ação

Obter acesso ao Skip Cloud para aplicar a segregação de acesso na coleção `fila_leads`; em paralelo, submeter a emenda da SPEC-1-001 à consultora.
