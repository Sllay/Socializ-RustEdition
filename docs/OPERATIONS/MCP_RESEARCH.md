# MCP Horizon — caderno de pesquisa ABERTO

**DECISÃO ATUAL: EM ESTUDO. NÃO IMPLEMENTAR, CONFIGURAR, CONECTAR OU ENCERRAR ESTA DISCUSSÃO.**

O usuário quer explorar com o assistente as alternativas antes de escolher como Codex interagirá com o Horizon. Este documento **não** determina uma implementação.

## Opções candidatas
| Opção | Vantagem | Limitações / dúvida |
|---|---|---|
| Testes Rust sem jogo | Determinismo, rapidez, CI | Não valida hooks ou UI |
| `horizon-ctl` / CLI oficial | Automação sem criar servidor remoto | Confirmar comandos efetivos da versão instalada |
| MCP oficial do Horizon | Interface acessível por agentes como Codex | Depende do executor, permissões e sessão local |
| Modo headless | Testes de lógica sem interface | Não substitui verificação gráfica |
| Capturas GUI e interação | Valida diálogos, HUD, câmera e input | Necessita ambiente gráfico acessível |
| Instrumentação de debug no mod | Inspecionar objetivos, reservas, eventos | Precisa de hooks seguros e protocolo próprio |
| MCP complementar futuro | Ferramentas específicas ausentes no oficial | Só considerar após inventário do que falta |

## Perguntas em aberto
- Quais comandos exatos existem na revisão pinada? Há API para inspecionar NPCs personalizados?
- Execução no mesmo host? Como isolar mundo e permissões?
- O modo headless conserva sistemas de entidade, blocos e UI lógica relevantes?
- O Codex do usuário consegue controlar o processo local ou apenas um executor remoto?
- Como capturar logs, snapshots de estado e provas de falha sem confundir resultado previsto com real?
- Como adaptar essa automação futuramente ao Android, se o port nativo não aceitar `.hnmod`?

## Critérios futuros, não decisão
A solução escolhida deve ser local/offline, reproduzível, auditável, reversível, segura para saves, com baixo custo de tokens e testes reais de comportamento. Nenhuma solução foi aprovada. Não adicionar configuração MCP ao repositório por antecipação.

Referência: https://playhorizon.dev/docs/agents
