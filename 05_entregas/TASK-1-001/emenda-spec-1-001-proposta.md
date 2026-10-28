# Proposta de emenda — SPEC-1-001 (fila manual)

**Origem do sinal:** verificação de fechamento da TASK-1-001, 2026-10-28
**Solicitante:** Alexandre (champion)
**Decisão:** consultora Kim (Adapta Native) — **emenda não é autoaprovada**
**Status:** proposta, aguardando validação

## Por que a emenda é necessária

A SPEC-1-001 foi escrita para **planilha/kanban (Google Sheets)** e veda integração na F1. A implementação construída e aprovada pelo champion é uma **aplicação web no Skip Cloud** (PocketBase), com a mesma estrutura de dados. Duas consequências:

1. CA-1-01c e CA-1-01d descrevem recursos que só existem no Sheets — "abrir o link da planilha de conta não autorizada" e "restaurar versão anterior via histórico do Sheets".
2. O "Degrau da solução" justifica o Sheets pelo volume; a aplicação já existe e está em uso, então a justificativa deixou de valer.

## Emenda proposta

### Degrau da solução

> **De:** construção mínima — planilha/kanban estruturado (Google Sheets) porque a F1 veda integração e o volume atual não justifica sistema próprio ainda.
>
> **Para:** aplicação web dedicada (Skip Cloud / PocketBase), entregue como tela "Fila Manual" com coleção protegida `fila_leads`. A restrição da F1 permanece: **sem integração automática com Agendor** e **sem disparo automático de e-mail**; a captação continua manual. O uso de aplicação em vez de planilha foi decidido com o champion após a geração da SPEC.

### CA-1-01c

> **De:** prova negativa de acesso: abertura da planilha a partir de conta NÃO autorizada falha ou exige solicitação de acesso.
>
> **Para:** prova negativa de acesso em duas frentes: (a) sem autenticação, a API não devolve nenhum registro da fila e não permite leitura, criação ou alteração; (b) sem a chave de convite o cadastro é recusado, de modo que não existe conta "não autorizada" com acesso. Complemento de segregação (RNF-03): a fila deve distinguir papéis — **só leitura** × **editor** — e impedir que uma conta apague registros de outra sem permissão explícita; resultado registrado no dossiê.

### CA-1-01d

> **De:** prova de restauração: versão anterior da planilha restaurada via histórico do Sheets com colunas-chave íntegras.
>
> **Para:** prova de recuperação da fonte única de verdade: (a) export completo da fila em CSV com as 15 colunas, gerado pela própria tela; (b) reimportação do CSV em ambiente de teste reproduzindo os registros com as colunas-chave íntegras; (c) política de backup do provedor registrada por escrito (frequência, responsável, procedimento). Não há restauração ponto-no-tempo disponível ao cliente — a recuperação se dá por export + recriação a partir do arquivo.

## Ajustes de checklist que acompanham

- "Permissões da planilha restritas: compartilhamento por convite apenas" → "Acesso restrito a contas criadas com chave de convite; chave em cofre de segredos e rotacionada; papéis só-leitura × editor definidos".
- "Export semanal + prova de restauração via histórico do Sheets" → "Export da fila automatizado ou agendado + reimportação comprovada em ambiente de teste".

## O que NÃO muda

Estágios, tags ICP, campos obrigatórios e a regra "data de origem = data de submissão" permanecem idênticos. A proibição de integração e de disparo automático na F1 permanece. A fila continua sendo a fonte única de verdade da F1.

## Decisão necessária

Aprovar a emenda, ajustar a redação ou determinar a volta para Google Sheets. Sem essa decisão a TASK-1-001 permanece **bloqueada**.
