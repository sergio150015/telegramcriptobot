Funções e views para cálculo de posições, custo médio e PnL.

# 1) Posição e Custo Médio (CMA)

CREATE OR REPLACE FUNCTION fn_positions_cma(p_user uuid)\
RETURNS TABLE(symbol text, qty_net numeric, avg_cost_brl numeric) AS
\$\$\
WITH ops AS (\
SELECT symbol,\
SUM(CASE WHEN side=\'buy\' THEN qty ELSE -qty END) AS qty_net,\
SUM(CASE WHEN side=\'buy\' THEN qty\*price_brl + fee_brl ELSE 0 END) AS
buy_cost\
FROM trades\
WHERE user_id = p_user\
GROUP BY symbol\
)\
SELECT symbol,\
qty_net,\
CASE WHEN qty_net \> 0\
THEN buy_cost / NULLIF( (SELECT SUM(qty) FROM trades t WHERE
t.user_id=p_user AND t.symbol=ops.symbol AND t.side=\'buy\'), 0)\
ELSE 0 END AS avg_cost_brl\
FROM ops;\
\$\$ LANGUAGE sql STABLE;

# 2) View de Posições Correntes

CREATE OR REPLACE VIEW v_positions_current AS\
SELECT p.symbol, p.qty_net, p.avg_cost_brl\
FROM fn_positions_cma((SELECT id FROM users LIMIT 1)) p;

# 3) PnL Não Realizado (Snapshot de Preços)

CREATE OR REPLACE FUNCTION fn_pnl_cma(p_user uuid, p_prices jsonb)\
RETURNS TABLE(symbol text, qty numeric, avg_cost_brl numeric,
mkt_price_brl numeric, pnl_unrealized numeric) AS \$\$\
WITH pos AS (\
SELECT \* FROM fn_positions_cma(p_user)\
)\
SELECT\
pos.symbol,\
pos.qty_net,\
pos.avg_cost_brl,\
(p_prices -\>\> pos.symbol)::numeric AS mkt_price_brl,\
( (p_prices -\>\> pos.symbol)::numeric - pos.avg_cost_brl ) \*
pos.qty_net AS pnl_unrealized\
FROM pos;\
\$\$ LANGUAGE sql STABLE;

# 4) Observações

\- As funções usam custo médio móvel (CMA) para simplicidade.\
- Para FIFO, implementar função específica (p.ex. fn_pnl_fifo)
futuramente.\
- Todos os valores monetários em BRL (numeric(18,2)).
