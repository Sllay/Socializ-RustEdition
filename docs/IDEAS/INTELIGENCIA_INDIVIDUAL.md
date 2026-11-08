# AI-001 — Autonomia individual e resolução de tarefas

## V1 — EM_REFINAMENTO

### Modelo de agente
`Perception -> Belief/Memory -> Need -> Goal -> Plan -> Reservation -> Validation -> Physical Action -> Commit -> Feedback`.
Agente tem necessidades (comida, sono, abrigo, segurança, convivência), habilidades, preferências, inventário, ferramentas, conhecimentos, tarefas, emoções e limitações de tempo.

### Seleção de objetivos
Utility AI pontua alternativas por urgência, custo, risco, capacidade, compromissos e relevância social. Normalizar pesos, registrar razões e usar **histerese**: o NPC não abandona objetivo porque outra opção pontuou 0,01 a mais. Emergências interrompem trabalhos; recuperações e cooldowns limitam oscilações.

### Planejamento
- GOAP: ações com pré-condições e efeitos (ter madeira -> construir; falta de madeira -> cortar árvore -> transportar).
- HTN: decompor "construir casa" em terreno, materiais, fundação, acesso, paredes, telhado, inspeção.
- Behavior Tree/rotina de execução: caminhar, interagir, esperar, reagir a perigo.
- Não forçar todas tecnologias desde V1: introduzir somente algoritmos necessários, mantendo interfaces intercambiáveis.

### Capacidade limitada
NPC não pode conhecer depósitos ainda não descobertos, nem teleportar para recursos. Se ferramenta indisponível: criar subobjetivo de fabricação, empréstimo, comércio ou substituição. Limitar tentativas, registrar erro, recuperar estado e liberar reservas.

### Rotina e atenção
Sono, trabalho, lazer, relações, horários flexíveis, descanso e pausas; atenção limitada a eventos importantes. Percepção por visão/audição/proximidade, sem leitura onisciente de estado do mundo. Memória significativa e crenças com confiança; rumores podem ser incorretos.

### Navegação
Dois níveis: grafo regional entre lugares e navegação local em blocos. A* com cache/invalidação por mudanças do terreno. Verificar portas, altura, água, perigos, permissões e capacidade. Regra de recuperação: caminho obstruído -> replanejar limitado -> cancelar com diagnóstico se necessário. No LOD abstrato, viagem é representada por rota e tempo, não teleporte físico visível.

### Job Broker
Trabalhos possuem prioridade, local, esforço, recursos, dependências, duração estimada, dono opcional e estado. `OFFERED -> CLAIMED -> RUNNING -> DONE`, alternativas `FAILED`, `CANCELLED`, `EXPIRED`. Reserva expira; NPC morto libera tarefa. Profissão influencia preferência e habilidade, não bloqueia outras atividades.

### Testes
Fome vence trabalho decorativo; promessa importante supera trabalho trivial sem perigo; falta madeira leva a coleta e não geração; falha de rota não trava agente; duas estações disputadas não geram deadlock; qualquer saída é explicável por métricas.

## V2 — CAPTURADA
Aprendizagem de habilidades por experiência, especialização dinâmica, hábitos culturais, lembranças de rotas seguras e objetivos de longo prazo entre cidades.
