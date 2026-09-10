# SPEC-1-006 — Governança da F1: gates, fonte de verdade e rotina de captação

**Fase:** 1
**Status:** planejada
**Dono:** Consultora (Kim) — documento; cliente — decisões e dono operacional
**Origem no escopo:** CA-1-06, RN-09, gates D7-1..D7-5, achados do painel (fonte única de verdade, rotina de captação, dono operacional, cobertura de SLA)
**Degrau da solução:** construção mínima — documento de governança de 1 página + registro dos gates, porque os riscos da F1 são de adoção e decisão humana, não técnicos.

## Resultado observável

Documento de governança assinado com: (1) regra de fonte única de verdade na F1 (fila substitui ou espelha o Agendor), (2) rotina de captação manual (quem monitora formulário/e-mail, em quais horários), (3) dono operacional da fila no cliente (nome definido com Alexandre), (4) regra de cobertura do SLA quando o SDR estiver ausente, (5) gates D7-1..D7-5 com responsável e prazo, (6) política LGPD mínima (retenção de logs, acesso a PII).

## Limites e dependências

- **Inclui:** documento de governança + registro dos gates com prazo + política LGPD mínima da F1.
- **Fora de escopo:** implementação de qualquer gate (são decisões humanas das fases futuras); contrato formal LGPD; DPO.
- **Entradas e pré-condições:** decisões D2–D6 registradas; disponibilidade do Alexandre (viaja 11–25/09 — decisões podem ser coletadas por escrito).
- **Saídas/artefatos:** documento de governança (1 página) + tabela de gates com responsável/prazo.
- **Dependências e responsáveis:** consultora redige; Alexandre valida por escrito (e-mail/WhatsApp) mesmo durante a viagem.
- **Risco e plano B:** Alexandre não responder durante a viagem → coletar decisões por escrito com prazo pós-viagem (25/09); fila opera com regras provisórias da consultora registradas como tal.
- **Rollback ou reversão:** documento revisável por emenda; gates são decisões humanas e podem ser redecididos com registro.

## Fluxo e regras

1. Redigir o documento de governança com as 6 seções.
2. Coletar do cliente (por escrito): dono operacional da fila, rotina de captação aprovada, regra de cobertura de SLA, respostas do checklist de credenciais (com SPEC-1-005).
3. Registrar gates D7-1..D7-5 com responsável e prazo em tabela.
4. Documentar política LGPD mínima: quem acessa PII, retenção dos registros da fila, opt-out. **Esta política (mesmo provisória, com prazo) é PRÉ-CONDIÇÃO da primeira semana de operação da fila (SPEC-1-001) — a fila não coleta PII real antes dela existir.** A política de opt-out da reativação/WhatsApp fica na SPEC-1-005 (dossiê de integração); esta SPEC é dona do acesso a PII e retenção da fila.
5. Assinatura/validação por escrito do cliente.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Cliente responde durante a semana | Documento completo e validado | — |
| Limite | Alexandre viajando | Decisões coletadas por escrito; itens pendentes marcados com prazo 25/09 | Fila opera com regras provisórias registradas |
| Falha | SDR ausente sem cobertura definida | Regra de cobertura do documento define quem assume (CEO) | SLA violado é registrado, não escondido |

## Checklist de execução

- [ ] Documento de governança redigido (6 seções)
- [ ] Regra de fonte única de verdade definida e registrada
- [ ] Rotina de captação manual definida (horários + responsável)
- [ ] Dono operacional da fila definido com o cliente
- [ ] Regra de cobertura de SLA definida
- [ ] Gates D7-1..D7-5 com responsável e prazo registrados
- [ ] Política LGPD mínima documentada
- [ ] Validação do cliente por escrito

## Critérios de aceite

- [ ] **CA-1-06:** aprovado SOMENTE com os 4 itens completos (pass/fail por item): (i) gates D7-1..D7-5 com responsável e prazo; (ii) regra de fonte única de verdade definida (registro único aqui — SPEC-1-001 apenas referencia); (iii) rotina de captação manual definida; (iv) dono operacional da fila definido. Item pendente do cliente (viagem) = CA não batido, com prazo 25/09 registrado.
- [ ] **CA-1-06a:** documento de governança validado por escrito pelo cliente (ou itens pendentes com prazo explícito pós-viagem).

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Sem governança: fila sem dono e gates sem prazo | Verificar ausência de documento e de prazos | Falha: adoção e gates sem régua | Registro da verificação (nota no dossiê) |
| GREEN | Documento operando | Preencher as 6 seções com respostas do cliente | Documento completo com validação | Documento + e-mail de aprovação |
| REFACTOR/REGRESSÃO | Revisão semanal da F1 | Conferir aderência à rotina e aos donos definidos | Desvios registrados e corrigidos | Registro semanal |

**Dados/fixtures:** decisões D2–D6 já registradas; calendário do Alexandre (viagem 11–25/09).
**Caminhos de erro obrigatórios:** cliente não responde (prazo pós-viagem + regras provisórias), SDR ausente (regra de cobertura), gate vencido (escalação à consultora).
**Quando não houver código:** cenário verificável acima.

**Evidência exigida:** documento de governança + validação por escrito do cliente.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| — | *preenchido por gerar-tasks* | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
