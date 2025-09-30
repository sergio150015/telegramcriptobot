# 1. Introdução

Este sumário executivo apresenta uma visão consolidada do projeto Bot
Cripto Telegram, incluindo objetivos, escopo, arquitetura, riscos e
próximos passos.

# 2. Objetivos do Projeto

\- Criar um bot no Telegram para uso pessoal, com funções principais:\
- Consulta de preços em tempo real.\
- Criação e monitoramento de alertas de preço.\
- Registro e consulta de trades (portfólio real, não simulado).\
- Cálculo de posições e PnL (custo médio móvel).\
- Consulta de notícias do mercado cripto.\
- Arquitetura modular, com espaço para extensões futuras (multiusuário,
análise técnica, dashboard web).

# 3. Escopo do Projeto

\- \*\*Funcionalidades incluídas (MVP):\*\*\
- Preço em tempo real (/preco).\
- Alertas configuráveis (/alerta).\
- Registro de operações (/comprar, /vender).\
- Consulta de portfólio e PnL (/posicao, /pnl).\
- Consulta de notícias (/news).\
- \*\*Futuro:\*\*\
- Análises técnicas (TAAPI.io).\
- Dashboard web.\
- Multiusuário.\
- Escalabilidade com RabbitMQ.

# 4. Arquitetura do Sistema

\- Orquestração: n8n.\
- Banco de dados: Supabase/Postgres.\
- Cache: Redis.\
- APIs externas: Binance, OpenAI, RSS, Telegram.\
- Agente IA: LangChain + MCP.

# 5. Principais Riscos e Mitigações

\- Dependência de APIs externas → Redis e Supabase como fallback.\
- Rate limiting de APIs → monitoramento ApiUsage e TTLs.\
- Erros de IA → logs em ErrorState e ajuste de prompts.\
- Falhas de infraestrutura → backup no Supabase, workflows exportados.\
- Segurança → Vault de credenciais, chaves read-only, webhook protegido.

# 6. Documentação Produzida

\- PDR, Prisma, SQL auxiliares, Diagramas, Guia de DB, Runbook, Matriz
de Riscos,\
Plano de Monitoramento, Plano de Segurança, Guia de APIs, Casos de Uso,\
Checklist de Deploy, DFD, Mapa Mental (este documento).

# 7. Próximos Passos

\- Finalizar Plano de Continuidade de Negócios.\
- Consolidar Guia de Workflows do n8n.\
- Testes integrados no staging.\
- Implantação controlada e monitorada.

# 8. Conclusão

O projeto já possui base sólida de requisitos, arquitetura e
documentação. Com os próximos passos, estará pronto para testes finais e
entrada em produção.
