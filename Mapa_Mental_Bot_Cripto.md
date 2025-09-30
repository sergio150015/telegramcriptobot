# 1. Introdução

Este documento apresenta um Mapa Mental do Bot Cripto Telegram. O
objetivo é organizar de forma hierárquica as principais áreas do
projeto, fornecendo uma visão geral clara e rápida.

# 2. Estrutura do Mapa Mental

Bot Cripto Telegram\
│\
├── Funcionalidades\
│ ├── Consulta de Preço (/preco)\
│ ├── Alertas de Preço (/alerta)\
│ ├── Registro de Trades (/comprar, /vender)\
│ ├── Portfólio & PnL (/posicao, /pnl)\
│ └── Notícias (/news)\
│\
├── Infraestrutura\
│ ├── N8N Workflows\
│ │ ├── WF_Bot_Principal\
│ │ ├── WF_Monitor_Alertas\
│ │ └── WF_Error_Handler\
│ ├── Supabase (Postgres)\
│ │ ├── Users\
│ │ ├── Alerts\
│ │ ├── Trades\
│ │ └── Logs & Erros\
│ └── Redis (Cache)\
│ ├── Preços (px:spot:\*)\
│ ├── Conversão USDTBRL\
│ ├── Símbolos (meta:symbols)\
│ └── Notícias (news:top)\
│\
├── Integrações Externas\
│ ├── Binance API\
│ ├── Telegram Bot API\
│ ├── OpenAI (LangChain/MCP)\
│ ├── RSS Feeds\
│ └── TAAPI.io (futuro)\
│\
├── Segurança\
│ ├── N8N Vault (credenciais)\
│ ├── API Keys read-only\
│ ├── Webhook protegido\
│ └── Backups & Recovery\
│\
├── Operação & Monitoramento\
│ ├── Logs (BotLog, ErrorState)\
│ ├── ApiUsage (limites)\
│ ├── UptimeRobot (webhook)\
│ ├── Monitoramento Redis\
│ └── Relatórios periódicos\
│\
└── Extensões Futuras\
├── Multiusuário\
├── Dashboard Web\
├── Análises Técnicas (TAAPI)\
└── Escalabilidade com RabbitMQ

# 3. Conclusão

O mapa mental serve como visão global do projeto, mostrando de forma
organizada as funcionalidades, infraestrutura, integrações, segurança,
operação e futuras extensões do Bot Cripto Telegram.
