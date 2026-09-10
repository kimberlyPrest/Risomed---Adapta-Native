# Check de Escopo — Risomed

**Estado: APROVADO**

| Gate | Descrição | Dono | Estado |
|---|---|---|---|
| Check-escopo | Aprovação da consultora (Kim) sobre PRD, escopo, fases e matriz | Consultora | **APROVADO** (Kim, 10/09/2026 15:13) |
| Check-cliente | Aprovação do cliente/CSM antes da execução | CSM/cliente | PENDENTE |

## Observações para a consultora

- F1 não depende de credencial/token (decisão D2), mas EXIGE adoção do SDR na fila e acesso aos dados históricos para o baseline — premissa reescrita após o painel.
- RN-07 é provisória até D7-3; lead incompleto vai para fila de exceção (nunca tag calculada). D7-3 deve ser resolvido antes do go-live da F2.
- K1–K3 só se tornam verificáveis após o baseline congelado da F1 (RF-04, janela mínima 4 semanas/20 leads, medido da ORIGEM do lead).
- **Dependência declarada do K3 (seção 5.1 do escopo):** o sistema ataca conversão e velocidade; o volume de leads segue com a agência. Recomendação: decompor K3 (gate D7-9) na 1ª revisão mensal pós-baseline.
- Painel de revisão 10/09: 4 lentes, 6 achados graves — 1 corrigido (K1 viciado pela digitação), 5 tratados como gates/emendas (cronograma D7-8, K3×volume D7-9, SLA sem escalação → RN-05 emendado, formulário sem webhook → RF-05 emendado, F3 refém da F2 → pré-condição flexibilizada). JSONs em `revisoes/`.
