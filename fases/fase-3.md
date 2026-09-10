# Fase 3 — Reativação de base

**Status:** check-escopo APROVADO · **Pré-condição:** F2 concluída OU autorização da consultora para rodar em paralelo (a reativação trabalha a base EXISTENTE do Agendor, não o fluxo de formulário — a dependência técnica da F2 é mínima; a ordem D2 é preferência de sequência, não bloqueio técnico). Gate adicional: base legal/opt-out da reativação decidido na F1 (ver RF-05).

## Resultado
Base de clientes perdidos/dormintes organizada em fila de reativação com próxima ação e data, gerando oportunidades sem depender de novo lead.

## Entregas
1. **Segmentação da base (RF-09):** perdido / dorminte / ativo, com critério explícito e documentado. **Etapa de saneamento prévia:** amostragem da base histórica antes de congelar os critérios (a base tem histórico de funil errado, registros manuais e duplicidades — os critérios só são congelados após validar que são executáveis sobre os dados reais).
2. **Fila de reativação (RF-09):** ordem por potencial; próxima ação e data em cada registro; resultado de cada tentativa registrado.
3. **Critério de saída:** reativado / perdido definitivo / sem resposta após N tentativas (N definido na fase).
4. **Conformidade (RN-09):** base legal e opt-out registrados antes do primeiro disparo.

## Limites
- Sem IA; sem automação de mensagens (disparo manual assistido pela fila).
- Não altera cadastro existente além do registro de reativação.

## Sequência ASA
Automático: nada novo. Semiautomático: ordenação da fila. Humano: contato e registro do resultado.

## Checklist
- [ ] Critérios de segmentação documentados APÓS saneamento/amostragem da base
- [ ] Base segmentada e revisada
- [ ] Fila ordenada com próxima ação/data
- [ ] Opt-out e base legal registrados
- [ ] Primeira leva definida (50 contatos)

## Critérios de aceite
- **CA-3-01:** base segmentada com critério explícito por categoria.
- **CA-3-02:** toda tentativa com resultado e próxima ação registrados.
- **CA-3-03:** critério de saída aplicado a 100% dos registros trabalhados.
- **CA-3-04:** opt-out registrado e respeitado (prova com 1 caso).
- **CA-3-05:** primeira leva de 50 contatos concluída com resultado.
