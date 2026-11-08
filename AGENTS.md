# Contrato operativo do Codex — Socializ-RustEdition

Leia `README.md`, `docs/DECISIONS.md`, `docs/ROADMAP.md` e **apenas** os documentos da tarefa. `docs/GDD.md` descreve a experiência, `docs/ARCHITECTURE.md` os limites, `docs/IDEAS/` as especificações vivas.

## Regras mandatórias
1. Foco single-player **offline**; servidor, LAN e multiplayer congelados. Não criar código ou infra para isso.
2. Três NPCs de teste por mundo: A/B irmãos, B/C casal, A inicialmente solteiro; criação idempotente, sem ressuscitar mortos ou teleportar emigrados na reabertura.
3. Sem LLM/serviço remoto na inteligência ou nos diálogos; todos os resultados devem ser reproduzíveis e testáveis localmente.
4. Nunca improvisar uma API Horizon. Verificar revisão real, fonte, contrato, disponibilidade e limitações antes de adaptar. Não alterar upstream sem tarefa explícita.
5. Núcleo Rust separado do adaptador Horizon; não exigir o jogo para testes de domínio.
6. Não editar saves do usuário. Usar mundo-espelho temporário, backup e fixture isolada; nunca destruir estruturas preexistentes.
7. Sem duplicação de entidades/itens, alterações de blocos sem validação, conhecimento onisciente, progressão espontânea sem recursos ou resultados inventados.
8. Os documentos de ideias são **centrais por domínio**, com V1/V2 e estado por versão. V1 especificada não equivale a implementada; teste unitário não equivale a teste in-game. Atualizar índice e documento juntos.
9. Antes de criar arquivo de ideias, pesquisar domínio já existente; evitar microdocumentos. Novas ideias começam `CAPTURADA`.
10. **MCP Horizon está EM ESTUDO.** Não instalar/configurar integração, abrir sockets, conectar ao jogo, acionar comandos ou criar MCP novo sem autorização e decisão posteriores; pode analisar documentação e testar código Rust independentemente do jogo.
11. Ferramentas/agentes: um executor principal por padrão; subagente apenas com justificativa e tarefa paralelizável, sem delegação recursiva. Não desperdiçar contexto lendo toda a base.
12. Segurança de dependências: sem chaves, tokens, recursos de Mojang, binários de terceiros, licenças incompatíveis ou scripts remotos executados sem inspeção.
13. PC é o alvo inicial; Android/Starling é alvo **condicional**. Não afirmar suporte `.hnmod` ou cross-platform sem testes reais.
14. Alterar apenas o necessário e reportar incertezas. Não atualizar estados ou declarar sucesso com base em documentação externa.
15. Antes de entregar qualquer implementação: `fmt`, `clippy`, testes relevantes e cenário de falha, se ambiente permitir; registrar comandos e saída reais.
16. Commits somente dentro do escopo autorizado; se houver mudanças concorrentes, parar e reconciliar em vez de sobrescrever.

## Relatório obrigatório por tarefa
- Objetivo e escopo; decisão/ideia versionada relacionada;
- Arquivos e diffs relevantes;
- Revisões exatas de dependências, se houver;
- Comandos e testes **realmente executados**, resultados e links para evidências;
- Não executados e motivo;
- Riscos, bloqueios e próxima ação mínima.

Se a integração Horizon/MCP não estiver disponível, **não simular uma aprovação in-game**.