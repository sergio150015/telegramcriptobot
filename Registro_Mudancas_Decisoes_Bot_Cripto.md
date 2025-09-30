# 1. Introdução

Este documento mantém um histórico consolidado das principais mudanças e
decisões tomadas durante o desenvolvimento do Bot Cripto Telegram. O
objetivo é garantir rastreabilidade, clareza de motivos e registro de
impacto para cada alteração.

# 2. Registro

  -----------------------------------------------------------------------------
  Data           Tipo           Descrição      Motivo         Impacto
  -------------- -------------- -------------- -------------- -----------------
  2025-09-25     Decisão        Não adotar     Projeto é      Menos
                                DRP/BCP no     estudo         complexidade,
                                projeto        pessoal, sem   foco em
                                               necessidade de funcionalidades
                                               continuidade   principais
                                               formal         

  2025-09-25     Mudança        Agente IA não  Segurança e    Escopo
                                executa ordens clareza de     simplificado,
                                reais          escopo         evita riscos
                                                              desnecessários

  2025-09-25     Decisão        Redis não      Uso apenas     Evita
                                precisa de     como cache     complexidade
                                modelagem      (chaves/TTLs   desnecessária na
                                formal         já definidos)  fase inicial
  -----------------------------------------------------------------------------

# 3. Conclusão

O registro de mudanças e decisões será atualizado continuamente conforme
o projeto evoluir. Esse histórico permitirá entender não apenas o estado
atual, mas também o porquê de cada alteração realizada.
