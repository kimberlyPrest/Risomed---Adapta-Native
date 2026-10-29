## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Fila inexistente: coleção nova sem estrutura | Conferir campos obrigatórios e restrições ausentes | Falha: campos/validação não existem | Print da coleção vazia |
| GREEN | Estrutura mínima operando | Criar 3 leads de teste (1 ICP, 1 Fora ICP, 1 Incompleto) com validação ativa | Registros aceitos, tags restritas à lista, estágios válidos | Print da fila com 3 leads |
| REFACTOR/REGRESSÃO | Uso real por 1 semana | Auditoria semanal: cruzar e-mails da semana × registros da fila | 100% dos leads presentes com tag e próxima ação | Registro de auditoria |
| REFACTOR/REGRESSÃO | Prova negativa de acesso (CA-1-01c) | Requisições sem token e cadastro sem chave de convite; tentativa de forjar `created_by` | Leitura vazia, escrita recusada, cadastro recusado, autoria não forjável | Log das requisições com códigos HTTP |
| REFACTOR/REGRESSÃO | Prova de restauração (CA-1-01d) | Criar sonda → exportar → apagar → restaurar do arquivo → conferir campo a campo | Campos íntegros, sem duplicata | Log do script de prova |
| REFACTOR/REGRESSÃO | Segregação por papel (CA-1-01e) | Com 2 contas: só-leitura tenta criar/editar/apagar; editor tenta apagar registro de outro autor | Operações recusadas pelo servidor | Log das requisições (códigos HTTP) por papel |

**Dados/fixtures:** 3 leads de teste (empresa real fictícia: 45 vidas Campinas = ICP; 5 vidas Recife = Fora ICP; lead sem nº de vidas = Incompleto) + 2 contas (champion e conta de teste descartável).