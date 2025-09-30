# 1. Introdução

Esta matriz de riscos identifica os principais riscos associados ao Bot
Cripto Telegram, bem como suas probabilidades, impactos e estratégias de
mitigação. Ela serve como guia para antecipar problemas e garantir maior
resiliência operacional.

# 2. Matriz de Riscos

\*\*Risco:\*\* Falha ou indisponibilidade de APIs externas (Binance,
RSS, OpenAI)\
- Probabilidade: Alta\
- Impacto: Alto\
- Mitigação: Uso de Redis como cache, fallback para dados armazenados no
Supabase, WF_Error_Handler para notificação imediata.\
\
\*\*Risco:\*\* Rate limiting em APIs externas (Binance, OpenAI)\
- Probabilidade: Média\
- Impacto: Alto\
- Mitigação: Estratégia de cache com TTL adequado, monitoramento via
tabela ApiUsage, escalonamento para planos pagos se necessário.\
\
\*\*Risco:\*\* Erros de interpretação da IA (LangChain)\
- Probabilidade: Média\
- Impacto: Médio\
- Mitigação: Ajustes iterativos em prompts de sistema, registro em
ErrorState para auditoria e refinamento.\
\
\*\*Risco:\*\* Perda de dados ou corrupção no banco (Supabase/Postgres)\
- Probabilidade: Baixa\
- Impacto: Alto\
- Mitigação: Backups automáticos do Supabase, restore rápido, boas
práticas de schema.\
\
\*\*Risco:\*\* Redis não disponível\
- Probabilidade: Baixa\
- Impacto: Médio\
- Mitigação: Fallback para Supabase PriceCache, monitoramento do serviço
Redis.\
\
\*\*Risco:\*\* Webhook do Telegram exposto/abusado\
- Probabilidade: Baixa\
- Impacto: Alto\
- Mitigação: Proteção com token secreto, whitelisting de chatId,
monitoramento de acessos.\
\
\*\*Risco:\*\* Custos inesperados de APIs (OpenAI, TAAPI.io)\
- Probabilidade: Média\
- Impacto: Médio\
- Mitigação: Monitoramento ApiUsage, alertas de consumo, definir limites
orçamentários.\
\
\*\*Risco:\*\* Falha de infraestrutura (n8n, servidor
Hostinger/Portainer)\
- Probabilidade: Baixa\
- Impacto: Alto\
- Mitigação: Backup de workflows, possibilidade de reimplantar em outro
host rapidamente.\
\
\*\*Risco:\*\* Crescimento inesperado de usuários (mesmo não previsto)\
- Probabilidade: Baixa\
- Impacto: Médio\
- Mitigação: Arquitetura já preparada para múltiplos usuários,
escalabilidade futura com RabbitMQ se necessário.

# 3. Conclusão

A matriz de riscos fornece um mapa claro dos pontos vulneráveis do
projeto e suas soluções. Com mitigação ativa (cache, monitoramento, logs
e segurança de credenciais), o bot terá resiliência suficiente para uso
pessoal e expansões futuras.
