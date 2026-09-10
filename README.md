# Risomed — Adapta Native

**Cliente:** Risomed Planos Odontológicos (transição de marca ARM Odonto → Risomed Multibenefícios)
**Produto:** Central de Captação e Reativação B2B com SDR de IA
**Consultora técnica:** Kim (Adapta Native) · **Data:** 10/09/2026

## Estado

| Etapa | Estado |
|---|---|
| Escopo definitivo | ✅ Aprovado (check-escopo 10/09) |
| SPECs Fase 1 | ✅ Geradas e revisadas (painel 4 lentes) |
| Check-cliente/CSM | ⏳ Pendente |
| Tasks Fase 1 | ⏳ Próximo passo (gerar-tasks) |

## Estrutura

```
02-Escopo-Definitivo.md      — escopo canônico (11 RFs, 9 RNs, 4 RNFs, 5 fases, gates D7)
PRD.md                       — problema, KPIs K1–K3, riscos
matriz-de-rastreabilidade.md — 25 linhas fonte → decisão → requisito → fase
check-escopo.md              — APROVADO (Kim, 10/09/2026)
fases/fase-1..5.md           — resultado, entregas, limites, ASA, checklist, CAs
04_fase-atual/               — Fase 1 aberta
  specs/                     — 6 SPECs + matriz-specs-fases
```

## Fases

1. **F1 — Fundação manual** (sem integração, sem LP): fila, e-mail institucional, roteiro SPIN, baseline congelado, preparação de integração
2. **F2 — Integração determinística**: formulário → Agendor (anti-duplicidade, roteamento VEN, tags, SLA 30min)
3. **F3 — Reativação de base**
4. **F4 — SDR de IA (modo assistido)**: WhatsApp com transbordo humano
5. **F5 — Loop Meta/Google Ads**: relatório semanal (fase cortável)

## KPIs

- **K1** Speed-to-lead ≤ 30 min (medido da ORIGEM do lead — submissão do formulário — nunca da digitação na fila)
- **K2** 100% dos leads de formulário no funil VEN sem digitação nem roteamento manual
- **K3** 4 vendas/mês no ICP (baseline: 1–2)

> **Nota:** K3 = conversão × volume. O sistema ataca conversão e velocidade; o volume de leads permanece com a agência de marketing (seção 5.1 do escopo).
