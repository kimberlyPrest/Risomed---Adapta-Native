# Matriz SPECs × Fases — Risomed Fase 1

| Fase | Requisito | SPEC | Critérios de aceite | Prova (TDD) | Status |
|---|---|---|---|---|---|
| 1 | RF-01 | SPEC-1-001 Fila manual estruturada | CA-1-01, CA-1-01a, CA-1-01b, CA-1-01c, CA-1-01d | RED/GREEN/REGRESSÃO (auditoria semanal + provas negativas de acesso e restauração) | planejada |
| 1 | RF-02 | SPEC-1-002 E-mail institucional | CA-1-02, CA-1-02a | RED/GREEN/REGRESSÃO (auditoria da fila + aprovação humana) | planejada |
| 1 | RF-03 | SPEC-1-003 Roteiro SPIN + checklist | CA-1-03a, CA-1-03b | RED/GREEN/REGRESSÃO (role-play + auditoria + validação humana) | planejada |
| 1 | RF-04 | SPEC-1-004 Baseline congelado | CA-1-03, CA-1-03c | RED/GREEN/REGRESSÃO (documento assinado + janela mínima) | planejada |
| 1 | RF-05 | SPEC-1-005 Preparação de integração | CA-1-04, CA-1-05, CA-1-05a | RED/GREEN/REGRESSÃO (smoke test + laudo + sanitização) | planejada |
| 1 | CA-1-06/RN-09 | SPEC-1-006 Governança da F1 | CA-1-06, CA-1-06a | RED/GREEN/REGRESSÃO (documento validado) | planejada |

Cobertura: CA-1-01(+a,b,c,d), CA-1-02(+a), CA-1-03(+a,b,c), CA-1-04, CA-1-05(+a), CA-1-06(+a) — todos os CAs da Fase 1 têm SPEC dona.

**Nota de numeração:** CA-1-03a/03b pertencem à SPEC-1-003 (roteiro SPIN); CA-1-03/03c pertencem à SPEC-1-004 (baseline). A família 03 atravessa duas SPECs — mantida por fidelidade à numeração da fase-1.md; a matriz acima é o mapa canônico de donos.

**Nota SPEC-1-005:** provas de ESCRITA da API (tarefa em minutos, tag) exigem token de escrita (gate D7-1, da F2). Se indisponível na F1, CA-1-04 é satisfeito com provas de leitura + prova negativa de produção + laudo do formulário; a prova de escrita vira CA-2-00 (primeiro ato da F2).
