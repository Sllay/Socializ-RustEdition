# Prompt para Codex — Fase 0, auditoria (usar somente quando o usuário autorizar execução)

Você está no repositório `Sllay/Socializ-RustEdition`, um projeto em fase de documentação. **Objetivo exclusivo: verificar a viabilidade de um mod offline Rust do Horizon e produzir relatório técnico. Não implementar NPCs ou mexer em saves reais.**

Leia `AGENTS.md`, `docs/DECISIONS.md`, `docs/ROADMAP.md`, `docs/TOOLS_AND_COMPATIBILITY.md`, `docs/ARCHITECTURE.md`, `docs/IDEAS/COLONIA_INICIAL.md` e `docs/TESTING.md`. Não varra outros documentos sem necessidade.

1. Inspecione o template oficial `horizon-rust/horizon-native-mod-template`, revisões e licenças; registre SHA realmente verificado e compatibilidade com `horizon-mixins`.
2. Audite fontes e hooks de entidade, tick, alteração de bloco, save, spawn seguro, eventos de UI e mod nativo offline. Classifique: confirmado por código; documentado; experimental; indisponível.
3. Identifique ferramentas e dependências realmente disponíveis no executor (Rust/Cargo, assets legalmente preparados, binários) e as que faltam. `cargo test` em fixture se possível, sem alterar motor do usuário.
4. Em `docs/REPORTS/`, crie relatório com comandos executados, logs curtos, versão, evidência, hipóteses e bloqueios. Não invente benchmarks ou screenshots.
5. Pesquise comandos CLI, MCP e headless do Horizon para um **quadro comparativo**. **O MCP está EM ESTUDO: não instalar, conectar, configurar, ativar agent control, criar MCP customizado nem usar o jogo para automação nesta fase.** Apenas descrever capacidades e riscos.
6. Verifique restrições do port Android/Starling e registre que o APK padrão não aceita nativos `.hnmod` diretamente, salvo prova contrária na revisão atual.
7. Atualize somente docs afetados e entregue um resumo auditável. Não marque nenhum módulo como integrado.

Não execute trabalho de servidor/LAN/multiplayer. Não crie agentes aninhados, nem múltiplos subagentes. Se ambiente não estiver disponível, relate claramente `BLOCKED`.

Critério: inventário técnico rastreável + plano mínimo da Fase 1 com interfaces e incertezas. A decisão de usar MCP fica **explicitamente pendente** ao usuário.
