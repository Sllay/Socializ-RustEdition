# ECO-001 — Economia material, tarefas e construções reais

## V1 — EM_REFINAMENTO

### Princípio de conservação
O NPC minera, derruba, coleta, carrega, troca, fabrica e coloca **blocos reais**. Estoques pessoais, familiares, de armazém e em trânsito devem ser registrados; nenhuma construção pode consumir mais do que existe.

### Cadeia exemplar
Árvore válida -> ferramenta e alcance -> ação de quebrar confirmada -> drops reais -> inventário de lenhador -> transporte -> entrega confirmada -> armazém -> fabricação com receita -> reserva do construtor -> colocação de bloco confirmada.

### Job Broker
Tarefas têm `job_id`, pré-condições, materiais, local, exigência de habilidade, prioridade, executante, dependências, riscos e prazo de reserva. `OFFERED/CLAIMED/RUNNING/DONE/FAILED/CANCELLED`; sem duplicação ao retomar. Ferramenta pode ser emprestada somente com autorização de posse.

### Reservas
Itens, estações de trabalho, blocos/posições e rotas estreitas são reservados com duração e prioridade; detectar deadlocks e liberar reserva em falha, morte ou descarregamento.

### Construção
Blueprint definido por dimensões, materiais, zonas, dependências e acessos. Etapas: planejamento do sítio, verificação de propriedade, limpeza autorizada, coleta, fundação, paredes, entrada, telhado, iluminação, inspeção de segurança. Uma obra não é "concluída" sem acessibilidade e uso real. Workers dividem subtarefas sem colocar o mesmo bloco duas vezes.

### Recuperação
Se o jogador modificar terreno durante obra, revalidar. Se o Horizon rejeitar `PlaceBlock`, não descontar material como se tivesse sido colocado. Se for interrompido no meio da gravação, reconcile journal + bloco atual + estoque; nunca insistir apagando mundo do jogador.

### Trabalhos e profissões
Morador escolhe com base em habilidade, necessidade, demanda, vontade e risco; profissão aumenta aptidão mas não impede trabalhos emergenciais. Transporte entre cidades exige tempo, inventário e rota.

### Testes
Dois construtores tentam usar mesmo stack; vários crafts com materiais limitados; queda em etapa de colocação; inventário do NPC morto; obra sem entrada não é declarada válida; propriedade do jogador bloqueia alterações.

## V2 — CAPTURADA
Produção organizada, comércio entre assentamentos, preços dinâmicos, contratos, armazenamento coletivo, ferramentas degradadas, reparos, estradas e engenharia de muralhas complexas.
