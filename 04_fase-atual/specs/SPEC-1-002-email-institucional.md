# SPEC-1-002 — E-mail institucional de apresentação (disparo manual)

**Fase:** 1
**Status:** planejada
**Dono:** Consultora (Kim) — template; SDR Risomed — disparo
**Origem no escopo:** RF-02, RN-03, Fase 1 (escopo definitivo 10/09)
**Degrau da solução:** reuso — template de e-mail no Gmail/Outlook existente do cliente (rascunho salvo), sem ferramenta nova, porque a F1 veda automação de disparo.

## Resultado observável

Todo lead novo recebe, em até 1 dia útil, o e-mail institucional da Risomed com a proposta de valor — enviado manualmente pelo SDR a partir de um template aprovado — e o envio fica registrado na ficha do lead na fila (SPEC-1-001).

## Limites e dependências

- **Inclui:** template de e-mail (assunto + corpo + apresentação anexada/link), regra de personalização mínima (nome do solicitante e empresa), registro do envio na fila.
- **Fora de escopo:** disparo automático (F2+); sequência de nutrição; assinatura HTML complexa; landing page.
- **Entradas e pré-condições:** lead registrado na fila (SPEC-1-001); material institucional da Risomed fornecido pelo cliente; remetente institucional definido (conta de e-mail).
- **Saídas/artefatos:** template salvo como rascunho/modelo no e-mail do cliente + coluna "e-mail enviado em" na fila.
- **Dependências e responsáveis:** cliente fornece apresentação institucional atual e define remetente; SDR executa o disparo.
- **Risco e plano B:** material institucional desatualizado → consultora revisa com o cliente antes de aprovar o template; se o cliente não enviar, template mínimo com texto aprovado por ele.
- **Rollback ou reversão:** template pode ser substituído sem impacto; registro na fila permanece.

## Fluxo e regras

1. SDR abre o template salvo no e-mail.
2. Personaliza: nome do solicitante + empresa (única edição permitida sem aprovação).
3. Envia para o lead com a apresentação anexada.
4. Registra na fila: data de envio na coluna "e-mail enviado em" (RN-03: todo lead novo recebe).
5. **Conferência de destinatário:** o endereço é SEMPRE colado da fila (nunca digitado) e conferido antes do envio — apresentação institucional enviada a destinatário errado vaza material e expõe a prospecção.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Lead novo ICP registrado | E-mail enviado em até 1 dia útil, registrado na fila | — |
| Limite | Lead `Fora ICP` | E-mail institucional enviado igualmente (RN-03 não distingue) | — |
| Falha | E-mail do lead inválido (bounce) | Registrar na fila "e-mail inválido" e seguir para contato telefônico | Nunca deixar a linha sem registro |
| Falha | Destinatário divergente da ficha | Envio cancelado antes de sair; corrigir na fila e reenviar | Regra: colar da fila, nunca digitar |

## Checklist de execução

- [ ] Material institucional atual recebido do cliente
- [ ] Template escrito e aprovado pelo cliente (Alexandre)
- [ ] Template salvo como modelo/rascunho no e-mail do SDR
- [ ] Coluna "e-mail enviado em" adicionada à fila
- [ ] Regra de personalização documentada no documento de uso
- [ ] Regra de conferência de destinatário (colar da fila, nunca digitar) documentada

## Critérios de aceite

- [ ] **CA-1-02:** template de e-mail aplicado a todo lead novo da semana de auditoria, com registro na ficha (data de envio preenchida em 100% das linhas com e-mail preenchido; "válido" = campo existe e formato sintático — bounce é tratado DEPOIS do envio como caminho de erro, não como pré-filtro).
- [ ] **CA-1-02a:** template aprovado por escrito pelo cliente antes do primeiro envio (e-mail/WhatsApp de aprovação). **Fallback de viagem (11–25/09):** aprovação coletada por escrito; se não obtida, template mínimo provisório aprovado pela consultora com registro e revisão obrigatória até 25/09.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Sem template: SDR escreve e-mail do zero | Verificar inexistência de modelo salvo | Falha: não há template aprovado | Print da caixa de e-mail |
| GREEN | Template operando | Enviar para 1 lead de teste (e-mail da consultora) com personalização | E-mail entregue com apresentação anexa e registro na fila; destinatário confere com a ficha | Print do e-mail enviado + linha da fila |
| GREEN | Aprovação humana (CA-1-02a) | Coletar aprovação por escrito do cliente (ou registrar fallback provisório) | Aprovação registrada antes do 1º envio real | E-mail/WhatsApp de aprovação |
| REFACTOR/REGRESSÃO | Semana de uso | Auditoria: 100% dos leads novos com "e-mail enviado em" preenchido ou "e-mail inválido" registrado | Sem linha sem registro | Planilha de auditoria |

**Dados/fixtures:** 1 lead de teste (e-mail da consultora como destinatário) para validar o template antes do uso real.
**Caminhos de erro obrigatórios:** bounce (registrar e seguir), lead sem e-mail (registrar "sem e-mail" e priorizar telefone), template rejeitado pelo cliente (revisar antes de usar).
**Quando não houver código:** cenário verificável acima.

**Evidência exigida:** print do e-mail enviado + aprovação do cliente + auditoria da fila.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| — | *preenchido por gerar-tasks* | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
