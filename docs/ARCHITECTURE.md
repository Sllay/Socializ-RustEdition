# Arquitetura — proposta de fronteiras

**Estado:** design a validar contra código-fonte e uma revisão fixa do Horizon.

## Camadas / crates propostos
```text
lc-core          IDs, relógio lógico, comandos, eventos, regras e persistência
lc-ai            percepção, crenças, necessidades, Utility AI, GOAP/HTN, tarefas, navegação
lc-social        vínculos, memória episódica, conversas, cultura e conflitos
lc-world         terreno, direitos, estoques, manufatura, obras, ecologia, população e ameaças
lc-simulation    scheduler, níveis de fidelidade, materialização, métricas, fixtures
lc-horizon       adaptador mínimo para hooks, blocos, entidades, HUD, save e entrada
```
O adaptador conhece `lc-core`; o núcleo **não** conhece tipos internos de Horizon. Não criar as crates antes de confirmar interfaces e prioridades.

## Pipeline de tick lógico
1. Coletar observações do jogo, com identidades e timestamp; deduplicar.
2. Atualizar necessidades, memórias, conhecimento e eventos.
3. Decidir apenas quando vencido prazo de replanejamento, quando houve interrupção importante ou evento crítico.
4. Planejar / negociar empregos / reservar recursos e posições.
5. Validar pré-condições, permissões, alcance, inventário e dependências.
6. Adaptador tenta a ação física; **somente sucesso confirmado** aplica consequência lógica.
7. Commit do evento e das quantidades; registrar métricas. Falha libera reservas e produz motivo para nova decisão.

## Regras invariantes
- Exatamente um `NpcRecord` por `(WorldId,NpcId)`; entidade renderizada é handle efêmero.
- A cabana inicial tem um `GenesisId` por mundo; reiniciar não cria nova família ou habitação.
- Falecer é estado persistente, descarregar não equivale a falecer, morrer não obriga substituição.
- Itens e blocos nunca surgem por duplicação de operações; resultados idempotentes por `OperationId`.
- NPC sabe somente o que percebeu, viveu ou recebeu por relato; rumores não equivalem à verdade.
- Nenhuma mudança física sem checagem de terreno/permissão e registro de procedência.
- Reserva de tarefa/item/espaço tem duração, dono e liberação por falha/morte.
- Mesma seed + mundo inicial + versão + sequência de comandos -> mesmo estado lógico.
- O jogador não perde estruturas em regiões desconhecidas por materialização de planejamento abstrato.
- Mudança de LOD preserva IDs, inventários, vínculos, posição coerente, tarefas e conservação de recursos.
- População varia por natalidade, morte, migração e condições; não há crescimento descontrolado nem despawn usado como controle demográfico.

## Relógio / RNG
Relógio lógico ligado ao mundo; não avançar quando o jogo estiver fechado na V1. RNG particionado por seed mundial, sistema, entidade/evento e passo lógico; ordem de atualização estável. Evitar resultados diferentes por concorrência ou reordenação de tarefas.

## Scheduler / orçamento
IA, navegação e economia usam filas com orçamento por tick. Prioridades altas: dano, perigo imediato, ação física em andamento. Menores: decoração, trabalhos triviais e eventos distantes. Separar planejamento em dados imutáveis do commit no mundo. Frequências e limites serão calibrados por benchmark, não estimados como fatos.

## Três níveis de simulação
- **Ativo:** entidades físicas, navegação local, blocos e interações reais.
- **Regional:** viagens, recursos e compromissos agregados com eventos rastreáveis.
- **Estratégico:** crescimento/declínio e economia de assentamentos em intervalos maiores.
Interest Manager considera distância, vínculos com jogador, perigo, visibilidade e relevância. Histerese impede descarrega/recarrega contínuo. Materialização pausa região, reconcilia recursos e terreno, instancia entidades e retoma execução. **Não alterar chunks distantes por suposição.**

## Persistência
Snapshots versionados, log compacto de eventos e `OperationId` idempotente; recuperação de operação parcialmente aplicada; backups de saves de teste. Atomicidade entre save do jogo e dados do mod **não comprovada**: especificar protocolo de reconciliação só após auditoria do Horizon.

## Segurança
Operações destrutivas exigem validação de propriedade, distância, integridade estrutural e opção do jogador. UI móvel só será declarada compatível após testes reais. Código nativo tem privilégios do usuário do processo: auditar dependências e ferramentas.
