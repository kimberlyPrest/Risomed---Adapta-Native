# SPEC-1-003 — Roteiro SPIN + checklist de qualificação

**Fase:** 1
**Status:** planejada
**Dono:** Consultora (Kim) — documento; SDR Risomed — uso
**Origem no escopo:** RF-03, Fase 1 (escopo definitivo 10/09), RN-04
**Degrau da solução:** construção mínima — documento de 2 páginas (roteiro SPIN + checklist), sem ferramenta, porque a qualificação é 100% humana na F1.

## Resultado observável

O SDR conduz a ligação/WhatsApp de primeiro contato com um roteiro SPIN estruturado e fecha cada conversa com um checklist de qualificação preenchido (vidas, praça, decisor, urgência) — registrado na fila. O cliente demonstra: "qualquer contato segue o mesmo padrão e gera o mesmo registro".

## Limites e dependências

- **Inclui:** roteiro SPIN (Situação, Problema, Implicação, Necessidade) adaptado ao produto Risomed (odonto/telemedicina/bem-estar/NR-01 para PME 10–100 vidas); checklist de qualificação com campos binários; regra de registro na fila.
- **Fora de escopo:** script de IA; treinamento avançado de vendas; material de negociação de preço; proposta comercial.
- **Entradas e pré-condições:** fila operando (SPEC-1-001); dores do cliente conhecidas (DMO + call 26/08).
- **Saídas/artefatos:** documento de 2 páginas + colunas de qualificação na fila (decisor identificado? urgência?).
- **Dependências e responsáveis:** consultora escreve; cliente (Alexandre) valida o roteiro antes do uso; SDR usa.
- **Risco e plano B:** roteiro não usado por resistência do SDR → versão de bolso (1 página) e revisão em call semanal.
- **Rollback ou reversão:** documento substituível; nenhuma dependência técnica.

## Fluxo e regras

1. Antes do contato: SDR lê a ficha do lead na fila (vidas, cidade, origem).
2. Durante: conduz SPIN na ordem (Situação → Problema → Implicação → Necessidade), adaptando ao segmento.
3. Ao final: preenche checklist de qualificação — [ ] 10–100 vidas confirmado, [ ] praça atendida, [ ] decisor identificado (nome/cargo), [ ] urgência/timeline, [ ] interesse em apresentação.
4. Registra na fila: resultado do contato + campos do checklist + próxima ação com data.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Lead ICP atendido por telefone | Checklist 100% preenchido + próxima ação agendada | — |
| Limite | Lead não decide (funcionário) | Campo "decisor" fica "não identificado" + próxima ação = conseguir o decisor | Nunca marcar qualificado sem decisor |
| Falha | Lead recusa/ignora | Registrar motivo + estágio Perdido ou nova tentativa com data | Sem linha sem registro |

## Checklist de execução

- [ ] Roteiro SPIN escrito e adaptado ao produto/ICP
- [ ] Checklist de qualificação com 5 campos binários
- [ ] Colunas de qualificação adicionadas à fila
- [ ] Validação do roteiro pelo cliente (Alexandre) por escrito
- [ ] SDR treinado (role-play de 1 sessão)

## Critérios de aceite

- [ ] **CA-1-03a:** roteiro SPIN + checklist validados por escrito pelo cliente antes do primeiro uso.
- [ ] **CA-1-03b:** na semana de auditoria, 100% dos contatos registrados na fila têm checklist preenchido (5 campos) e próxima ação com data.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Sem roteiro: contato livre sem registro | Verificar ausência de documento e campos na fila | Falha: não há padrão nem registro | Print da fila sem colunas |
| GREEN | Roteiro operando | Role-play com 1 lead de teste + preenchimento do checklist | Checklist preenchido + registro na fila | Print da linha + documento |
| GREEN | Validação humana (CA-1-03a) | Coletar validação por escrito do cliente (fallback de viagem: prazo 25/09, uso provisório registrado) | Roteiro validado antes do uso real | E-mail/WhatsApp de validação |
| REFACTOR/REGRESSÃO | Semana de uso | Auditoria: 100% dos contatos com checklist completo | Sem contato sem registro | Planilha de auditoria |

**Dados/fixtures:** 1 lead de teste para role-play; dores reais do cliente (DMO) como insumo do roteiro.
**Caminhos de erro obrigatórios:** recusa (motivo + estágio), decisor não identificado (próxima ação específica), lead sem WhatsApp (ligação).
**Quando não houver código:** cenário verificável acima.

**Evidência exigida:** documento final + aprovação do cliente + auditoria da fila.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| — | *preenchido por gerar-tasks* | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
