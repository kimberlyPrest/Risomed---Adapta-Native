# Escopo Definitivo — Central de Captação e Reativação B2B com SDR de IA

**Cliente:** Risomed Planos Odontológicos · **Data:** 10/09/2026 · **Status:** check-escopo APROVADO (Kim, 10/09/2026) · check-cliente PENDENTE

## 1. Objetivo

Elevar a Risomed de 1–2 para **4 vendas/mês no ICP** (empresas de 10–100 colaboradores, Grande SP / Sul de Minas / Vale do Paraíba), eliminando a perda de leads por fragmentação de canais e atraso de resposta, com esteira em 5 fases que começa manual e evolui para automação e IA assistida.

**KPIs:**
- **K1** Speed-to-lead ≤ 30 min em horário útil, medido do timestamp de ORIGEM do lead (submissão do formulário/recebimento do e-mail) até o primeiro registro de contato — nunca da digitação na fila (baseline F1: 1–2 dias). Aplica-se a leads de formulário dentro do ICP; leads fora do ICP têm régua de 2h; leads por outros canais entram na fila com prioridade padrão.
- **K2** 100% dos leads de formulário no funil VEN sem digitação nem roteamento manual (tratamento de duplicidade e exceção pode exigir toque humano — o que é vedado é a digitação e o roteamento manual) (baseline: desvios para ARM + retrabalho).
- **K3** 4 vendas/mês no ICP (baseline: 1–2).

## 2. Requisitos funcionais

### RF-01 — Fila manual estruturada (F1)
Kanban/planilha com estágios do funil (Prospecção → Contato → Apresentação → Proposta → Fechamento → Perdido), tags ICP aplicadas manualmente (10–100 vidas, praça), registro padronizado do resultado de cada contato (data, canal, resumo, próxima ação com data).

### RF-02 — E-mail institucional de apresentação (F1)
Template pronto com a proposta de valor Risomed; disparo manual no início; registro do envio na ficha do lead.

### RF-03 — Roteiro SPIN + checklist de qualificação (F1)
Documento de abordagem (SPIN Selling) e checklist de qualificação (vidas, praça, decisor, urgência) para o SDR.

### RF-04 — Baseline congelado (F1)
Medição e registro do baseline: volume de leads/semana, speed-to-lead atual (da ORIGEM do lead ao primeiro contato), conversão por etapa, vendas/mês no ICP. Janela mínima de observação: 4 semanas ou 20 leads, o que ocorrer por último — congelar com amostra menor exige decisão da consultora registrada no documento. Documento assinado pela consultora com validação do cliente; é a régua de K1–K3. Método: prospectivo a partir da fila; dados históricos do Agendor usados apenas como referência complementar (timestamps não confiáveis).

### RF-05 — Preparação de integração (F1)
Mapeamento de campos formulário atual → Agendor; **verificação da capacidade técnica do formulário atual (Locaweb): emite POST/webhook ou só e-mail? captura parâmetro de origem (UTM/campanha)?** — se só e-mail, decisão humana (ponte de e-mail vs. ajuste de formulário) registrada antes de liberar a F2; contrato de webhook desenhado; **smoke test da API do Agendor** (criar tarefa com prazo em minutos, escrever tag, buscar por CNPJ/e-mail); checklist de credenciais/permissões do plano; decisão WhatsApp oficial + LGPD documentada (insumo do gate D7-4), incluindo estimativa de prazo/custo da aprovação do número na Meta.

### RF-06 — Ingestão automática formulário → Agendor (F2)
Lead do formulário cria/atualiza Empresa + Contato + Negócio no Agendor sem intervenção humana; anti-duplicidade por CNPJ/e-mail (duplicado vira nota no negócio existente + notificação).

### RF-07 — Roteamento e tags automáticos (F2)
Todo lead de formulário no funil VEN, etapa Prospecção; tags automáticas de porte (<10 / 10–100 / >100 vidas) e praça; tag `ICP Principal` para 10–100 vidas na praça.

### RF-08 — Tarefa de primeiro contato com SLA (F2)
Tarefa automática de primeiro contato com prazo de 30 min em horário útil (2h fora de prioridade ICP), atribuída ao responsável.

### RF-09 — Fila de reativação (F3)
Base de clientes perdidos/dormintes do Agendor organizada em fila com próxima ação e data; registro do resultado de cada tentativa; critério de saída (reativado / perdido definitivo / sem resposta após N tentativas).

### RF-10 — SDR de IA no WhatsApp, modo assistido (F4)
Agente aborda o lead via WhatsApp oficial imediatamente após o formulário; valida vidas, identifica desafios (benefícios/NR-01), oferece horários. Transbordo humano obrigatório em: menção a preço/desconto, questão regulatória, insatisfação, recusa, 2 falhas de interpretação seguidas, **ou número sem WhatsApp/fixo/inválido** (exceção de canal → transbordo imediato). IA nunca negocia preço, nunca concede desconto, não assina termos. Pré-condições: causa-raiz da tentativa anterior de agente documentada (post-mortem conduzido pela consultora com acesso/histórico fornecido pelo cliente) e critério de pausa/rollback quantificado definido (ex.: taxa de transbordo indevido ou reclamações acima do limite → volta para modo assistido total).

### RF-11 — Relatório de campanhas Meta/Google Ads (F5)
Relatório semanal automático (gasto por campanha, resultados, tendência) entregue ao cliente para cobrança da agência. Somente leitura — a agência continua operando as campanhas. **Nota de prioridade:** F5 é a fase cortável sem comprometer K1–K2; se o prazo apertar, é o sacrifício declarado. CPL por campanha depende de o formulário capturar origem (verificado no RF-05); sem origem, CPL apenas agregado.

## 3. Regras de negócio

- **RN-01** Todo lead de formulário corporativo tramita exclusivamente no funil VEN (fonte: vídeo de mapeamento, ts 07:15).
- **RN-02** Campos mínimos de entrada: Empresa, Solicitante, E-mail, Telefone, CNPJ, Nº de funcionários, Cidade (fonte: vídeo, ts 00:53).
- **RN-03** Todo novo lead recebe a apresentação institucional (fonte: vídeo, ts 09:05).
- **RN-04** ICP = 10–100 colaboradores em Grande SP / Sul de Minas / Vale do Paraíba → tag `ICP Principal` + prioridade alta (fonte: DMO + call 26/08).
- **RN-05** SLA de primeiro contato: 30 min em horário útil para leads do ICP; 2h para leads fora do ICP (proposta; baseline medido na F1). Tarefa de SLA vencida gera notificação ao CEO no mesmo dia e registro de violação para o painel mensal.
- **RN-06** Duplicidade: CNPJ ou e-mail com negócio ativo → nota no negócio existente + notificação; nunca card duplicado.
- **RN-07** Leads <10 vidas, fora da praça ou incompletos: regra formal pendente do cliente (gate D7-3) — enquanto não definida, leads fora do ICP entram na fila com tag `Fora ICP` e prioridade baixa; leads INCOMPLETOS (sem campos para calcular porte/praça) vão para a fila de exceção, nunca recebem tag calculada. D7-3 deve ser resolvido ANTES do go-live da F2; se não for, a F2 entra com o comportamento provisório acima e a reescrita posterior é emenda aprovada.
- **RN-08** IA (F4): transbordo humano obrigatório nos casos do RF-10; log completo de todas as conversas; nenhuma ação fora do WhatsApp + Agendor.
- **RN-09** LGPD: base de reativação (F3) e WhatsApp (F4) exigem base legal e opt-out registrados; decisão documentada na F1.

## 4. Requisitos não funcionais

- **RNF-01** Nenhuma fase depende de integração não confirmada: F1 zero integrações; F2+ só inicia com credenciais em mãos.
- **RNF-02** Toda automação tem caminho de erro visível (lead que falha na ingestão fica em fila de exceção, nunca perdido).
- **RNF-03** Dados de contato (PII) acessíveis apenas ao comercial e à consultora; logs de conversa IA retidos conforme política LGPD definida na F1. Cobertura: checklist da F1 (política documentada) e CA-4-03 (log de conversas).
- **RNF-04** Reversibilidade: F2 pode ser desligada sem perda de dados (formulário continua funcionando manualmente); F4 tem critério quantificado de pausa/rollback (ver RF-10). Cobertura: checklist da F2 e CA-4-04.

## 5.1 Dependência declarada do K3

**K3 (4 vendas/mês no ICP) = conversão × volume.** Este sistema ataca conversão e velocidade (K1, K2, reativação, SDR); o VOLUME de leads permanece sob responsabilidade da agência de marketing (fora do controle do sistema — LP nova é evolução condicionada, F5 é somente leitura). Se o volume não subir, K3 pode não ser atingido mesmo com K1/K2 batendo. Recomendação registrada: decompor K3 em meta de conversão (controlável pelo sistema) × meta de volume (responsabilidade da agência) na primeira revisão mensal após o baseline.

## 5. Fases

### Fase 1 — Fundação manual (sem integração, sem LP)
**Entrega palpável:** a operação comercial rodando em fila estruturada com régua de baseline.
- RF-01 fila manual com estágios e tags ICP.
- RF-02 e-mail institucional (template, disparo manual).
- RF-03 roteiro SPIN + checklist de qualificação.
- RF-04 baseline congelado (volume/semana, speed-to-lead, conversão, vendas/mês).
- RF-05 preparação de integração (mapeamento de campos, contrato de webhook, checklist de credenciais, LGPD/WhatsApp documentados).
- **Demonstração visível:** primeira semana operando 100% na fila, com baseline documentado.
- **Critérios de aceite:** (a) 100% dos leads da semana registrados na fila com estágio, tag ICP e próxima ação; (b) template de e-mail aplicado a todo lead novo; (c) baseline congelado com as 4 métricas; (d) mapeamento de campos formulário→Agendor revisado; (e) gates D7 listados com responsável e prazo.

### Fase 2 — Integração determinística
**Entrega palpável:** lead do formulário aparece no Agendor em segundos, no funil certo, sem digitação.
- RF-06 ingestão automática + anti-duplicidade; RF-07 roteamento VEN + tags; RF-08 tarefa SLA 30min.
- **Pré-condição:** credenciais Agendor + permissões de webhook confirmadas (gate).
- **Demonstração visível:** lead de teste preenchido no formulário aparece no VEN com tags e tarefa criadas.
- **Critérios de aceite:** (a) 0 leads fora do VEN em 2 semanas de operação; (b) duplicidade tratada por nota, 0 cards duplicados; (c) tarefa de contato criada com prazo correto; (d) fila de exceção recebe leads com falha de ingestão; (e) K1 medido automaticamente a partir daí.

### Fase 3 — Reativação de base
**Entrega palpável:** fila de reativação rodando com registro de resultado.
- RF-09 fila de perdidos/dormintes com próxima ação e data.
- **Pré-condição:** F2 concluída OU autorização da consultora para rodar em paralelo (a reativação trabalha a base EXISTENTE do Agendor, não o fluxo de formulário — dependência técnica mínima; a ordem D2 é preferência de sequência, não bloqueio técnico).
- **Demonstração visível:** primeira leva de 50 clientes reativados com resultado registrado.
- **Critérios de aceite:** (a) base segmentada (perdido/dorminte/ativo) com critério explícito; (b) toda tentativa com resultado e próxima ação; (c) critério de saída aplicado; (d) opt-out registrado (RN-09).

### Fase 4 — SDR de IA (modo assistido)
**Entrega palpável:** IA respondendo o lead no WhatsApp em minutos, com transbordo humano.
- RF-10 agente assistido com transbordo; RN-08 limites e logs.
- **Pré-condições:** WhatsApp oficial + LGPD (gate); causa-raiz do agente anterior documentada (gate).
- **Demonstração visível:** conversa real lead↔IA com transbordo executado e registrado.
- **Critérios de aceite:** (a) 100% dos gatilhos de transbordo testados com prova; (b) IA sem acesso a preço/desconto (prova negativa); (c) log completo das conversas; (d) modo sombra por 2 semanas antes de operar com lead real; (e) K1 ≤ 30min medido com IA no ar.

### Fase 5 — Loop Meta/Google Ads
**Entrega palpável:** relatório semanal automático das campanhas.
- RF-11 relatório de campanhas (somente leitura).
- **Pré-condição:** token Meta/Google Ads (gate).
- **Demonstração visível:** primeiro relatório semanal entregue.
- **Critérios de aceite:** (a) relatório com gasto/resultados por campanha; (b) entrega automática semanal; (c) dado conciliado com o painel da plataforma; (d) CPL calculado contra leads da fila (F1–F2).

## 6. Matriz de rastreabilidade (resumo)

| Fonte | Achado/Decisão | Requisito | Fase |
|---|---|---|---|
| Call 26/08 | Cliente aprova SDR + reativação + dashboard + site | RF-10, RF-09, RF-11 | F4, F3, F5 |
| Kim 10/09 (D2) | F1 sem integração/LP; ordem das fases | RF-01..05 | F1 |
| Kim 10/09 (D3) | LP removida → evolução condicionada | — (fora de escopo) | — |
| Kim 10/09 (D4) | Manter Agendor no MVP | RF-06..08 | F2 |
| Kim 10/09 (D5) | IA assistida, transbordo, causa-raiz prévia | RF-10, RN-08 | F4 |
| Call 26/08 (D6) | Meta 4 vendas/mês ICP; leads com atraso 1–2 dias | K1–K3, RN-04, RN-05 | F1–F5 |
| Escopo base RN01 | Funil VEN exclusivo | RN-01, RF-07 | F2 |
| Escopo base RN02 | Campos obrigatórios | RN-02, RF-06 | F2 |
| Escopo base RN03 | Disparo institucional | RN-03, RF-02 | F1 |
| Escopo base RN06 | Trava de duplicidade | RN-06, RF-06 | F2 |
| Análise crítica AC (baseline ausente) | Congelar baseline | RF-04 | F1 |
| Análise crítica AC (Agendor não confirmado) | Preparação de integração + gate | RF-05 | F1/F2 |
| Análise crítica AC (recorte misto) | Jurídico/implantação fora do escopo | — (fora de escopo) | — |
| Análise crítica AC (segurança/LGPD) | RN-09, RNF-03 | RN-09, RNF-03 | F1, F3, F4 |

## 7. Decisões humanas pendentes (gates — não bloqueiam F1)

| ID | Decisão | Dono | Necessária para |
|---|---|---|---|
| D7-1 | Credenciais do Agendor | Cliente | F2 |
| D7-2 | Token Meta/Google Ads | Cliente | F5 |
| D7-3 | Regra p/ leads <10 vidas / fora da praça / incompletos | Consultora + cliente | F2 (RN-07 provisória) |
| D7-4 | WhatsApp oficial + base legal LGPD | Consultora + cliente | F4 |
| D7-5 | Causa-raiz do agente anterior (post-mortem conduzido pela consultora; cliente fornece acesso/histórico) | Consultora + cliente | F4 |
| D7-8 | Duração alvo por fase e datas de revisão dos gates (cronograma) | Consultora | antes da aprovação do check-escopo |
| D7-9 | Decomposição do K3 em meta de conversão × meta de volume (dependência da agência declarada na seção 5.1) | Consultora + cliente | 1ª revisão mensal pós-baseline |
| D7-6 | Aprovação do check-escopo | Consultora | antes da publicação |
| D7-7 | Aprovação do cliente/CSM | CSM/cliente | antes da execução |