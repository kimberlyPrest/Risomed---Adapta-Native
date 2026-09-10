# Fase 2 — Integração determinística

**Status:** check-escopo APROVADO · **Pré-condição:** credenciais Agendor + permissões de webhook confirmadas (gate D7-1)

## Resultado
Lead do formulário atual aparece no Agendor em segundos, no funil VEN correto, com tags ICP e tarefa de primeiro contato — sem digitação, sem dupla checagem de e-mail.

## Entregas
1. **Ingestão automática (RF-06):** formulário → Empresa + Contato + Negócio no Agendor; anti-duplicidade por CNPJ/e-mail (duplicado vira nota + notificação, RN-06).
2. **Roteamento e tags (RF-07):** funil VEN exclusivo (RN-01); tags de porte (<10 / 10–100 / >100 vidas) e praça; `ICP Principal` conforme RN-04; leads fora do ICP com tag `Fora ICP` e prioridade baixa (RN-07 provisória até D7-3).
3. **Tarefa SLA (RF-08):** tarefa de primeiro contato com prazo de 30 min em horário útil (2h fora de ICP), atribuída ao responsável.
4. **Fila de exceção (RNF-02):** lead que falha na ingestão fica em fila visível, nunca perdido.

## Limites
- Sem IA; sem WhatsApp automático; sem alteração de campanhas.
- Formulário atual permanece; nenhuma mudança de site.

## Sequência ASA
Automático: ingestão, roteamento, tags, tarefa. Semiautomático: tratamento de exceção. Humano: primeiro contato e qualificação.

## Checklist
- [ ] Credenciais e permissões confirmadas (gate)
- [ ] Webhook de ingestão implementado e testado
- [ ] Anti-duplicidade com prova (CNPJ e e-mail)
- [ ] Tags automáticas conforme RN-04/RN-07
- [ ] Tarefa SLA com prazo correto
- [ ] Fila de exceção operando

## Critérios de aceite
- **CA-2-00:** primeiro ato da F2 — smoke test de ESCRITA da API do Agendor executado com a prova negativa de produção (busca por cliente real retorna vazio no token de teste) antes de qualquer escrita em produção; se o token apontar para produção, escrita bloqueada e escalada ao cliente.
- **CA-2-01:** 0 leads de formulário fora do VEN em 2 semanas de operação.
- **CA-2-02:** 0 cards duplicados; duplicidade tratada por nota + notificação.
- **CA-2-03:** tarefa de primeiro contato criada com prazo correto (30min ICP / 2h fora do ICP); tarefa vencida gera notificação ao CEO no mesmo dia e registro de violação.
- **CA-2-04:** leads com falha de ingestão aparecem na fila de exceção (prova com erro simulado); lead incompleto (sem campos de porte/praça) vai para a fila de exceção, nunca recebe tag calculada.
- **CA-2-05:** K1 (speed-to-lead da origem) medido automaticamente a partir da entrada em produção.
