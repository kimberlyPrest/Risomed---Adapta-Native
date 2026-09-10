# Fase 5 — Loop Meta/Google Ads

**Status:** check-escopo APROVADO · **Pré-condição:** token Meta/Google Ads (gate D7-2)

## Resultado
Relatório semanal automático das campanhas da agência, dando ao cliente instrumento de cobrança baseado em dados — sem que a consultoria opere as campanhas.

## Entregas
1. **Relatório de campanhas (RF-11):** gasto por campanha, resultados, tendência; somente leitura.
2. **Entrega automática:** relatório semanal enviado ao cliente (e-mail/WhatsApp).
3. **CPL real:** custo por lead calculado contra os leads da fila (F1–F2), fechando o loop marketing → comercial.

## Limites
- **Nota de prioridade (do escopo, RF-11):** F5 é a fase cortável sem comprometer K1–K2; se o prazo apertar, é o sacrifício declarado.
- Somente leitura das plataformas; nenhuma alteração de campanha.
- Sem otimização automática de lances/verba.

## Sequência ASA
Automático: coleta e envio do relatório. Semiautomático: nada. Humano: cobrança/gestão da agência.

## Checklist
- [ ] Token Meta/Ads obtido (gate)
- [ ] Coleta de métricas implementada e testada
- [ ] Relatório semanal com gasto/resultados/tendência
- [ ] Entrega automática configurada
- [ ] CPL integrado aos dados da fila

## Critérios de aceite
- **CA-5-01:** relatório com gasto e resultados por campanha.
- **CA-5-02:** entrega automática semanal funcionando (2 semanas consecutivas).
- **CA-5-03:** dado conciliado com o painel da plataforma (amostra de 1 semana).
- **CA-5-04:** CPL calculado contra leads da fila e comparado ao volume/semana do baseline da F1 (CPL não faz parte do baseline congelado; por campanha apenas se o formulário capturar origem — ver RF-05; sem origem, CPL agregado).
