# Fase 4 — SDR de IA (modo assistido)

**Status:** check-escopo APROVADO · **Pré-condições:** WhatsApp oficial + LGPD (gate D7-4, com prazo/custo da Meta estimados na F1); causa-raiz do agente anterior documentada via post-mortem conduzido pela consultora com acesso/histórico fornecido pelo cliente (gate D7-5); critério de pausa/rollback quantificado definido (ver RF-10)

## Resultado
IA aborda o lead no WhatsApp imediatamente após o formulário, qualifica e agenda — com transbordo humano obrigatório nas travas. Speed-to-lead cai para minutos.

## Entregas
1. **Agente WhatsApp (RF-10):** saudação em nome da Risomed, validação de vidas, identificação de desafios (benefícios/NR-01), oferta de horários.
2. **Transbordo humano:** obrigatório em menção a preço/desconto, questão regulatória, insatisfação, recusa, ou 2 falhas de interpretação seguidas; notificação ao responsável.
3. **Limites (RN-08):** IA nunca negocia preço, nunca concede desconto, não assina termos; log completo das conversas.
4. **Modo sombra:** operação em paralelo (IA sugere, humano envia) com critério de saída DUPLO: mínimo 2 semanas **E** mínimo de conversas por gatilho de transbordo definido pela consultora antes do início (com o volume atual baixo, duração sozinha não garante amostra). Relatório de divergências ao final. Nota: no modo sombra a latência medida é a do humano — o dado de latência da IA só vale após o go-live.

## Limites
- Sem negociação autônoma; sem acesso a dados além de WhatsApp + Agendor.
- Causa-raiz da tentativa anterior documentada como insumo (o que deu errado, por quê, como este design evita).

## Sequência ASA
Automático: primeira abordagem, validação de vidas, oferta de horários. Semiautomático: sugestão de resposta no modo sombra. Humano: transbordo, negociação, fechamento.

## Checklist
- [ ] WhatsApp oficial aprovado (gate)
- [ ] LGPD/base legal documentada (gate)
- [ ] Causa-raiz do agente anterior documentada (gate)
- [ ] Gatilhos de transbordo implementados
- [ ] Log de conversas operando
- [ ] Modo sombra executado com critério duplo (2 semanas E amostra mínima por gatilho)

## Critérios de aceite
- **CA-4-01:** 100% dos gatilhos de transbordo testados com prova (cada gatilho, 1 caso), incluindo exceção de canal (número sem WhatsApp/fixo → transbordo imediato).
- **CA-4-02:** prova negativa: IA sem acesso a preço/desconto.
- **CA-4-03:** log completo das conversas disponível e retido conforme política.
- **CA-4-04:** modo sombra concluído com critério duplo (duração + amostra mínima por gatilho) e relatório de divergências.
- **CA-4-05:** K1 ≤ 30min medido com IA no ar (média semanal, da origem do lead).
- **CA-4-06:** critério de pausa/rollback documentado e testado (simulação de degradação → volta para modo assistido total).
