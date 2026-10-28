# Verificação independente de fechamento — TASK-1-001

**Data:** 2026-10-28
**Sistema verificado:** https://jornada-comercial-risomed-0b95a.shrd00.internal.goskip.dev
**Preview:** https://jornada-comercial-risomed-0b95a--preview.goskip.app
**Veredito: NÃO PRONTA** — a implementação funciona, mas dois critérios não são fecháveis como estão escritos.

## 1. Disponibilidade

| Item | Resultado | Evidência |
|---|---|---|
| API backend | ✅ PASSOU | `GET /api/health` → HTTP 200 `{"message":"API is healthy."}` |
| Preview (frontend) | ✅ PASSOU | `GET /` → HTTP 200 |
| Login do champion | ✅ PASSOU | `POST /auth-with-password` → HTTP 200, token emitido |

## 2. Critérios de aceite

### CA-1-01b — tag ICP e estágio restritos à lista — ✅ PASSOU

| Prova | Ação | Resultado |
|---|---|---|
| Tag inválida | `POST /fila_leads/records` com `tag_icp` fora da lista | HTTP 400 — rejeitado |
| Estágio inválido | `POST /fila_leads/records` com `estagio` fora da lista | HTTP 400 — rejeitado |
| Campos obrigatórios | `POST` sem os campos da SPEC | HTTP 400 com `validation_required` em `data_origem`, `data_proxima_acao`, `estagio`, `origem`, `proxima_acao`, `solicitante`, `tag_icp` |

A validação de domínio roda no servidor, não só na tela.

### CA-1-01c — prova negativa de acesso — ✅ PASSOU (com risco registrado)

O critério pede que uma conta **não autorizada** falhe. O modelo é: **entrar exige a chave de convite**. Sem ela não existe conta, e sem conta não há acesso.

| # | Prova | Ação | Resultado |
|---|---|---|---|
| 1 | Cadastro sem convite | `POST /users/records` sem `invite_key` | ✅ HTTP 400 — recusado |
| 2 | Cadastro com convite | `POST /users/records` com a chave válida | ⚠️ HTTP 200 — conta criada (usada na prova) |
| 3 | Leitura sem autenticação | `GET /fila_leads/records` sem token | ✅ HTTP 200 com **0 registros** |
| 4 | Registro específico sem autenticação | `GET /fila_leads/records/<id>` sem token | ✅ HTTP 404 |
| 5 | Criação sem autenticação | `POST /fila_leads/records` sem token | ✅ HTTP 400 |
| 6 | Forjar autoria | `POST` com `created_by` de outro usuário | ✅ HTTP 400 — recusado |

**RISCO REGISTRADO (alto, não reprova o CA):** dentro da fila não há separação por usuário nem por papel. Conta criada com a chave de convite lista, altera e **apaga** leads de outra pessoa. Prova isolada: conta nova listou 3 registros e apagou um registro-sonda criado pelo champion (HTTP 204); o registro passou a 404 para o dono. Não existe perfil só-leitura; o botão de excluir aparece para todos.

Consequências: o único guarda da fronteira de PII (RNF-03) é uma chave compartilhada, que já circulou fora de cofre de segredos — recomenda-se rotacionar. Segregação por papel deve entrar antes do uso com dados reais.

### CA-1-01d — prova de restauração — ❌ NÃO SATISFATÓRIO

| Prova | Resultado |
|---|---|
| Export CSV na interface | ✅ existe (15 colunas, separador `;`, BOM UTF-8) |
| `GET /api/backups` | ❌ HTTP 403 — sem acesso a backups |
| Restauração pontual de registro | ❌ recurso inexistente; recuperar exigiu recriar à mão, com id novo |

A SPEC pede restauração via histórico do Google Sheets, que não existe nesta plataforma. O critério precisa ser reescrito.

### CA-1-01 e CA-1-01a — não executados

Dependem de 1 semana de operação real do SDR e da comparação de 3 leads com os e-mails originais. Não são verificáveis por teste técnico.

## 3. Integridade dos dados após a verificação

| Item | Estado |
|---|---|
| Madeira Madeira (Apresentação, ICP Principal) | ✅ intacto |
| Academia Corpo Forte (Prospecção, ICP Principal) | ⚠️ apagado pela prova de exclusão e recriado com todos os campos — novo id `e7jmfg4tzfzf0x3` (original `h4patyf6gisxd36`) |
| Registros-sonda | ✅ removidos |

Nenhum dado de cliente real foi perdido: os 2 leads seguem na fila com todos os campos.

## 4. Risco residual — conta de teste não removível

`probe.qa.1793223729@example.com` continua ativa e autenticável: `DELETE` → 403, troca de senha → 403, login → 200. Um superusuário do Skip Cloud precisa apagá-la.

## 5. O que a verificação NÃO alterou

- Nenhum arquivo de código do projeto foi modificado.
- Nenhuma regra de coleção foi alterada (acesso administrativo ao Skip Cloud indisponível nesta sessão).
- Os dois leads reais foram preservados; o registro apagado pela prova foi restaurado.

## 6. Veredito e o que falta

**NÃO PRONTA.** Impedem o fechamento:

1. **Divergência de plataforma** — a SPEC determina Google Sheets; a implementação é aplicação Skip. Os CAs 01c e 01d citam recursos que só existem no Sheets. Requer emenda aprovada pela consultora (proposta em `emenda-spec-1-001-proposta.md`).
2. **CA-1-01d sem solução na plataforma** — decidir entre export periódico + reimportação comprovada ou habilitar backup no provedor.

Antes de operar com dados reais:

3. Corrigir a segregação de acesso na fila (só-leitura × editor × dono) e rotacionar a chave de convite.
4. Remover a conta de teste por superusuário.
5. Reexecutar CA-1-01c e CA-1-01d após 1–3.
