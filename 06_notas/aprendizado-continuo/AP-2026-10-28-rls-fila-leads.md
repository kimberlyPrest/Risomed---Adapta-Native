# AP-2026-10-28 — Fila sem segregação de acesso por dono

**Origem:** verificação independente de fechamento da TASK-1-001 (2026-10-28)
**Área:** segurança de dados / regras de acesso
**Gatilho:** prova negativa de acesso (CA-1-01c)

## O que aconteceu

A coleção `fila_leads` libera listagem, leitura, alteração e exclusão para qualquer usuário autenticado. Como o cadastro exige apenas uma chave de convite compartilhada, quem tiver a chave entra e passa a operar sobre **todos** os leads, inclusive apagando os de outra pessoa.

Reproduzido de forma limpa: conta nova criada com a chave → listou 3 registros → apagou o registro-sonda do dono (HTTP 204) → o registro passou a 404 para o dono.

## Por que passou nos testes anteriores

O reteste humano de 22/10 exercitou o fluxo funcional (criar lead, validar, mover estágio, exportar) sempre **com a conta do próprio champion**. Falta de segregação só aparece quando se testa com uma segunda conta — exatamente o que a CA-1-01c pede e que não havia sido executado ponta a ponta.

## Regra para as próximas tasks

1. Toda coleção com PII precisa de prova negativa **com duas contas distintas**: a do champion e uma de teste. Testar só com a conta do dono não prova isolamento.
2. Regra de acesso nunca deve ser "usuário autenticado" quando o cadastro não é uma lista fechada. Usar filtro por `created_by` ou lista de e-mails autorizados, e definir papéis (só-leitura × editor).
3. Chave de convite é segredo: não pode aparecer em documento versionado em repositório público. Se circular, precisa ser rotacionada.
4. Conta criada para prova negativa precisa ser removível. Se o provedor não permite ao cliente apagar, a prova tem de ser feita em ambiente descartável, não em produção — aqui a conta de teste ficou ativa e só um superusuário remove.

## Pendência

A correção depende de acesso ao Skip Cloud (regras de coleção), indisponível na sessão de 28/10. Registrar para a consultora junto com a emenda da SPEC.
