# Contratos do domínio — esquema lógico preliminar

Estas estruturas **não são API Rust nem formato de save final**; representam campos/garantias a estabilizar por testes de domínio.

```text
WorldId       id estável do save
NpcId         id estável dentro do mundo
EntityHandle  referência efêmera do Horizon; pode desaparecer com unload
GenesisId     marcador único do Trio da Cabana
SettlementId  identidade persistente de assentamento
OperationId   chave idempotente de mutação
EventId       evento confirmado, causal e ordenado
Version       versão de esquema e semântica
```

## NpcRecord
`{world_id, npc_id, schema_version, alive_state, demographic_profile, personality, skills, needs, physical_location, region, residence_id, kinship_edges, romance_edges, social_edges, inventory_ref, knowledge_ref, memory_ref, intent, active_job, last_sim_tick, revision}`

- Estado vital: `ALIVE_ACTIVE`, `ALIVE_ABSTRACT`, `DEAD`; ausência física não apaga registro.
- Identidade e relações não derivam da renderização.
- Nascimento liga pais, gera um novo ID; parentesco não pode ter auto-relação, duplicata ou ciclo genealógico impossível.
- Morte desencadeia liquidação da tarefa, reservas, itens, vínculos e sucessão conforme política; nunca recriar por carregamento.

## SettlementRecord
`{id, generation_origin, region, stage, population_ids, property_claims, stockpiles, job_board, buildings, trade_routes, security, productive_capacity, social_rules, last_sim_tick, revision}`

- Estágio não obriga expansão; capacidade populacional decorre de moradias, alimentação e recursos.
- Template inicial e crescimento histórico são processos distintos.
- Regiões não vistas usam seed e gerador histórico **com limite** e não retroativamente modificam chunks vistos.

## Comandos / transações
`Command {operation_id, actor, target, expected_revision, Preconditions, Reservations, ProposedAction}`  
`Outcome {operation_id, success|failed|pending, actual_changes, error_reason}`  
`Event {event_id, cause_id?, operation_id?, tick, participants, facts, visibility_scope}`

Para `PlaceBlock`, validar posição, colisão, direito, alcance, material e reserva; tentar alteração física; confirmar e então ajustar estoque. Se cair entre efeitos, recuperar com journal e idempotência. Para ações multiobjeto, documentar compensação possível e limites do adaptador.

## Percepção, crença, memória
- `Fact` é observação confirmada pelo sistema; `Belief` é crença do NPC com fonte, confiança e tempo; `Rumor` pode ser falso.
- `Memory` prioriza eventos emocional/socialmente significativos; sumarização e esquecimento são explícitos, não deleção de consequências legais/parentais.
- Assuntos privados só circulam se o NPC decidir compartilhar, observada política de diálogos.

## Social
- Vínculo possui tipo (parentesco, romance, amizade, rivalidade, profissão), histórico e dimensões distintas (confiança, afeto, respeito, medo, ressentimento). Não usar uma barra única para todo relacionamento.
- Sessão de conversa tem `conversation_id`, participantes, assunto, turnos, interrupções e compromissos.
- Compromisso prometido não equivale a trabalho concluído; somente prova material o confirma.

## Governança do esquema
Nenhum formato persistido pode mudar silenciosamente: definir migração, testes de leitura/reescrita e backup. Mudança incompatível bloqueia o carregamento com erro recuperável, não tenta adivinhar os dados.
