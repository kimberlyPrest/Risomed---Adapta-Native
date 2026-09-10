# SPEC-1-004 — Baseline congelado (régua de K1–K3)

**Fase:** 1
**Status:** planejada
**Dono:** Consultora (Kim) — medição e documento; cliente — validação
**Origem no escopo:** RF-04, K1–K3 (escopo definitivo 10/09), achado do painel (baseline ausente)
**Degrau da solução:** construção mínima — documento de baseline medido a partir da fila (SPEC-1-001) e dos registros do cliente, sem ferramenta de analytics, porque não há fonte histórica confiável (timestamps não confiáveis no Agendor).

## Resultado observável

Documento de baseline assinado pela consultora e validado pelo cliente, com as 4 métricas da régua: volume de leads/semana, speed-to-lead atual (da ORIGEM do lead ao primeiro contato), conversão por etapa e vendas/mês no ICP. A partir dele, K1–K3 se tornam verificáveis.

## Limites e dependências

- **Inclui:** definição operacional de cada métrica, janela de observação (mínimo 4 semanas ou 20 leads — o que ocorrer por último), coleta prospectiva via fila, documento final com valores congelados.
- **Fora de escopo:** dashboards; recuperação de histórico antigo (timestamps não confiáveis — dados históricos do Agendor são referência complementar apenas); metas por segmento.
- **Entradas e pré-condições:** fila operando (SPEC-1-001); acesso de leitura aos registros de venda do cliente (vendas/mês no ICP).
- **Saídas/artefatos:** documento de baseline congelado (PDF/Doc) com data, janela, valores e assinaturas.
- **Dependências e responsáveis:** SDR opera a fila com data de origem correta (SPEC-1-001); cliente fornece vendas/mês do ICP; consultora mede e assina.
- **Risco e plano B:** amostra fraca no fim da janela → congelar com ressalva registrada (decisão da consultora no documento) e revisar na 1ª revisão mensal; se o SDR não preencher a origem, o speed-to-lead fica incompleto → auditoria semanal corrige antes do congelamento.
- **Rollback ou reversão:** baseline pode ser reaberto por decisão registrada do consultor (emenda), nunca silenciosamente.

## Fluxo e regras

1. Definir as 4 métricas com definição operacional escrita (o que conta, de onde vem o número). **Definição de "venda no ICP": contrato assinado (assinatura eletrônica confirmada) com empresa elegível ao ICP (10–100 vidas na praça, validado na ficha do lead); a data da venda é a data da assinatura. Definição validada pelo cliente no documento.**
2. Coletar prospectivamente durante a janela mínima (4 semanas/20 leads): volume/semana (contagem da fila), speed-to-lead (data de origem → primeiro registro de contato), conversão por etapa (contagem por estágio), vendas/mês ICP (registro do cliente).
3. Congelar: documento com valores, janela, método e ressalvas; assinatura da consultora + validação do cliente.
4. A partir do congelamento, qualquer mudança de régua é emenda aprovada (nunca silenciosa).

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Janela completa com ≥20 leads | Baseline congelado com 4 métricas | — |
| Limite | Janela completa com <20 leads | Congelar com ressalva registrada OU estender janela (decisão da consultora no documento) | Nunca congelar sem registrar a ressalva |
| Falha | SDR não preencheu data de origem em parte dos leads | Speed-to-lead calculado só sobre leads completos, com % de cobertura registrada | % de cobertura <80% → estender janela |

## Checklist de execução

- [ ] Definição operacional das 4 métricas escrita
- [ ] Janela de observação iniciada (data de início registrada)
- [ ] Coleta semanal conferida pela consultora (4 semanas)
- [ ] Vendas/mês no ICP obtidas do cliente
- [ ] Documento de baseline redigido com valores, janela, método e ressalvas
- [ ] Assinatura da consultora + validação do cliente registradas
- [ ] Documento armazenado na pasta do projeto com acesso restrito (mesmo padrão da fila — SPEC-1-006/CA-1-01c)

## Critérios de aceite

- [ ] **CA-1-03:** baseline congelado com as 4 métricas (volume/semana, speed-to-lead da ORIGEM do lead, conversão, vendas/mês ICP), com janela mínima de 4 semanas ou 20 leads (o que ocorrer por último) — amostra menor só com decisão registrada da consultora.
- [ ] **CA-1-03c:** documento assinado pela consultora e validado pelo cliente por escrito (e-mail/WhatsApp).

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Sem baseline: K1–K3 não verificáveis | Tentar responder "qual o speed-to-lead atual?" sem documento | Falha: não há número congelado | Registro da pergunta sem resposta (nota no dossiê) |
| GREEN | Coleta operando | 1 semana de coleta via fila com definições escritas | 4 métricas calculáveis com % de cobertura | Planilha de coleta |
| GREEN | Janela mínima cumprida (CA-1-03) | Fechar a janela: 4 semanas OU 20 leads, o que ocorrer por último | Janela fechada com critério atendido e registrado | Documento de congelamento com datas e contagem |
| REFACTOR/REGRESSÃO | Congelamento | Documento final assinado + validação do cliente | Baseline congelado, régua única | Documento assinado |

**Dados/fixtures:** coleta real da fila; vendas/mês do ICP fornecidas pelo cliente (1–2, conforme call 26/08 — confirmar na coleta).
**Caminhos de erro obrigatórios:** amostra fraca (ressalta ou estende), cobertura de origem <80% (estende), cliente não fornece vendas (usar estimativa declarada com ressalva).
**Quando não houver código:** cenário verificável acima.

**Evidência exigida:** documento de baseline assinado + planilha de coleta.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| — | *preenchido por gerar-tasks* | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
