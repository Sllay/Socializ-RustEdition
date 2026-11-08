# GDD — Socializ-RustEdition

**Fase:** concepção e documentação; nenhuma feature jogável concluída.

## Premissa
No Minecraft Horizon, humanos autônomos vivem com limitações, personalidade, necessidades, profissões, famílias, memória, interesses e história. Eles coletam, fabricam e consomem materiais reais, constroem no terreno, desenvolvem culturas e comunidades, negociam e podem entrar em crise ou desaparecer. O jogador pode observar, colaborar, interferir, criar laços ou provocar conflitos. Não há roteiro obrigando civilizações a crescer.

## Pilares de experiência
1. **Agência**: NPC decide segundo informações imperfeitas, necessidades, recursos e valores; não executa eternamente uma linha fixa.
2. **Causalidade**: cada construção, conversa, promessa, morte e conflito altera o mundo e gera consequências observáveis.
3. **Vida social**: relações familiares, amizade, atração, confiança, ressentimento e reputação evoluem por ações e histórias compartilhadas.
4. **Sobrevivência material**: estoques reais, transporte, ferramentas, alimentação, abrigo e trabalho; nenhum recurso surge para disfarçar simulação.
5. **Mundo persistente, mas limitado**: indivíduos não desaparecem ao descarregar chunks; fidelidade da simulação varia com distância e relevância.
6. **Equilíbrio ecológico/demográfico**: escassez, doença simulada, migração, mortalidade e ataques produzem declínio; expansão não é inevitável.
7. **Autonomia offline**: não utilizar ChatGPT/Llama, inferência remota ou acesso à rede no loop de IA.

## Primeira experiência / laboratório
Cabana perto da área inicial, com três moradores permanentes **por mundo**. A/B são irmãos biológicos; B/C casal; A solteiro inicialmente. Podem construir, conversar, discordar e desenvolver vínculos com o jogador; não existem apenas como parceiros românticos predestinados. Morte e migração persistem.

## Experiência futura
Assentamentos esparsos com presets gerados por seed ao explorar:
- cabana isolada 1–2; tribo 3–6; vila 10–15; cidade 20–30; capital 30–50 habitantes iniciais.
- laboratório Trio da Cabana é exceção deliberada de 3 moradores.
- Estruturas iniciais procedurais; crescimento posterior com obras e materiais. Habitantes de regiões não descobertas não são instanciados globalmente.
- Viajantes, comerciantes, refugiados e migrantes conectam assentamentos; assentamentos podem dividir-se, tornar-se ruínas ou ser ocupados novamente.
- Invasões de mobs, inclusive ataques coordenados de zumbis, respeitam orçamento de simulação e condições da região.

## Interface
Balões de fala próximos e legíveis, interação explícita para conversas completas, opções contextuais, indicadores de compromissos; acessibilidade de toque e mouse/teclado desde a concepção. Sem afirmar suporte Android executável antes da prova.

## Não objetivos imediatos
Servidor dedicado, LAN, multiplayer, LLM, geração textual sem limites, história de mundo inteiro pré-simulada, batalhas gigantescas, cidade completa na primeira entrega. Testes in-game/MCP dependem de decisões posteriores.

## Tom e agência do jogador
Mundo vivo e crível, não utopia automática. NPCs podem discordar do jogador, proteger privacidade, cooperar ou recusar solicitações. Conflitos e consequências podem ser ajustados por opções de segurança para evitar perda imprevista de construções.
