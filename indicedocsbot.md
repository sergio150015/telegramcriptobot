# 🤖 Projeto Bot Cripto Telegram

> **Versão:** 1.0 | **Status:** Em Desenvolvimento | **Data:** Dezembro 2024

Este é o documento central que organiza toda a documentação do projeto Bot Cripto. Utilize os links abaixo para navegar rapidamente para o documento específico de cada área.

## 📄 Documentação Principal

### 1. Planejamento e Visão do Produto

* [**PRD - Documento de Requisitos do Produto**](./PDR2.pdf)  
    * Define o que o bot deve fazer, para quem e por quê. [cite_start]Cobre o objetivo, o usuário-alvo, as tecnologias e as funcionalidades principais[cite: 75, 78, 80, 85].

* [**Casos de Uso**](./casos-uso-bot-cripto.md)  
    * Descreve em detalhes cada interação do usuário com o bot, como `UC-02: Consultar Preço` e `UC-03: Criar Alerta`, incluindo fluxos principais, alternativos e regras de negócio.

### 2. Arquitetura e Engenharia

* [**Mapa Mental**](./mapa-mental-bot-cripto.md)  
    * Oferece uma visão geral da arquitetura e dos componentes, conectando a Interface (Telegram), o Núcleo (N8N), as APIs Externas e o Banco de Dados (Supabase).

* [**Diagrama de Fluxo de Dados (DFD)**](./dfd-bot-cripto.md)  
    * Mostra visualmente como os dados se movem através do sistema, desde os comandos do usuário até as respostas, passando pelos processos internos e armazenamentos de dados.

* [**APIs e Integrações**](./apis-integracoes-bot.md)  
    * Documento técnico com os detalhes de todas as APIs externas: Telegram, Binance, TAAPI.io, CryptoCompare, OpenAI e Supabase, incluindo endpoints, rate limits e exemplos.

* [**Schema do Banco de Dados (SQL)**](./tabelas-supabase-schema-completo.sql)  
    * O script SQL completo para criar todas as 9 tabelas, índices, funções e views necessárias no nosso banco de dados Supabase (PostgreSQL).

* [**Schema Prisma (ORM)**](./prisma-schema-bot.txt)  
    * Uma representação alternativa do schema do banco de dados utilizando a sintaxe do Prisma ORM, definindo models como `Alert` e `PriceCache`.

### 3. Operação e Qualidade

* [**Matriz de Riscos e Contingências**](./matriz-riscos-bot-cripto.md)  
    * Identifica e prioriza 15+ riscos potenciais, como `R01: Falha Total da API Binance` e `R02: Ataque/Abuso do Bot`, e define planos de mitigação e contingência para cada um.

* [**Runbook Operacional**](./runbook-operacional-bot.md)  
    * O guia prático para troubleshooting e operações diárias. Contém checklists e procedimentos passo a passo para resolver problemas comuns, como "Bot não responde" ou "Alertas não disparam".

* [**Checklist de Deploy**](./checklist-deploy-bot.md)  
    * O roteiro completo, dividido em 7 fases, para colocar o bot no ar de forma segura e verificada, cobrindo desde a preparação das credenciais até os testes pós-deploy.