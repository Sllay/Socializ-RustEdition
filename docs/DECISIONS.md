# Registro de decisões e hipóteses

Última revisão documental: **2026-11-08**. Atualizar este arquivo apenas após decisão explícita; citar evidências para decisões técnicas.

| ID | Tipo | Decisão / restrição | Estado |
|---|---|---|---|
| D-001 | Escopo | Single-player offline antes de qualquer rede/servidor | FIXA (fase atual) |
| D-002 | Produto | Mod de humanos autônomos sem LLM/ChatGPT/Llama | FIXA |
| D-003 | Tecnologia | Núcleo Rust independente, adaptador Horizon separado | DIRETRIZ DE ARQUITETURA |
| D-004 | Laboratório | Trio da Cabana: A-B irmãos, B-C casal, A solteiro | FIXA |
| D-005 | Persistência | Genesis uma vez por mundo; nenhuma duplicação ao reabrir | FIXA |
| D-006 | Mundo | Assentamentos esparsos, geração sob demanda, presets iniciais 1–50 | DIRETRIZ |
| D-007 | IA | Combinar Utility, GOAP/HTN, árvore de comportamentos e percepção | CANDIDATA, avaliar por necessidade |
| D-008 | Simulação | LOD ativo/regional/estratégico com reconciliação | DIRETRIZ |
| D-009 | Diálogo | Sem LLM; intenção social + estado + realização linguística contextual | FIXA |
| D-010 | Interface | **Android é o dispositivo real**; manter compatibilidade por design com PC, mas validar funcionamento no app móvel instalado | FIXA quanto ao ambiente |
| D-011 | MCP Horizon | Socket local do app Android identificado; bridge Cloud↔Android depende de acesso autorizado ao socket e transporte remoto; **não fechar o desenho agora** | **EM ESTUDO** |
| D-012 | Ferramenta Codex | Codex executor com relatórios, limites de contexto e testes | FIXA |
| D-013 | Repositório | `Sllay/Socializ-RustEdition` | FIXA |
| D-014 | Segurança | Não sobrescrever mundo real nem teleportar/ressuscitar personagem por unload | FIXA |
| D-015 | Ambiente | Usuário **não dispõe de PC**; possui Android com Horizon instalado e Termux; Codex executa em **cloud** | FIXA |
| D-016 | Conexão | Configuração `horizon-ctl mcp` via socket privado Android **não alcança Codex Cloud diretamente** | VERIFICADA (topologia), conexão ainda BLOQUEADA |

## Questões abertas (não transformar em implementação por conta própria)
- Como disponibilizar hooks exatos de entidade, save, geração de cabana, diálogos e UI na revisão pinada do Horizon?
- Qual abordagem de transação consegue conciliar mudanças do mod com commits de chunk?
- Qual presença de dados em memória será reservada para familiares importantes longe do jogador?
- Como testar interface e gameplay com **Codex Cloud** e **Horizon Android**: acesso permitido ao socket privado, possível bridge interna do app, transporte autenticado e capacidade de MCP remoto no executor específico? **Investigar; não escolher ainda.**
- Port Android/Starling: quais interfaces e mods são tecnicamente viáveis, com evidência no aparelho?
- Parâmetros de demografia, ética de interação, proteção do jogador, escala temporal e personalidade são **ajustáveis**, ainda não números finais.

## Política
Não retroativamente declarar hipóteses como fatos. Uma decisão revisada registra motivo, alternativa rejeitada, data e impacto nos documentos de ideias.
