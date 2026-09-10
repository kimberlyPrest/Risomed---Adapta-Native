# PRD — Risomed Planos Odontológicos

**Produto:** Central de Captação e Reativação B2B com SDR de IA
**Cliente:** Risomed Planos Odontológicos Ltda (transição de marca ARM Odonto → Risomed Multibenefícios)
**Consultora técnica:** Kim (Adapta Native) · **Data:** 10/09/2026
**Fontes:** call de consultoria 26/08/2026 (tl;dv 6a8f378df221220013ba1757), kick-off 18/08/2026 (tl;dv 6a84656f86d9f9001328382f), escopo base `01-Escopo.md` (26/08), análise crítica preliminar (26/08), decisões da consultora de 10/09 (`decisoes-consultora.md`).

## 1. Problema

A Risomed (31 anos, benefícios corporativos B2B para 10–100 colaboradores) nunca teve processo comercial estruturado. Leads chegam por formulário/e-mail/CRM em canais desconectados, com 1–2 dias de atraso; parte cai no funil errado (ARM em vez de VEN); triagem e duplicidade são manuais; não há baseline nem indicadores. Resultado: 1–2 vendas/mês no ICP contra meta de 4. A agência de marketing tem baixa performance e não há instrumento de cobrança baseado em dados.

## 2. Objetivo mensurável

Aumentar a conversão comercial da Risomed para **4 vendas/mês dentro do ICP** (baseline: 1–2/mês), garantindo:
- **K1 — Speed-to-lead:** ≤ 30 min em horário útil do primeiro contato com todo lead B2B de formulário dentro do ICP (2h para leads fora do ICP; leads por outros canais entram na fila com prioridade padrão). Baseline atual: 1–2 dias. **Definição operacional:** timestamp de ORIGEM do lead (submissão do formulário / recebimento do e-mail) → primeiro registro de contato — nunca a data de digitação na fila, que mascararia o atraso atual.
- **K2 — Integridade de funil:** 100% dos leads de formulário no funil VEN, etapa correta, sem intervenção manual (baseline: leads desviados para ARM e retrabalho manual).
- **K3 — Vendas no ICP:** 4 vendas/mês (baseline: 1–2).

Baselines serão congelados manualmente na Fase 1; sem baseline congelado, as metas K1–K3 permanecem não verificáveis.

## 3. Solução (visão)

Uma esteira comercial em 5 fases que começa 100% manual (F1), automatiza a entrada no CRM (F2), reativa a base existente (F3), adiciona SDR de IA no WhatsApp com transbordo humano (F4) e fecha o loop de marketing com relatório de campanhas (F5). Decisão comercial sempre humana; IA assiste, nunca negocia.

## 4. Escopo por fase (resumo)

| Fase | Nome | Entrega central | Dependência externa |
|---|---|---|---|
| F1 | Fundação manual | Fila manual estruturada, e-mail institucional (manual), roteiro SPIN, baseline congelado, preparação de integração | Nenhuma |
| F2 | Integração determinística | Formulário atual → Agendor: anti-duplicidade, roteamento VEN, tags ICP, tarefa SLA 30min | Credenciais Agendor |
| F3 | Reativação de base | Fila de perdidos/dormintes com próxima ação e data | Dados do Agendor |
| F4 | SDR de IA (assistido) | Agente WhatsApp com transbordo humano; causa-raiz do agente anterior documentada | WhatsApp oficial + LGPD |
| F5 | Loop Meta/Ads | Relatório semanal automático das campanhas | Token Meta/Google Ads |

## 5. Fora de escopo

- Landing page nova (evolução opcional pós-F2, condicionada ao baseline da F1).
- Substituir o Agendor no MVP (reavaliação só após F4, com dado real).
- Enriquecimento com notícias/faturamento (Evolução IA 01 do escopo base).
- Automação de contratos, decisões jurídicas, beneficiários em 5 plataformas.
- Automações complexas de marketing; geração de conteúdo com avatar de vídeo.
- IA autônoma sem transbordo humano.

## 6. Riscos e contornos

| Risco | Contorno |
|---|---|
| Credenciais Agendor atrasarem | F1 não depende delas; F2 só inicia com credenciais em mãos |
| Formulário atual "não converte" | Baseline da F1 mede o gargalo; LP nova é evolução condicionada a dado |
| Tentativa anterior de agente falhou (devolvia leads errados) | Causa-raiz documentada como pré-condição da F4; F4 em modo assistido |
| Sem baseline → metas inverificáveis | F1 congela baseline manualmente antes de qualquer automação |
| LGPD/WhatsApp não oficial | Gate documentado na F1; F4 só com WhatsApp oficial |
| Alexandre viaja 11–25/09 | F1 executável pela consultora sem dependência do cliente |

## 7. Critérios de sucesso (verificação)

- K1 medido na fila (F1 manual → F2 automático): timestamp de ORIGEM do lead (submissão do formulário/recebimento do e-mail) → primeiro registro de contato. A data de digitação na fila NÃO é usada como origem — ela mascararia o atraso atual de 1–2 dias.
- K2 auditado no Agendor: 0 leads de formulário fora do VEN após F2.
- K3 medido mensalmente contra baseline congelado na F1.
