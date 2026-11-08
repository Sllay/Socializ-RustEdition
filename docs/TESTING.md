# Estratégia de testes e observabilidade

Não existem testes de runtime executados ainda; isto é uma **matriz de aceitação futura**.

## Níveis
1. **Unitários Rust:** estado, transições, decisões, prioridades, genealogia, texto procedural e eventos.
2. **Propriedades:** simular milhares de ações geradas para detectar duplicação, deadlock e estados impossíveis.
3. **Determinismo:** mesma seed, versão, entrada e sequência de ações -> mesmo hash lógico; threads e relógio real não devem contaminar o resultado.
4. **Persistência:** snapshot -> crash simulado -> recovery -> compare; operações idempotentes.
5. **Adaptador:** verificar hooks e efeitos físicos com fixture isolada, se ambiente real estiver disponível.
6. **UI visual:** screenshots e interações de mouse/teclado; toque/Android só com ambiente/dispositivo realmente comprovado.
7. **Performance:** medir CPU/tempo por tick, RAM, filas, pathfinding, número de NPCs ativos vs abstratos, tempo de load/save.

## Matriz principal
| Caso | Critério |
|---|---|
| Inicializar 100 vezes mesmo mundo | 1 Genesis, 1 cabana, 3 NpcIds, nenhum reset indevido |
| Criar mundo novo | Trio distinto do mundo anterior |
| NPC morre e jogo reinicia | Continuar morto, sem substituição automática |
| NPC migra para longe | Persistir rota/posição e não voltar ao spawn |
| Interromper save durante construção | Não criar/destroçar blocos ou materiais sem reconciliação |
| 10 construtores, 20 tábuas | Gastos confirmados não excedem estoque |
| Estrutura do jogador ocupa spawn | Buscar local alternativo, nunca sobrescrever |
| Assunto interrompido em conversa | Estado social coerente; sem sessões duplicadas |
| Notícia falsa via rumor | NPC não converte automaticamente crença em fato |
| 2 NPCs requisitam mesma estação | Reserva e timeout funcionam |
| Caminho fechado enquanto NPC anda | Replanejar com limite, liberar reserva |
| Regiões alternam LOD repetidamente | Sem IDs, itens ou tarefas duplicadas |
| Falta alimento em vila | Nascimento não cresce indefinidamente; efeitos causais |
| Mobs atacam vila distante | Perdas limitadas por recursos e regras, registro de causalidade |
| Código compila mas jogo não inicia | NÃO marcar integrada/validada |
| Cliente Android não aceita hnmod | Bloquear etapa de port, não maquiar o erro |

## Instrumentação
Inspector opcional por `NpcId`: objetivo, pontuações, crenças, necessidades, tarefa, reservas, histórico de falhas, caminho e último evento. Limitar logs; usar amostragem e IDs para correlacionar.

## Evidência
Toda validação deve conter comando executado, ambiente, versão, saída, screenshot quando apropriado, interpretação e limites. Separar `PASS`, `FAIL`, `BLOCKED` e `NOT_RUN`. Nunca inventar números de TPS ou players suportados.

## Segurança de teste
Criar fixture isolada e cópia descartável do mundo; desativar qualquer comando destrutivo sobre saves reais. Teste headless não substitui testes visuais. MCP e conectores permanecem sob decisão pendente conforme `docs/OPERATIONS/MCP_RESEARCH.md`.
