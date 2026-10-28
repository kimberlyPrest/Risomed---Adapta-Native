# Backup e restauração — fila de leads

Proteção da fonte única de verdade da Fase 1 (coleção `fila_leads`, projeto Skip 57599).

**Resolve:** CA-1-01d — prova de restauração da fonte única de verdade.

## Por que existe

A fila é a fonte única de verdade da F1. Antes deste script não havia backup nem forma de recuperar um lead apagado: `GET /api/backups` responde 403 e a plataforma não oferece restauração ponto-no-tempo ao cliente. Um lead apagado por engano era perda definitiva.

## Scripts

Localização no workspace do agente: `scripts/jornada-backup/`.

| Comando | O que faz |
|---|---|
| `./backup_diario.sh` | Exporta, verifica as 15 colunas e aplica retenção de 90 dias. É o que roda na automação das 22h |
| `python3 backup_fila.py export` | Gera `backups/fila-leads-<data>.csv` (15 colunas, `;`, UTF-8 com BOM — abre no Excel) e o `.json` com todos os campos técnicos |
| `python3 backup_fila.py verify <csv>` | Confere que as 15 colunas da SPEC estão presentes |
| `python3 backup_fila.py restore <csv> [--filtro=texto] [--dry-run]` | Recria registros a partir do CSV. Com `--filtro`, restaura só as linhas cujo nome de empresa contenha o texto. Pula registros que já existem (mesma empresa + e-mail), para não duplicar |
| `./prova_restauracao.sh` | Prova completa do CA-1-01d: cria sonda → exporta → apaga → restaura → confere campo a campo → limpa |

## Prova executada em 2026-10-28

```
=== 1. criar registro-sonda com os 15 campos ===
  PASSOU  sonda criada
=== 2. exportar a fila ===
  PASSOU  sonda presente no CSV exportado
=== 3. apagar a sonda (simula a perda) ===
  PASSOU  sonda apagada (HTTP 204)
  PASSOU  confirmado: registro nao existe mais (HTTP 404)
=== 4. restaurar a partir do CSV ===
  filtro: 1 linha(s) selecionada(s) — restaurados: 1 | pulados: 0 | falhas: 0
=== 5. conferir campo a campo ===
  PASSOU  empresa, solicitante, email, telefone, cnpj, vidas, cidade,
          origem, tag_icp, estagio, resultado_contato, proxima_acao
=== 6. limpar residuo da prova ===
  removido -> 204
=== RESULTADO: PROVA PASSOU (CA-1-01d) ===
```

## Automação

Job `Backup fila de leads` (id `cc627d297a64934c`), todo dia às 22:00 (America/Sao_Paulo). Se o export falhar ou vier vazio, o script sai com código de erro e o job reporta.

## Limitações honestas

- **Não é restauração ponto-no-tempo.** Recupera-se o que estava no último export. Um lead criado e apagado entre dois backups não volta.
- **O id original não é preservado.** O registro restaurado recebe id novo; todos os campos de negócio voltam idênticos.
- **A credencial fica em `credentials.json`** (permissão 600, fora do repositório git). Se a senha do usuário mudar, atualizar esse arquivo.
- **Rate limit:** a API limita logins repetidos (HTTP 429). O script espera e repete até 5 vezes.

## Pendência que este script NÃO resolve

A segregação de acesso: qualquer conta criada com a chave de convite lê, altera e apaga todos os leads. Isso exige alterar as regras da coleção no Skip Cloud — não é possível pela API pública com conta de usuário.
