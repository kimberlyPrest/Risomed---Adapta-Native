# Changelog — Risomed · Adapta Native

Registro das ações executadas no projeto, em ordem cronológica.
Formato: `- AAAA-MM-DD · [autor] · <ação>: <resumo e evidência>`

- 2026-09-10 · [Kim] · Escopo definitivo aprovado: PRD, matriz de rastreabilidade, 5 fases e gates D7 em `02-Escopo-Definitivo.md`; check-escopo APROVADO.
- 2026-09-10 · [Kim] · SPECs da Fase 1 geradas e revisadas por painel de 4 lentes (6 SPECs + matriz-specs-fases).
- 2026-09-10 · [Alexandre] · TASK-1-001 implementada no Skip Cloud (projeto "Jornada Comercial Risomed", id 57599): coleção `fila_leads` + tela Fila Manual com os campos da SPEC, tags ICP, estágios, próxima ação com data e motivo de perda obrigatório.
- 2026-10-12 · [Alexandre] · Correção de segurança aplicada (v0.0.20–0.0.24): autocadastro fechado com chave de convite, `created_by` honesto, normalização de datas. Provas P1–P8 executadas.
- 2026-10-22 · [Alexandre] · Reteste humano da TASK-1-001 declarado APROVADO pelo champion.
- 2026-10-22 · [Alexandre] · Fechamento formal bloqueado: repositório sem os arquivos canônicos de fase/estado/changelog e SPEC-1-001 divergente da implementação. Nenhum arquivo do projeto alterado.
- 2026-10-28 · [Alexandre] · **Registro criado**: `STATUS.md`, `changelog.md`, `04_fase-atual/fase.md`, `.adapta-cliente/estado-atual.md`, `05_entregas/` e `06_notas/` — resolve a pendência de registro apontada em 22/10.
- 2026-10-28 · [Alexandre] · Verificação independente de fechamento executada ponta a ponta no sistema em produção. Evidência em `05_entregas/TASK-1-001/verificacao-2026-10-28.md`. Resultado: **NÃO PRONTA**.
- 2026-10-28 · [Alexandre] · CA-1-01b PASSOU: tag ICP e estágio inválidos rejeitados pelo servidor (HTTP 400); campos obrigatórios exigidos.
- 2026-10-28 · [Alexandre] · CA-1-01c PASSOU: sem autenticação a fila devolve 0 registros e não permite escrita; sem a chave de convite o cadastro é recusado; `created_by` não pode ser forjado.
- 2026-10-28 · [Alexandre] · **DÚVIDA (segurança)** — dentro da fila não há separação por usuário: conta criada com a chave de convite lista, altera e apaga leads de outra pessoa (prova isolada com registro-sonda: DELETE HTTP 204). Não reprova a CA-1-01c como escrita, mas exige segregação por papel antes do uso com dados reais. Ver `06_notas/aprendizado-continuo/AP-2026-10-28-rls-fila-leads.md`.
- 2026-10-28 · [Alexandre] · CA-1-01d NÃO SATISFATÓRIO: export CSV existe na tela, mas não há backup nem restauração ponto-no-tempo acessível ao cliente (`GET /api/backups` → 403). Critério não é fechável na redação atual.
- 2026-10-28 · [Alexandre] · **DÚVIDA (escopo)** — divergência de plataforma: SPEC-1-001 determina Google Sheets e veda integração na F1; a implementação é aplicação Skip. Proposta de emenda redigida em `05_entregas/TASK-1-001/emenda-spec-1-001-proposta.md`, aguardando a consultora.
- 2026-10-28 · [Alexandre] · **Risco residual** — a conta de teste `probe.qa.1793223729@example.com` criada na prova negativa não pôde ser removida: exclusão e troca de senha retornam 403 ("Only superusers can perform this action"). Ação necessária por superusuário.
- 2026-10-28 · [Alexandre] · Integridade dos dados: o lead "Academia Corpo Forte" foi apagado pela prova de exclusão e recriado com todos os campos (novo id `e7jmfg4tzfzf0x3`); "Madeira Madeira" intacto; registros-sonda removidos.
