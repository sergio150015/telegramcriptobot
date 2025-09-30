# 1. Introdução

Este checklist de deploy garante que todos os passos críticos sejam
verificados antes de colocar o Bot Cripto Telegram em produção. Ele
serve como guia rápido para reduzir riscos de falhas e garantir
estabilidade.

# 2. Preparação do Ambiente

\- \[ \] Instância N8N provisionada (Docker, VPS ou cloud provider).\
- \[ \] Projeto Supabase criado e migrado com schema Prisma.\
- \[ \] Redis provisionado (Upstash ou self-hosted) e acessível via
HTTP/TLS.\
- \[ \] Variáveis de ambiente configuradas (DATABASE_URL, REDIS_URL,
API_KEYS).\
- \[ \] N8N Vault configurado para credenciais sensíveis (Binance,
OpenAI, Telegram, Supabase).

# 3. Configuração do Banco de Dados

\- \[ \] Executar migrações Prisma no Supabase/Postgres.\
- \[ \] Criar funções auxiliares (fn_positions_cma, fn_pnl_cma).\
- \[ \] Criar views de posição atual (v_positions_current).\
- \[ \] Validar índices nas tabelas (alerts, trades, bot_log).\
- \[ \] Testar consultas diretas no Supabase (via SQL Editor).

# 4. Configuração dos Workflows N8N

\- \[ \] WF_Bot_Principal configurado com Telegram Trigger e roteamento
de comandos.\
- \[ \] WF_Monitor_Alertas configurado com Cron + Supabase + Binance.\
- \[ \] WF_Error_Handler ativo, registrando em ErrorState e notificando
no Telegram.\
- \[ \] Sub-workflows de /preco, /alerta, /news, /comprar, /vender,
/posicao, /pnl implementados.\
- \[ \] Logs configurados para BotLog (via Supabase).

# 5. Testes Finais (Go/No-Go)

\- \[ \] Testar /preco BTC (resposta em \<3s).\
- \[ \] Testar criação e disparo de alerta.\
- \[ \] Testar registro de trade e consulta de posição.\
- \[ \] Testar /news com cache Redis.\
- \[ \] Testar comando em linguagem natural via agente IA.\
- \[ \] Simular falha de API externa e validar WF_Error_Handler.

# 6. Monitoramento Inicial

\- \[ \] Configurar UptimeRobot para webhook do Telegram.\
- \[ \] Configurar alertas de erro (taxa de falha \>5%).\
- \[ \] Validar logging no Supabase (BotLog, ErrorState).\
- \[ \] Validar consumo de APIs em ApiUsage.

# 7. Aprovação

\- \[ \] Todos os itens acima checados.\
- \[ \] Operador responsável valida checklist.\
- \[ \] Bot autorizado a entrar em produção.
