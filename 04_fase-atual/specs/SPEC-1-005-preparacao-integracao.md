# SPEC-1-005 — Preparação de integração (Agendor + formulário + WhatsApp/LGPD)

**Fase:** 1
**Status:** planejada
**Dono:** Consultora (Kim)
**Origem no escopo:** RF-05, Fase 1 (escopo definitivo 10/09), gates D7-1/D7-3/D7-4, achados do painel (webhook não confirmado; API não testada)
**Degrau da solução:** reuso — API existente do Agendor (já provada pela consultora no Ethos) + verificação do formulário atual; nenhuma construção, porque esta SPEC é preparação documental e de evidência para a F2.

## Resultado observável

Dossiê de integração completo que destrava a F2 sem improvisação: (1) verificação da capacidade do formulário atual (emite POST/webhook ou só e-mail? captura origem/UTM?), (2) smoke test da API do Agendor executado com prova (tarefa com prazo em minutos, escrita de tag, busca por CNPJ/e-mail), (3) mapeamento de campos formulário → Agendor, (4) contrato de webhook desenhado, (5) checklist de credenciais/permissões enviado ao cliente, (6) decisões WhatsApp oficial + LGPD e base legal da reativação documentadas com estimativa de prazo/custo.

## Limites e dependências

- **Inclui:** tudo documental e de evidência; smoke test de API em ambiente de teste do Agendor (nunca em dados reais de produção sem autorização).
- **Fora de escopo:** implementação do webhook (F2); qualquer escrita em dados reais do cliente; criação de número WhatsApp; contratação de API oficial.
- **Entradas e pré-condições:** acesso de LEITURA à API do Agendor (já demonstrado via relatório semanal no Ethos); URL do formulário atual; material público da Meta sobre WhatsApp Business API. **Token de ESCRITA:** se indisponível na F1 (gate D7-1 é da F2), o smoke test de escrita fica condicionado — executa-se a prova negativa de produção + busca por CNPJ/e-mail (leitura) e registra-se a limitação no dossiê; a escrita (tarefa em minutos, tag) é executada no início da F2 como primeiro ato, com a mesma prova negativa. CA-1-04 é satisfeito com as provas de leitura + laudo do formulário + contrato desenhado; a prova de escrita vira pré-condição de go-live da F2 (CA-2-00).
- **Saídas/artefatos:** dossiê de integração (documento único) com as 6 seções + resultado do smoke test (log/prints).
- **Dependências e responsáveis:** consultora executa tudo; cliente/agência fornece URL do formulário e responde o checklist de credenciais; se o formulário não emitir POST, decisão humana registrada (ponte de e-mail vs. ajuste de formulário) — insumo do gate D7-1.
- **Risco e plano B:** API do Agendor não suportar tarefa com prazo em minutos → registrar limitação e propor contorno (ex.: tarefa com data + hora de criação como referência de SLA) antes da F2; formulário sem POST → decisão registrada no dossiê.
- **Rollback ou reversão:** nenhuma — nada é alterado em produção.

## Fluxo e regras

1. **Formulário:** inspecionar o formulário atual (URL fornecida pelo cliente): método de envio (POST?), campos coletados vs. RN-02, captura de origem (UTM/hidden field). Registrar resultado.
2. **Smoke test Agendor:** (a) **PRÉ-CONDIÇÃO OBRIGATÓRIA antes de qualquer escrita — prova negativa de produção:** buscar por CNPJ/e-mail de um cliente REAL da Risomed com o token do teste; retorno VAZIO prova conta de teste e libera a escrita; retorno COM dados prova token de produção e BLOQUEIA a escrita (registrar e escalar ao cliente); (b) criar tarefa com prazo em minutos, (c) escrever tag em negócio de teste, (d) buscar empresa por CNPJ e por e-mail. Registrar cada prova (log/prints). Se não existir sandbox no plano do cliente, a escrita só ocorre em negócio de TESTE criado na conta real COM autorização por escrito do cliente — nunca em dados de clientes reais.
3. **Mapeamento de campos:** tabela campo do formulário → campo do Agendor (Empresa, Contato, Negócio), com campos ausentes destacados.
4. **Contrato de webhook:** desenhar gatilho, payload, **autenticação de origem (assinatura HMAC/secret ou allowlist de IP — requisição sem credencial válida deve ser rejeitada com HTTP 401 e registrada na fila de exceção)**, tratamento de erro (fila de exceção) e anti-duplicidade — sem implementar.
5. **Credenciais:** checklist enviado ao cliente (plano do Agendor suporta webhook? permissões de API? quem cria o token?). **Regra de segredo:** token transmitido por canal acordado (gerenciador de senhas ou contato direto — nunca e-mail/WhatsApp/dossiê), armazenado FORA do dossiê; item de encerramento da F2 para revogação/rotação do token de teste.
6. **WhatsApp/LGPD:** decisão documentada — WhatsApp oficial (prazo/custo de aprovação na Meta), base legal da reativação (F3) e do WhatsApp (F4), política de opt-out.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Formulário emite POST + API suporta os 3 testes | Dossiê completo, F2 liberada para iniciar quando credenciais chegarem | — |
| Limite | Formulário só envia e-mail | Decisão registrada: ponte de e-mail vs. ajuste de formulário (dono: consultora + cliente) | F2 não inicia sem essa decisão |
| Falha | API não suporta prazo em minutos | Limitação registrada + contorno proposto no dossiê | F2 adapta o desenho do SLA |

## Checklist de execução

- [ ] URL do formulário obtida e inspecionada (método, campos vs. RN-02, origem)
- [ ] Smoke test da API executado: tarefa em minutos, tag, busca CNPJ/e-mail (com prova)
- [ ] Mapeamento de campos formulário → Agendor completo
- [ ] Contrato de webhook desenhado (gatilho, payload, erro, duplicidade)
- [ ] Checklist de credenciais/permissões enviado ao cliente
- [ ] Decisão WhatsApp oficial documentada (prazo/custo Meta)
- [ ] Base legal + opt-out da reativação (F3) e do WhatsApp (F4) documentados

## Critérios de aceite

- [ ] **CA-1-04:** mapeamento de campos formulário→Agendor completo e revisado (revisão: cliente valida os campos do formulário; consultora valida os campos do Agendor — prova: validação registrada no dossiê), incluindo verificação da capacidade do formulário (POST/webhook vs. e-mail; captura de origem) e smoke test da API do Agendor (provas de leitura: busca por CNPJ/e-mail + prova negativa de produção; provas de escrita se o token estiver disponível — senão, CA-2-00 na F2).
- [ ] **CA-1-05:** contrato de webhook desenhado (campos, gatilho, tratamento de erro) sem implementação; decisão de ponte de e-mail vs. ajuste de formulário registrada se o formulário não emitir POST.
- [ ] **CA-1-05a:** dossiê único de integração existe com as 6 seções completas e provas anexadas.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Sem dossiê: F2 começaria com hipóteses | Verificar inexistência das evidências (formulário, API, mapeamento) | Falha: capacidade não comprovada | Registro da verificação (nota no dossiê vazio) |
| GREEN | Evidências coletadas | Executar smoke test + inspeção do formulário | 3 provas de API + 1 laudo do formulário | Logs/prints no dossiê |
| REFACTOR/REGRESSÃO | Revisão do dossiê | Conferir as 6 seções completas e decisões registradas | Dossiê aprovado pela consultora | Documento final |
| REFACTOR/REGRESSÃO | Sanitização de evidências | Revisar todos os prints/logs antes de anexar | Nenhum print contém CNPJ/e-mail/nome de cliente real (mascarar ou usar fixtures) | Checklist de sanitização assinado |

**Dados/fixtures:** negócio/empresa de TESTE no Agendor (nunca dados reais); URL real do formulário; documentação pública da API Agendor e da Meta.
**Caminhos de erro obrigatórios:** formulário sem POST (decisão registrada), API sem suporte a minutos (limitação + contorno), credenciais negadas pelo plano (registrar e escalar ao cliente), smoke test falhando (registrar e reavaliar degrau).
**Quando não houver código:** smoke test via curl/ferramenta de requisição HTTP com prints — endpoints conforme documentação pública da API do Agendor (consultar em developer.agendor.com.br no momento da execução; a SPEC não fixa URL/payload porque a versão da API pode mudar — o dossiê registra os comandos exatos usados); inspeção do formulário via código-fonte da página (método do <form>, campos, hidden fields de origem).

**Evidência exigida:** dossiê de integração com logs/prints do smoke test e laudo do formulário.

## Tasks vinculadas

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| — | *preenchido por gerar-tasks* | | | | | | | |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |
