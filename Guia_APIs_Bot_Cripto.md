# 1. Escopo

Este guia documenta como o bot integra Binance (Spot), RSS, OpenAI,
Supabase/PostgREST, Telegram e Redis, com exemplos práticos para uso no
n8n.

# 2. Binance Spot API

Base: https://api.binance.com

\- exchangeInfo: GET /api/v3/exchangeInfo (cache Redis: meta:symbols,
TTL 6--12h)

\- 24h ticker: GET /api/v3/ticker/24hr?symbol=\<SYMBOL\> (lastPrice,
priceChangePercent, volume)

\- price simples: GET /api/v3/ticker/price?symbol=\<SYMBOL\>

BRL strategy: usar \<ASSET\>BRL; se não existir, \<ASSET\>USDT ×
USDTBRL.

Caching Redis: px:spot:\<SYMBOL\> (TTL 5--10s), px:conv:USDTBRL (TTL
30--60s).

Erros 429/5xx: backoff exponencial (1s,2s,4s; máx 3 tentativas).

# 3. RSS (Notícias)

Fontes: CoinDesk, CoinTelegraph, etc. via RSS público.

n8n: RSS Read → Function (top N) → Telegram. Cache: news:top (TTL
120--300s).

# 4. OpenAI (Agente/Curadoria)

Auth: Authorization: Bearer \<API_KEY\>. Usar agente com ferramentas:
get_price, create_alert, record_trade, get_position, get_news.

Registrar custo estimado por execução em ApiUsage.

# 5. Supabase (PostgREST + Postgres)

REST base: https://\<project\>.supabase.co/rest/v1

Headers: apikey: \<service_role\>, Authorization: Bearer
\<service_role\>, Prefer: return=representation

Operações: alerts/trades/bot_log/error_state via REST; SQL avançado via
nó Postgres (pooler).

Idempotência: Prefer: resolution=merge-duplicates ou chaves naturais
(trades: userId+symbol+ts).

# 6. Telegram Bot API (via n8n)

Usar Telegram Trigger (webhook) + Telegram (sendMessage). Whitelist de
chat_id, rate \~30 msg/s.

# 7. Redis (HTTP/Upstash ou Bridge)

Operações: GET, SETEX, DEL. Chaves: px:spot:\<SYMBOL\>, px:conv:USDTBRL,
meta:symbols, news:top.

Padrão cache-aside: tenta cache → miss chama API → grava SETEX.

# 8. Tratamento de Erros & Retries

Timeouts 5--8s; 3 tentativas com backoff; degradar para cache quando API
lenta; logar requestId, status e duração em BotLog.

# 9. Segurança

Chaves no n8n Vault; Binance read-only para saldo/trades; TLS/HTTPS;
sanitizar inputs antes de SQL.

# 10. Exemplos (HTTP Request)

Binance: GET https://api.binance.com/api/v3/ticker/24hr?symbol=BTCBRL

Supabase (create alert): POST
https://\<project\>.supabase.co/rest/v1/alerts + headers apikey/Auth +
Prefer: return=representation

Upstash SETEX: POST
https://\<UPSTASH\>/setex/px:spot:BTCBRL/10/250000.00
