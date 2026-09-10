# Fase 1 — Fundação manual (sem integração, sem LP)

**Status:** check-escopo APROVADO · **Dependências externas:** nenhuma credencial/token · **Construção:** consultora (Kim) · **Operação:** SDR/comercial do cliente (adoção é pré-condição de valor — dono operacional definido no CA-1-06)

## Resultado
A operação comercial da Risomed rodando em uma fila estruturada (kanban/planilha), com régua de baseline congelada e toda a preparação documentada para a integração da Fase 2 — sem depender de credenciais, token ou qualquer acesso técnico do cliente. A F1 exige participação operacional do SDR (adoção da fila) e acesso aos dados históricos de venda do cliente para o baseline; o que ela NÃO exige é credencial, token ou mudança de sistema.

## Entregas
1. **Fila manual estruturada (RF-01):** kanban/planilha com estágios Prospecção → Contato → Apresentação → Proposta → Fechamento → Perdido; colunas de tag ICP (10–100 vidas, praça), próxima ação e data.
2. **E-mail institucional (RF-02):** template com a proposta de valor Risomed; disparo manual; registro do envio na ficha do lead.
3. **Roteiro SPIN + checklist (RF-03):** documento de abordagem e qualificação (vidas, praça, decisor, urgência).
4. **Baseline congelado (RF-04):** volume de leads/semana, speed-to-lead atual, conversão por etapa, vendas/mês no ICP — medidos manualmente e registrados em documento de referência.
5. **Preparação de integração (RF-05):** mapeamento de campos formulário atual → Agendor; verificação da capacidade do formulário (POST/webhook vs. e-mail; captura de origem/UTM); smoke test da API do Agendor (tarefa em minutos, tag, busca por CNPJ/e-mail); contrato de webhook desenhado; checklist de credenciais/permissões do plano; decisão WhatsApp oficial + LGPD documentada (insumo do gate D7-4), com estimativa de prazo/custo da aprovação do número na Meta; decisão de base legal/opt-out da reativação (insumo da F3).

## Limites
- Nenhuma chamada de API, webhook ativo ou automação de disparo.
- Usa o formulário atual como está; não cria landing page.
- Não altera configuração do Agendor.

## Sequência ASA
Automático: nada (F1 é manual). Semiautomático: template de e-mail. Humano: toda a operação da fila.

## Checklist
- [ ] Fila criada com estágios, tags ICP e próxima ação
- [ ] Template de e-mail institucional aprovado
- [ ] Roteiro SPIN + checklist de qualificação prontos
- [ ] Baseline congelado (4 métricas, janela mínima 4 semanas/20 leads) e assinado
- [ ] Mapeamento de campos formulário→Agendor revisado + capacidade do formulário verificada (POST vs. e-mail; origem)
- [ ] Smoke test da API do Agendor executado (tarefa em minutos, tag, busca CNPJ/e-mail)
- [ ] Contrato de webhook desenhado
- [ ] Checklist de credenciais/permissões Agendor enviado ao cliente
- [ ] Decisão WhatsApp oficial + LGPD documentada (com prazo/custo da Meta) + base legal da reativação (F3)
- [ ] Regra de fonte única de verdade na F1 definida (fila substitui vs. espelha o Agendor)
- [ ] Rotina de captação manual definida + dono operacional da fila no cliente

## Critérios de aceite
- **CA-1-01:** 100% dos leads da semana registrados na fila com estágio, tag ICP e próxima ação com data.
- **CA-1-02:** template de e-mail aplicado a todo lead novo, com registro na ficha.
- **CA-1-03:** baseline congelado com as 4 métricas (volume/semana, speed-to-lead da ORIGEM do lead, conversão, vendas/mês ICP), com janela mínima de 4 semanas ou 20 leads (o que ocorrer por último) — amostra menor só com decisão registrada da consultora.
- **CA-1-04:** mapeamento de campos formulário→Agendor completo e revisado (revisão: cliente valida os campos do formulário; consultora valida os campos do Agendor — prova: validação registrada no dossiê), incluindo verificação da capacidade do formulário (POST/webhook vs. e-mail; captura de origem) e smoke test da API do Agendor (provas de leitura: busca por CNPJ/e-mail + prova negativa de produção; provas de escrita — tarefa em minutos, tag — se o token de escrita já estiver disponível, senão viram pré-condição de go-live da F2, CA-2-00).
- **CA-1-05:** contrato de webhook desenhado (campos, gatilho, tratamento de erro) sem implementação; decisão de ponte de e-mail vs. ajuste de formulário registrada se o formulário não emitir POST.
- **CA-1-06:** gates D7-1..D7-5 listados com responsável e prazo; regra de fonte única de verdade na F1 definida (fila substitui vs. espelha o Agendor); rotina de captação manual definida (quem monitora formulário/e-mail e com que frequência); dono operacional da fila no cliente definido com o Alexandre.

## Fora desta fase
- Integração formulário → Agendor (Fase 2 — exige credenciais, gate D7-1).
- Reativação de base (Fase 3).
- SDR de IA no WhatsApp (Fase 4 — exige WhatsApp oficial e post-mortem, gates D7-4/D7-5).
- Relatório Meta/Ads (Fase 5 — exige token, gate D7-2).
- Landing page nova (evolução opcional pós-F2, condicionada ao baseline — decisão D3).
- Qualquer automação de disparo de e-mail (na F1 o envio é manual com template).
