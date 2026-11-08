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
| Horizon Android single-player | **Ambiente real do usuário**, execução de `.hnmod` não validada | Identificar app, revisão, carregamento de código nativo e controles |
| Mods `.hnmod` nativos (Horizon desktop) | Documentados; **não supor funcionamento no APK móvel** | Auditar port instalado e alternativa de execução |
| Horizon CLI `horizon-ctl` | Documentado, **não escolhido** | Revisar comandos e segurança |
| MCP Horizon | **Socket local privado no Android identificado**; cloud não o acessa por path. **EM ESTUDO / NÃO CONECTAR AINDA** | Diagnóstico de permissões + desenho de bridge e autorização |
| Horizon headless | Possibilidade documentada, uso ainda não decidido | Confirmar flags/limitações |
| Android Starling `.hnmod` | Não suportado diretamente no APK padrão segundo documentação consultada; confirmar se o app `dev.horizon.android` corresponde à mesma distribuição | Auditoria de port/versionamento e runtime nativo |
| Android Starling `.hmod` sandbox | Documentação anuncia suporte em builds 64-bit | Não equivale a suporte `.hnmod` |
| Servidor/LAN/multiplayer | Congelado | Não desenvolver nesta fase |

## Topologia real de desenvolvimento

- **Dispositivo do usuário:** Android com Horizon (`dev.horizon.android`) e Termux; nenhum PC local disponível.
- **Codex:** executor cloud separado do Android; comandos stdio/caminhos de socket executados em cloud não alcançam o celular.
- **Caminho reportado pelo jogo:** `/data/user/0/dev.horizon.android/cache/horizon-control.sock`; pertence à sandbox privada do app. `/system/bin/horizon-ctl` é apenas um caminho que a interface informa e deve ser verificado localmente, sem assumir que existe.
- **Primeiro teste permitido:** inspeção não destrutiva no Termux, sem root/ADB/circunvenções de sandbox. Se houver `Permission denied`, interromper tentativa de acesso ao socket.
- **Futuro remoto, em pesquisa:** bridge *autorizado e embutido no app*, ou mecanismo de acesso explicitamente exportado pelo port, seguido de transporte autenticado de saída para um serviço remoto e suporte de cliente MCP no executor. Túnel Termux sozinho não rompe sandbox do Android.
- **Plano independente:** compilar e testar o núcleo Rust no Codex Cloud; avaliação de runtime headless na cloud é opcional e não substitui teste Android.

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
