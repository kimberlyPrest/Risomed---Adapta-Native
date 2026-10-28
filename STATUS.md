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
| Tasks Fase 1 | 🔶 TASK-1-001 implementada e aprovada no reteste humano — **fechamento bloqueado** |

## Tasks da Fase 1

| Task | SPEC | Estado | Observação |
|---|---|---|---|
| TASK-1-001 — Fila manual de leads | SPEC-1-001 | 🔶 **bloqueada** | Reteste humano aprovado em 22/10. Bloqueio por divergência de plataforma (SPEC pede Google Sheets; entregue aplicação Skip) e por CA-1-01d sem recurso de restauração na plataforma |
| TASK-1-002 a 006 | SPEC-1-002..006 | ⏳ não iniciadas | Aguardam o fechamento da 1-001 |

## Progresso

- **Tasks concluídas:** 0 de 6
- **TASK-1-001:** implementação completa; critérios CA-1-01b ✅ e CA-1-01c ✅ (com risco de segregação registrado); CA-1-01 e CA-1-01a dependem de 1 semana de operação real; CA-1-01d ❌
- **Percentual da Fase 1:** 0% (a fase só fecha após validação da consultora)

## Bloqueios abertos

1. **Divergência SPEC-1-001 × implementação** — a SPEC declara "planilha/kanban estruturado (Google Sheets)"; a implementação entregue é uma aplicação web no Skip Cloud. Os critérios 01c e 01d citam recursos que só existem no Sheets. Exige **emenda aprovada pela consultora** — proposta pronta em `05_entregas/TASK-1-001/emenda-spec-1-001-proposta.md`.
2. **CA-1-01d sem solução na plataforma** — o cliente não tem acesso a backup nem a restauração ponto-no-tempo (`GET /api/backups` → 403). Precisa de decisão: export periódico + reimportação comprovada, ou habilitar backup no provedor.
3. **Segregação de acesso na fila (risco, não bloqueio do CA)** — qualquer conta criada com a chave de convite lista, altera e apaga todos os leads; não há papel só-leitura. A chave de convite é o único guarda da fronteira de PII e deve ser rotacionada.
4. **Conta de teste ativa** — `probe.qa.1793223729@example.com`, criada para a prova negativa, não pode ser removida sem superusuário (403).

## Próxima ação

Decisão do Alexandre sobre a plataforma (manter Skip com emenda × voltar para Sheets). Aprovada a emenda, restam a correção de segregação, a remoção da conta de teste e a reexecução de CA-1-01c/01d.
