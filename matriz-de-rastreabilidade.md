# Matriz de Rastreabilidade — Risomed

| # | Fonte | Achado / Decisão | Tratamento | Requisito / KPI | Fase |
|---|---|---|---|---|---|
| 1 | Call 26/08 (tl;dv 6a8f378df) | Cliente aprova SDR de IA + reativação + dashboard de campanhas + olhar o site | Decisão do cliente | RF-10, RF-09, RF-11 | F4, F3, F5 |
| 2 | Kim 10/09 (D2) | F1 sem integrações e sem LP; ordem F1 manual → F2 integração → F3 reativação → F4 IA → F5 Ads | Decisão da consultora | RF-01..RF-05 | F1 |
| 3 | Kim 10/09 (D3) | Landing page nova removida; evolução opcional pós-F2 condicionada ao baseline | Fora de escopo | — | — |
| 4 | Kim 10/09 (D4) | Manter Agendor no MVP; reavaliar troca pós-F4 | Decisão da consultora | RF-06..RF-08 | F2 |
| 5 | Kim 10/09 (D5) | IA assistida com transbordo; causa-raiz do agente anterior como pré-condição | Decisão da consultora | RF-10, RN-08 | F4 |
| 6 | Call 26/08 (D6) | Meta 4 vendas/mês no ICP (hoje 1–2); leads com atraso 1–2 dias | Meta do cliente | K1, K3, RN-04, RN-05 | F1–F5 |
| 7 | Escopo base RN01 (vídeo ts 07:15) | Funil VEN exclusivo; leads caindo no ARM | Requisito | RN-01, RF-07 | F2 |
| 8 | Escopo base RN02 (vídeo ts 00:53) | Campos obrigatórios de entrada | Requisito | RN-02, RF-06 | F2 |
| 9 | Escopo base RN03 (vídeo ts 09:05) | Disparo institucional de apresentação | Requisito (disparo manual na F1) | RN-03, RF-02 | F1 |
| 10 | Escopo base RN06 | Trava de duplicidade por CNPJ/e-mail | Requisito | RN-06, RF-06 | F2 |
| 11 | Escopo base RN04/RN05 (propostas) | ICP 10–100 vidas + SLA 30min | Requisito (baseline na F1) | RN-04, RN-05, RF-07, RF-08 | F1, F2 |
| 12 | Análise crítica — baseline ausente | Metas inverificáveis sem baseline | Contorno | RF-04 | F1 |
| 13 | Análise crítica — Agendor/webhooks não confirmados | Capacidade técnica não validada | Contorno + gate | RF-05, D7-1 | F1, F2 |
| 14 | Análise crítica — recorte misto (jurídico/implantação) | Escopo base misturava captação e pós-venda | Fora de escopo | — | — |
| 15 | Análise crítica — segurança/LGPD não especificadas | PII e WhatsApp sem política | Requisito + gate | RN-09, RNF-03, D7-4 | F1, F3, F4 |
| 16 | Análise crítica — Risomed.pdf de outro projeto (ABC Log) | Briefing oficial ausente | Risco registrado; fonte = call + DMO + vídeo | — | — |
| 17 | Análise crítica — ICP não homologado | 10–100 vidas sem validação formal | Gate | D7-3, RN-07 | F2 |
| 18 | Call 26/08 — tentativa anterior de agente falhou | Devolvia leads errados | Pré-condição da F4 | D7-5, RF-10 | F4 |
| 19 | Call 26/08 — formulário "não converte" | LP nova desejada pelo cliente | Evolução condicionada ao baseline (D3) | — | pós-F2 |
| 20 | Call 26/08 — "briga" com a agência de marketing | Falta instrumento de cobrança | Requisito | RF-11 | F5 |
| 21 | Call 26/08 — Alexandre viaja 11–25/09 | Disponibilidade reduzida | Contorno: F1 sem dependência de credencial/token (decisão D2); operação da fila é do cliente | RF-01, D2 | F1 |
| 22 | Escopo base — Evolução IA 01 (enriquecimento) | Sumário executivo por CNPJ | Fora de escopo | — | — |
| 23 | Escopo base — Proposta 3 (handoff implantação) | Formulário único de vidas em 5 plataformas | Fora de escopo | — | — |
| 24 | Escopo base — Proposta 1 (domínio/301) | Redirecionamento armodonto → risomed | Fora de escopo (ligado à LP, D3) | — | — |
| 25 | Painel de revisão 10/09 — coerência/viabilidade/guardião/adversarial | K1 viciado pela digitação; formulário Locaweb sem webhook confirmado; K3 sem alavanca de volume; SLA sem escalação; modo sombra sem amostra; D7-5 com dono errado; F3 refém da F2; cronograma ausente | Correções safe_auto aplicadas; demais viraram gates D7-8/D7-9 e emendas nos RFs/CA | RF-04, RF-05, RF-10, RN-05, RN-07, seção 5.1 | F1–F5 |
