# 🧠 Mapa Mental - Bot Cripto Telegram

```
🤖 BOT CRIPTO TELEGRAM
│
├── 📱 INTERFACE (TELEGRAM)
│   ├── 🎯 Comandos
│   │   ├── /start → Boas-vindas → Solicita Token
│   │   ├── /help → Lista comandos e instruções
│   │   └── [Token Input] → Menu Inline Interativo
│   │       ├── 💰 Preço
│   │       ├── 🔔 Criar Alerta
│   │       ├── 📰 Notícias
│   │       ├── 📊 Análise Técnica
│   │       └── 📋 Meus Alertas
│   │
│   └── 🔄 Respostas
│       ├── Mensagens Formatadas
│       ├── Inline Keyboards
│       └── Notificações Push (Alertas)
│
├── 🧬 NÚCLEO N8N (WORKFLOWS)
│   ├── 📥 WF_Bot_Principal
│   │   ├── Webhook Telegram (entrada)
│   │   ├── 🤖 Agente Parser (IA)
│   │   │   ├── Interpreta comandos
│   │   │   ├── Identifica tokens
│   │   │   └── Extrai parâmetros
│   │   ├── Router de Comandos
│   │   ├── Processadores
│   │   │   ├── Buscar Preço
│   │   │   ├── Criar Alerta
│   │   │   ├── Buscar Notícias
│   │   │   └── Análise Técnica
│   │   └── Formatar e Enviar Resposta
│   │
│   ├── ⏰ WF_Monitor_Alertas
│   │   ├── Schedule (1 minuto)
│   │   ├── Query Alertas Ativos
│   │   ├── Buscar Preços Atuais
│   │   ├── Comparar Condições
│   │   └── Enviar Notificações
│   │
│   └── 🚨 WF_Error_Handler
│       ├── Capturar Erros
│       ├── Log Detalhado
│       ├── Estado DESCONHECIDO
│       └── Notificar Admin
│
├── 🤖 AGENTES IA (OpenAI)
│   ├── 📝 Parser de Comandos
│   │   ├── Entende linguagem natural
│   │   ├── Identifica intenções
│   │   └── Normaliza tokens
│   │
│   ├── 📊 Analista Técnico
│   │   ├── Interpreta indicadores
│   │   ├── Gera insights
│   │   └── Define tendências
│   │
│   └── 📰 Curador de Notícias
│       ├── Filtra relevância
│       ├── Traduz conteúdo
│       └── Analisa sentimento
│
├── 🔌 APIs EXTERNAS
│   ├── 💹 Binance
│   │   ├── Preços em tempo real
│   │   ├── Volume 24h
│   │   ├── OHLCV (candlesticks)
│   │   └── Todos os tokens
│   │
│   ├── 📈 TAAPI.io
│   │   ├── RSI
│   │   ├── Stochastic RSI
│   │   ├── MACD
│   │   └── EMAs (9,21,50,200)
│   │
│   ├── 📰 CryptoCompare
│   │   ├── Notícias cripto
│   │   ├── Categorias
│   │   └── Múltiplas fontes
│   │
│   └── 🧠 OpenAI
│       ├── GPT-4 parsing
│       ├── Tradução
│       └── Análise sentimento
│
├── 💾 BANCO DE DADOS (Supabase)
│   ├── 📊 Tabelas Principais
│   │   ├── alerts (alertas de preço)
│   │   ├── user_settings (preferências)
│   │   ├── bot_config (configurações)
│   │   └── bot_logs (auditoria)
│   │
│   ├── 🚀 Cache Tables
│   │   ├── price_cache (30s TTL)
│   │   ├── technical_analysis (15min TTL)
│   │   └── news_cache (30min TTL)
│   │
│   ├── 🔍 Controle e Debug
│   │   ├── api_usage (rate limiting)
│   │   └── error_states (debugging)
│   │
│   └── ⚡ Otimizações
│       ├── Índices estratégicos
│       ├── Views materializadas
│       └── Funções auxiliares
│
├── 🛡️ SEGURANÇA
│   ├── 🔐 Credenciais
│   │   ├── N8N Vault
│   │   ├── Variáveis ambiente
│   │   └── Tokens secretos
│   │
│   ├── ✅ Validações
│   │   ├── Input sanitization
│   │   ├── Schema validation
│   │   └── Type checking
│   │
│   └── 📝 Auditoria
│       ├── Logs completos
│       ├── Rastreamento execução
│       └── Métricas performance
│
├── 🎯 FUNCIONALIDADES
│   ├── 💰 Consulta de Preços
│   │   ├── Tempo real
│   │   ├── Variação 24h
│   │   └── Volume
│   │
│   ├── 🔔 Sistema de Alertas
│   │   ├── Criar (acima/abaixo)
│   │   ├── Monitorar (1min)
│   │   ├── Notificar
│   │   └── Gerenciar
│   │
│   ├── 📊 Análise Técnica
│   │   ├── Multi-timeframe
│   │   ├── 4 indicadores
│   │   ├── Interpretação IA
│   │   └── Tendência geral
│   │
│   └── 📰 Agregador Notícias
│       ├── Múltiplas fontes
│       ├── Tradução PT-BR
│       ├── Análise sentimento
│       └── Filtro por token
│
├── ⚙️ CONFIGURAÇÕES
│   ├── 🔧 Parâmetros
│   │   ├── Intervalos monitoramento
│   │   ├── TTL caches
│   │   ├── Rate limits
│   │   └── Timeframes análise
│   │
│   └── 🌍 Localização
│       ├── Idioma (PT-BR)
│       ├── Timezone (São Paulo)
│       └── Formato números
│
└── 📈 MONITORAMENTO
    ├── 📊 Métricas
    │   ├── Tempo resposta
    │   ├── Taxa sucesso
    │   ├── Uso APIs
    │   └── Alertas disparados
    │
    ├── 🚨 Alertas Sistema
    │   ├── Erros críticos
    │   ├── Rate limit exceeded
    │   └── Cache miss
    │
    └── 📝 Logs
        ├── Execuções
        ├── Erros
        ├── Performance
        └── Auditoria
```

## 🔄 Fluxo de Dados Principal

```
USUÁRIO → TELEGRAM → WEBHOOK N8N → AGENTE IA → ROUTER
           ↓                           ↓          ↓
      [Mensagem]                 [Interpretação] [Decisão]
                                                   ↓
                                            APIs EXTERNAS
                                                   ↓
                                              SUPABASE
                                                   ↓
                                            PROCESSAMENTO
                                                   ↓
                                            FORMATAÇÃO
                                                   ↓
                                        TELEGRAM ← USUÁRIO
```

## 🎯 Pontos-Chave de Integração

### 1. **Entrada Unificada**
- Todos os comandos entram pelo Webhook
- Parser IA normaliza diferentes formatos
- Router direciona para ação correta

### 2. **Cache Inteligente**
- 3 níveis de cache (preços, análise, notícias)
- TTL configurável por tipo
- Reduz chamadas de API em 70%

### 3. **Monitoramento Contínuo**
- Alertas verificados a cada minuto
- Logs de todas operações
- Métricas de performance

### 4. **Recuperação de Erros**
- Estado DESCONHECIDO para erros
- Fallbacks configurados
- Retry com backoff exponencial

## 🚀 Expansões Futuras

```
FASE 2
├── 📊 Dashboard Web
├── 📈 Backtesting
├── 🤝 Multi-usuário
└── 📱 App Mobile

FASE 3
├── 🎯 Trading automatizado
├── 🧠 ML predictions
├── 📊 Portfolio tracking
└── 🔗 DEX integration
```