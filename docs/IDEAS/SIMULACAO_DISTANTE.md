# LOD-001 — Simulação distante, persistência e reconciliação

## V1 — EM_REFINAMENTO

### Motivação
Não manter centenas de entidades físicas em chunks descarregados. Evitar o oposto: apagar personagens e seus acontecimentos por desempenho.

### Níveis
- **ACTIVE**: blocos, colisão, animação, percepção, diálogo e pathfinding local reais.
- **REGIONAL**: trabalhos, viagens, estoque e eventos por intervalos; indivíduos persistem em registros; alguns eventos sociais conservam maior detalhe.
- **STRATEGIC**: produção/consumo, risco, demografia e obras por agregados regionais, com eventos verificáveis.

### Interesse
Prioridade por proximidade, observação, ameaça, relações com jogador, importância narrativa e compromissos. Familiar muito querido deve manter contexto social mais detalhado, **não chunk físico carregado eternamente**. Faixas de distância e intervalos são parâmetros a medir. Histerese limita thrashing.

### Desmaterializar
Concluir/registrar operações pendentes, capturar inventário/local, liberar handle físico, manter record + tarefa + reservas válidas ou expiradas. Não inventar posição próxima ao jogador.

### Materializar
Travar estado regional, validar timestamp e recursos; reavaliar claims, estado de blocos, opções de caminho e operações pendentes; aplicar mudanças autorizadas gradualmente; criar entidades dos IDs existentes; iniciar rotina na posição coerente. Nenhuma mudança sobrescreve terreno alterado pelo jogador.

### Construções abstratas
Manter `BuildingPlan`, materiais reservados e progresso econômico. Obras **não são consideradas blocos efetivos** até aplicação validada. Se terreno mudou, replanejar ou suspender; crédito de material ajustado sem duplicação.

### Salvamento
Snapshot versionado + eventos compactados + IDs de operação. Se falha entre salvar chunks e mod, reconciliação por journal e inspeção; **não prometer atomicidade global** sem contrato de save do Horizon. Mundo não avança enquanto fechado na V1.

### Testes
Duas transições ACTIVE↔REGIONAL↔STRATEGIC -> mesmo NPC/itens; 100 aproximações e afastamentos -> nenhuma duplicação; personagem morto longe não renasce; mudança de blocos pelo jogador prevalece; mundo salvo durante transição recupera; eventos distantes não se tornam magicamente conhecidos.

## V2 — CAPTURADA
Simulação histórica de grandes regiões com compactação adaptativa, agendamento orientado por eventos, grupos de viajantes e proveniência de alterações físicas diferidas.
