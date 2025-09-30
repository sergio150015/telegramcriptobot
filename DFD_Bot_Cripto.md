# 1. Introdução

Este documento apresenta o Diagrama de Fluxo de Dados (DFD) do Bot
Cripto Telegram. O objetivo é visualizar como os dados circulam entre
entidades externas, processos internos e armazenamentos. São descritos
os níveis 0 e 1, seguidos de uma representação em Mermaid como anexo
técnico.

# 2. DFD -- Nível 0

\*\*Entidades externas:\*\*\
- Usuário (Telegram)\
- APIs externas (Binance, OpenAI, RSS Feeds)\
\
\*\*Processos:\*\*\
- Bot Cripto (n8n Workflows)\
\
\*\*Armazenamentos:\*\*\
- Supabase (Postgres)\
- Redis (Cache)\
\
\*\*Fluxos principais:\*\*\
1. Usuário envia comando ao Bot (via Telegram).\
2. Bot processa comando e consulta Redis e/ou Supabase.\
3. Se necessário, Bot consulta APIs externas (Binance, OpenAI, RSS).\
4. Resposta é retornada ao Usuário via Telegram.

# 3. DFD -- Nível 1

\*\*Processos detalhados:\*\*\
- WF_Bot_Principal: recebe comandos, roteia e responde.\
- WF_Monitor_Alertas: verifica alertas ativos, consulta preços e dispara
notificações.\
- WF_Error_Handler: captura e registra falhas.\
- WF_News: coleta e entrega notícias.\
\
\*\*Fluxos de dados detalhados:\*\*\
- Usuário → Telegram → WF_Bot_Principal (/preco, /alerta, /posicao,
/news).\
- WF_Bot_Principal → Redis: consulta/atualiza preços e notícias.\
- WF_Bot_Principal → Supabase: grava alertas, trades, logs.\
- WF_Bot_Principal → Binance/OpenAI/RSS: consulta dados externos.\
- WF_Monitor_Alertas → Supabase: lê alertas ativos.\
- WF_Monitor_Alertas → Binance/Redis: lê preços.\
- WF_Monitor_Alertas → Usuário (Telegram): dispara alerta quando
condição atendida.

# 4. Anexo Técnico -- Mermaid

\`\`\`mermaid\
flowchart TD\
User\[Usuário (Telegram)\] \--\>\|/preco, /alerta, /news\|
WF_Bot\[WF_Bot_Principal\]\
WF_Bot \--\> Redis\[(Redis Cache)\]\
WF_Bot \--\> Supabase\[(Supabase Postgres)\]\
WF_Bot \--\> Binance\[Binance API\]\
WF_Bot \--\> OpenAI\[OpenAI API\]\
WF_Bot \--\> RSS\[RSS Feeds\]\
WF_Bot \--\>\|Resposta\| User\
\
Cron\[Cron Job\] \--\> WF_Alerts\[WF_Monitor_Alertas\]\
WF_Alerts \--\> Supabase\
WF_Alerts \--\> Redis\
WF_Alerts \--\> Binance\
WF_Alerts \--\>\|Notificação\| User\
\
WF_Bot \--\> WF_Error\[WF_Error_Handler\]\
WF_Alerts \--\> WF_Error\
WF_Error \--\> Supabase\
WF_Error \--\>\|Alerta de falha\| User\
\`\`\`

# 5. Conclusão

O DFD permite visualizar de forma clara como as informações circulam
entre os componentes do Bot Cripto Telegram. O nível 0 mostra a visão
macro, enquanto o nível 1 detalha os principais processos internos do
n8n. O anexo em Mermaid permite renderização visual complementar.
