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

## 2026-11-08 — Topologia efetiva confirmada pelo usuário

- Apenas **um Android com Termux e Horizon mobile**; **nenhum PC local**.
- Codex utilizado é **Codex Cloud**, com executor remoto.
- O menu **Horizon agent control (this computer only)** apresenta:
  - `Socket: /data/user/0/dev.horizon.android/cache/horizon-control.sock`
  - `/system/bin/horizon-ctl --socket ... state`
  - configuração JSON MCP `command: "/system/bin/horizon-ctl"`, `args: ["--socket", "...", "mcp"]`.
- A configuração é stdio e exige que o executável e o socket existam no **mesmo host** do processo cliente; copiar texto ao Codex Cloud não transporta a conexão. O comando `/system/bin/horizon-ctl` é um **caminho anunciado**, existência/permissão ainda não verificadas.
- O socket está na pasta privada do app Android (`dev.horizon.android`), protegida por UID e SELinux; **Termux não possui acesso automático**. Android documenta que apps não podem acessar pastas privadas de outros apps. Acesso por ADB também não significa que o usuário `shell` possa abrir esse socket em uma release não depurável.
- **Não contornar sandbox** com root, exploits, permissões genéricas, chmod em diretórios privados ou exposição de portas públicas.

### Diagnósticos read-only permitidos, realizados pelo usuário no Termux, sem instalação
```sh
id
getprop ro.build.version.release
ls -l /system/bin/horizon-ctl
ls -ld /data/user/0/dev.horizon.android/cache
```
Interpretar `No such file or directory` (binário anunciado não presente), `Permission denied` (barreira de sandbox), e NÃO inferir que a porta está disponível. Não solicitar chaves nem tokens em chat.

### Duas estratégias técnicas, nenhuma adotada

**I — Testes Codex Cloud independentes:** executar `cargo test`, simulação em crates sem Horizon, fuzz/propriedades/snapshot; se executável compatível e assets legalmente preparados, experimentar Horizon `--headless` **no próprio executor cloud**. MCP nesse caso controlaria o Horizon **em nuvem**, NÃO o aplicativo Android do usuário. Avaliação visual e runtime Android continuam pendentes.

**II — Controle do Horizon móvel:** requer `horizon-ctl` e acesso autenticado/legítimo ao socket **dentro do próprio app**, ou serviço Android explicitamente exportado pelo port com permissões de assinatura/consentimento. Daí um bridge poderia enviar apenas comandos permitidos por canal autenticado (mTLS/túnel com saída iniciada no celular), traduzir para MCP Streamable HTTP e conectar-se a cliente cloud compatível. **Somente criar essa ponte após auditar o APK e o suporte a MCP externo do Codex Cloud real.** Termux pode gerenciar transporte externo autorizado, mas não rompe acesso ao sandbox por si só. Não afirmar que é possível no APK atual.

Possíveis alternativas sob condições especiais: build de depuração com `run-as`, autorização do mantenedor do port, API explícita no app ou aparelho com root (não recomendado). Cada opção exigirá consentimento e análise técnica/securitária; não oferecer como receita pronta.

### Requisitos de segurança para qualquer ponte
- Auth forte, tokens rotativos fora do Git e logs, lista mínima de ferramentas, confirmação para `setblock`, `fill`, `world-delete` e alteração de arquivos.
- Worlds de teste/backup; permitir corte imediato do Agent Control e conexão remota.
- Relatório de cada comando/reply e sessão; limitar frequências, dimensões de captura e duração.
- Não expor diretamente o Unix socket ou ADB na internet. Não criar serviço multiplayer Minecraft: seria transporte de **controle de ferramenta**, não um servidor do jogo.

### Port/mod nativo independente
Mesmo com controle remoto, ainda falta determinar se `dev.horizon.android` aceita as modificações Rust compiladas em `.hnmod`. A disponibilidade de MCP no menu não comprova suporte a mods nativos.

Fontes:
- https://playhorizon.dev/docs/agents
- https://playhorizon.dev/docs/api/agent-control
- https://developer.android.com/about/versions/11/privacy/storage
- https://developers.openai.com/api/docs/guides/agents-api/tools/mcp
- https://help.openai.com/pt-br/articles/20001545-using-codex-cloud
