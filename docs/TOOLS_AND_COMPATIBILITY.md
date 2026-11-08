# Ferramentas e compatibilidade — inventário, não instalação

## Stack proposta
- **Rust/Cargo** para núcleo determinístico, bibliotecas e testes. `cargo fmt`, `cargo clippy`, `cargo test`; usar lockfile e revisar licenças.
- **Horizon** como cliente offline alvo inicial. Mods `.hnmod` usam `horizon-mixins` e são compilados em uma build do jogo; a API é experimental.
- **Template oficial** `horizon-rust/horizon-native-mod-template` como candidato de partida: revisar `compatibility.json`, commits pinados, `VALIDATION.md` e requisitos do executor. Não copiar pin como se fosse da versão atual.
- **GitHub** para documentos, commits e revisão; **Codex** executor de implementação e testes, não fonte de evidência sem logs.
- Bibliotecas **candidatas** (não escolhidas): `serde` (serialização), `pathfinding` (A*), `petgraph` (grafos), `rstar` (índice espacial), crates de GOAP/BT; checar manutenção, licença, API e benchmark antes de integrar.
- **FAtiMA Toolkit / Prom Week / Dwarf Fortress / RimWorld / Songs of Syx** como referências conceituais, não dependências nem código para copiar.

## Matriz
| Ambiente | Classificação | Critério |
|---|---|---|
| PC Horizon single-player | Alvo inicial, **não testado no projeto** | Compilar, abrir mundo e validar ações |
| Mods `.hnmod` nativos | Documentados, integração própria pendente | Auditoria de hooks + build |
| Horizon CLI `horizon-ctl` | Documentado, **não escolhido** | Revisar comandos e segurança |
| MCP Horizon | Documentado oficialmente, **EM ESTUDO / NÃO CONECTAR AINDA** | Decisão em conjunto + prova no executor |
| Horizon headless | Possibilidade documentada, uso ainda não decidido | Confirmar flags/limitações |
| Android Starling `.hnmod` | Bloqueado no APK padrão | Novo binário/port e teste real |
| Android Starling `.hmod` sandbox | Documentação anuncia suporte em builds 64-bit | Não equivale a suporte `.hnmod` |
| Servidor/LAN/multiplayer | Congelado | Não desenvolver nesta fase |

## Android e UI
Desenhar interfaces com alvos de toque adequados, escala adaptativa, navegação de teclado, foco explícito e balões de texto com filtros de frequência. Isso **não** comprova portabilidade. O suporte oficial às fontes/hook/clientes Android precisa ser auditado no momento oportuno.

## Segurança de automação
MCP/CLI podem executar ações sobre mundos e arquivos. Documentação oficial descreve confirmação de ações destrutivas; mesmo assim exigir mundo descartável, backup, permissões mínimas e decisão explícita antes da conexão real. Não confundir integração com modelos generativos: MCP serviria para **testar**; NPCs continuam sem LLM.

## Fontes oficiais e pontos de consulta
- https://playhorizon.dev/docs/mods
- https://playhorizon.dev/docs/make-a-mod
- https://playhorizon.dev/docs/mod-code
- https://playhorizon.dev/docs/agents
- https://playhorizon.dev/docs/apis
- https://github.com/horizon-rust/horizon-native-mod-template
- https://github.com/horizon-rust/horizon
- https://github.com/starling-client/starling

Última consulta documental: 2026-11-08. Toda alteração de API exige nova verificação.
