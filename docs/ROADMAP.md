# Roadmap com portas de aceitação

**Estado geral:** planejamento documental. Nenhuma fase abaixo está validada.

| Fase | Resultado observável | Dependência / porta |
|---|---|---|
| 0 — Verificação técnica | Revisão pinada, mapa de hooks, plano de testes e restrições honestas | Fontes e ambiente do executor |
| 1 — Core Rust | IDs, estados, relógio, evento, RNG, persistência de fixture, invariantes testadas | Fase 0, sem jogo |
| 2 — Trio no Horizon Android | Uma cabana, 3 IDs únicos, vínculos, save/reload, sem duplicatas | **viabilidade de mod nativo Android comprovada** + hooks e save |
| 3 — Autonomia básica | Necessidades, tarefas, coleta, inventário real, construção, falhas recuperáveis | adaptador de ações validado |
| 4 — Sociedade V1 | memória, família, sessões de diálogo, interações, conflitos não obrigatórios | sistema de eventos + social |
| 5 — Assentamentos | templates, geração sob demanda, economia, população, ameaça e LOD | conservação + materialização |
| 6 — Cross-platform | adaptação para desktop além do Android e interfaces táteis/teclado | Android validado + prova técnica por plataforma |

## Critérios de passagem gerais
- Cada fase define invariantes e uma matriz de testes positivos, negativos, repetição e recuperação.
- Testes de Rust são evidência **unitária**, não evidência de funcionamento visual no Horizon.
- Uma fase bloqueada não autoriza afirmar que a próxima já funciona.
- Não abrir simultaneamente muitas frentes; encerrar integração anterior antes de avançar o escopo.

## Entregas sugeridas da fase 0
1. Identificar a versão específica do **Horizon Android** instalado (`dev.horizon.android`), seu suporte real a código nativo e compatibilidade com `horizon-mixins`; registrar commits/revisões de origem.
2. Verificar APIs concretas de tick, entidade, bloco, persistência e UI; citar arquivo e símbolo.
3. Definir opções de teste sem executá-las/desbloqueá-las automaticamente.
4. Registrar especificação mínima de tipos e invariantes para Fase 1.
5. Não criar um MCP customizado, nem ativar automações do Horizon sem decisão do usuário.

## Critério da primeira prova jogável
Três NPCs com identidades e vínculos corretos, uma única cabana em local seguro, save/reload consistente, pelo menos uma ação física consumindo recurso real e relatório reprodutível da integração. **Os demais sistemas são evolutivos**, não requisitos escondidos para essa primeira prova.
