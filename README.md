# Socializ-RustEdition

**Living Civilizations** — mod de simulação social e civilizações autônomas para **Minecraft Horizon**, com núcleo independente em Rust.

> Estado atual: **fundação documental / nenhuma jogabilidade implementada ou validada.** Esta documentação é uma proposta de engenharia, não uma descrição de um mod pronto.

## Visão

Um mundo Minecraft habitado por humanos com identidades persistentes, rotinas, necessidades, habilidades, relações de sangue e afetivas, memória, conversas procedurais, economia real, construção e mineração de blocos, conflitos e civilizações que podem prosperar, migrar ou desaparecer. Sem LLMs, conexão à internet ou diálogos gerados remotamente.

O usuário conduz a visão; o assistente elabora regras, contratos, casos críticos e planos; o Codex implementa, testa e documenta as evidências. **Não presumir que Codex tem acesso ao jogo sem verificar o executor.**

## Primeira experiência: laboratório Trio da Cabana

Em **cada mundo**, no primeiro uso do mod, uma cabana de teste deve ser preparada perto do spawn seguro, dentro da área visual inicial sempre que possível. São criados **exatamente três registros persistentes**, uma única vez:
- **A e B são irmãos biológicos**.
- **B e C têm relacionamento romântico inicial; C não é parente de A/B**.
- **A começa solteiro**, com liberdade para estabelecer relações; nenhum romance com o jogador é obrigatório.

Os NPCs não reaparecem a cada abertura. Personagens mortos, migrados ou ausentes fisicamente mantêm seu estado verdadeiro. A cabana de três moradores é uma exceção intencional aos presets futuros de cabana isolada (1–2 habitantes).

## Decisões e limites

- **Escopo atual:** single-player offline, inicialmente PC.
- **Fora de escopo por enquanto:** servidores dedicados, LAN, multiplayer e hospedagem.
- **Android:** objetivo de compatibilidade; o port Starling não oferece, no APK padrão atual, suporte direto a `.hnmod`. Nenhum suporte mobile está concluído.
- **Horizon MCP:** **EM ESTUDO / NÃO DECIDIDO**. Investigar comandos, permissões e automação sem configurar, integrar, fechar arquitetura ou criar MCP próprio sem decisão posterior.
- **Horizon:** usar revisão exata auditada e mixins nativos; não substituir essa verificação por suposições.
- **Segurança:** nunca alterar saves reais do usuário nos testes; proteger estruturas, recursos e privacidade.

## Comece aqui

| Documento | Responsabilidade |
|---|---|
| [AGENTS.md](AGENTS.md) | Contrato de execução econômica e verificável para Codex |
| [GDD](docs/GDD.md) | Experiência, princípios e escopo do jogo |
| [Arquitetura](docs/ARCHITECTURE.md) | Fronteiras, modelo de simulação e invariantes |
| [Contratos do domínio](docs/DOMAIN_CONTRACTS.md) | IDs, comandos, eventos e persistência |
| [Índice das ideias](docs/IDEAS/INDEX.md) | Status por domínio e versão, sem criar documentos infinitos |
| [Laboratório dos três NPCs](docs/IDEAS/COLONIA_INICIAL.md) | Fixture, criação uma vez, estados e testes |
| [Roadmap](docs/ROADMAP.md) | Marcos, dependências e critérios objetivos |
| [Testes](docs/TESTING.md) | Matriz de testes automatizados e verificações in-game |
| [Ferramentas e compatibilidade](docs/TOOLS_AND_COMPATIBILITY.md) | Rust, Horizon, Codex, Android e opções MCP em aberto |
| [Decisões](docs/DECISIONS.md) | Escolhas, pendências e não decisões |
| [Glossário](docs/GLOSSARY.md) | Termos para evitar ambiguidades |

**Estado de V1 de uma ideia = maturidade da especificação, não código integrado.** Consulte sempre [docs/IDEAS/INDEX.md](docs/IDEAS/INDEX.md).

Projeto não oficial; não incluir assets de Minecraft, credenciais nem código de terceiros sem licença.
