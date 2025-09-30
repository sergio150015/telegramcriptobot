# 1. Introdução

Este documento descreve os principais casos de uso do Bot Cripto
Telegram. Cada caso de uso define como o usuário interage com o sistema
e como os fluxos de dados são processados pelos componentes (n8n, Redis,
Supabase, APIs externas).

# 2. Caso de Uso: Consulta de Preço

\*\*Ator:\*\* Usuário (Telegram)\
\*\*Objetivo:\*\* Consultar o preço atual de um token em BRL\
\*\*Pré-condição:\*\* Bot ativo, símbolo válido\
\*\*Fluxo principal:\*\*\
1. Usuário envia /preco BTC no Telegram.\
2. N8N recebe via Telegram Trigger e envia ao Agente IA.\
3. Agente consulta Redis (px:spot:BTCBRL).\
4. Se miss, consulta Binance e atualiza Redis.\
5. Resposta formatada enviada ao usuário.\
\*\*Fluxo alternativo:\*\* símbolo inválido → bot responde "moeda não
suportada".

# 3. Caso de Uso: Criar Alerta de Preço

\*\*Ator:\*\* Usuário (Telegram)\
\*\*Objetivo:\*\* Criar alerta personalizado para preço\
\*\*Pré-condição:\*\* Usuário cadastrado\
\*\*Fluxo principal:\*\*\
1. Usuário envia /alerta add BTC abaixo 250000.\
2. N8N recebe, valida e grava no Supabase (tabela alerts).\
3. Workflow de monitoramento verifica alertas a cada 1--2min.\
4. Quando condição é atendida, bot envia alerta no Telegram.\
\*\*Fluxo alternativo:\*\* valor inválido → resposta de erro ao usuário.

# 4. Caso de Uso: Registro de Trade (Compra/Venda)

\*\*Ator:\*\* Usuário (Telegram)\
\*\*Objetivo:\*\* Registrar compra ou venda no portfólio\
\*\*Pré-condição:\*\* Usuário cadastrado\
\*\*Fluxo principal:\*\*\
1. Usuário envia /comprar BTC 0.05 a 248000.\
2. N8N valida dados e insere registro em Supabase (tabela trades).\
3. Bot confirma registro ao usuário.\
\*\*Fluxo alternativo:\*\* dados incompletos → bot solicita correção.

# 5. Caso de Uso: Consulta de Portfólio e PnL

\*\*Ator:\*\* Usuário (Telegram)\
\*\*Objetivo:\*\* Visualizar posições atuais e PnL\
\*\*Pré-condição:\*\* Existência de trades cadastrados\
\*\*Fluxo principal:\*\*\
1. Usuário envia /posicao ou /pnl.\
2. N8N consulta trades no Supabase.\
3. N8N consulta preços atuais (Redis/Binance).\
4. Supabase calcula posição e PnL via funções SQL.\
5. Bot retorna resumo de portfólio ao usuário.

# 6. Caso de Uso: Consulta de Notícias

\*\*Ator:\*\* Usuário (Telegram)\
\*\*Objetivo:\*\* Receber últimas notícias sobre criptomoedas\
\*\*Pré-condição:\*\* Bot ativo\
\*\*Fluxo principal:\*\*\
1. Usuário envia /news 5.\
2. N8N consulta Redis (news:top).\
3. Se miss, lê RSS Feed, formata e atualiza cache.\
4. Bot retorna lista das 5 últimas notícias com link.

# 7. Caso de Uso: Interação em Linguagem Natural

\*\*Ator:\*\* Usuário (Telegram)\
\*\*Objetivo:\*\* Usar comandos naturais com auxílio da IA\
\*\*Pré-condição:\*\* Agente IA ativo (LangChain + MCP)\
\*\*Fluxo principal:\*\*\
1. Usuário envia: "me avisa se o Solana cair abaixo de 150 reais e me
mostra o preço agora".\
2. N8N encaminha mensagem ao agente IA.\
3. IA decompõe intenção em duas ações: create_alert(SOL, abaixo, 150) +
get_price(SOL).\
4. IA chama ferramentas via workflows e retorna resultado combinado.

# 8. Caso de Uso: Tratamento de Erros

\*\*Ator:\*\* Sistema (n8n)\
\*\*Objetivo:\*\* Registrar e notificar erros operacionais\
\*\*Pré-condição:\*\* Workflow ativo\
\*\*Fluxo principal:\*\*\
1. Workflow falha em consultar API externa.\
2. WF_Error_Handler captura erro e registra em ErrorState (Supabase).\
3. Notificação é enviada ao operador no Telegram.\
4. Operador analisa log e executa medidas corretivas.
