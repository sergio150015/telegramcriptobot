# 1. Introdução

Este documento consolida a modelagem de dados do Bot Cripto Telegram.
Inclui tabelas e funções no Supabase/Postgres, bem como a estratégia de
armazenamento em Redis.

# 2. Estrutura no Supabase / PostgreSQL

\### Tabelas Principais:

\- users\
- id (uuid, pk)\
- chat_id (bigint, único)\
- created_at (timestamp)\
- updated_at (timestamp)\
\
- alerts\
- id (uuid, pk)\
- user_id (fk → users.id)\
- symbol (text)\
- direction (enum: above/below)\
- target_brl (numeric)\
- created_at (timestamp)\
- triggered_at (timestamp, nullable)\
\
- trades\
- id (uuid, pk)\
- user_id (fk → users.id)\
- symbol (text)\
- side (enum: buy/sell)\
- qty (numeric)\
- price_brl (numeric)\
- fee_brl (numeric)\
- created_at (timestamp)\
\
- bot_log\
- id (uuid, pk)\
- user_id (fk → users.id, nullable)\
- action (text)\
- payload (jsonb)\
- created_at (timestamp)\
\
- error_state\
- id (uuid, pk)\
- workflow (text)\
- error_message (text)\
- payload (jsonb)\
- created_at (timestamp)\
\
- api_usage\
- id (uuid, pk)\
- api_name (text)\
- call_count (int)\
- last_called_at (timestamp)

\### Funções Auxiliares:

\- fn_positions_cma(user_id): calcula posições e custo médio.\
- fn_pnl_cma(user_id): calcula PnL não realizado.\
- v_positions_current: view consolidada de posições atuais.

# 3. Estrutura no Redis

\### Chaves e TTLs:

\- px:spot:\<SYMBOL\> → preço spot, TTL 5--10s\
- px:conv:USDTBRL → conversão BRL, TTL 30--60s\
- meta:symbols → lista de símbolos Binance, TTL 6--12h\
- news:top → últimas notícias RSS, TTL 120--300s

\### Estratégia:

\- Padrão cache-aside: consultar Redis → se não existir, buscar API →
atualizar Redis.\
- TTLs ajustados para equilibrar frescor dos dados e economia de
chamadas de API.\
- Uso preferencial de Redis para preços e notícias, reduzindo custo e
latência.

# 4. Conclusão

Com esta modelagem, o Supabase/Postgres armazena dados persistentes e
históricos, enquanto o Redis atua como cache de alta performance para
dados temporais (preços e notícias). Essa combinação garante equilíbrio
entre confiabilidade, velocidade e custo.
