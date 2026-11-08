# Índice de ideias — fonte de verdade de status

A versão descreve **maturidade da ideia**, não versão do mod. Nenhuma feature abaixo está implementada. Consulte [processo](../OPERATIONS/IDEA_WORKFLOW.md).

Estados: `CAPTURADA`, `EM_REFINAMENTO`, `V1_ESPECIFICADA` (também para V2), `EM_IMPLEMENTACAO`, `IMPLEMENTADA_PENDENTE_INTEGRACAO`, `INTEGRADA_PENDENTE_VALIDACAO`, `VALIDADA`, `BLOQUEADA`, `DESCARTADA`, `SUBSTITUIDA`.

| ID | Documento central | V1 | V2 | Dependências principais |
|---|---|---|---|---|
| GEN-001 | [Trio da Cabana](COLONIA_INICIAL.md) | EM_REFINAMENTO | CAPTURADA | IDs, integração, spawn, save |
| AI-001 | [Agente individual](INTELIGENCIA_INDIVIDUAL.md) | EM_REFINAMENTO | CAPTURADA | tempo, conhecimento, scheduler |
| SOC-001 | [Família e sociedade](FAMILIA_E_SOCIEDADE.md) | EM_REFINAMENTO | CAPTURADA | eventos, memória, identidade |
| DIA-001 | [Diálogos](DIALOGOS.md) | EM_REFINAMENTO | CAPTURADA | SOC-001, AI-001, UI |
| CON-001 | [Conflitos e combate](CONFLITOS_E_COMBATE.md) | EM_REFINAMENTO | CAPTURADA | SOC-001, propriedade, IA |
| ECO-001 | [Economia e obras](ECONOMIA_E_CONSTRUCAO.md) | EM_REFINAMENTO | CAPTURADA | comandos, recursos, navegação |
| POP-001 | [Assentamentos e população](ASSENTAMENTOS_E_POPULACAO.md) | EM_REFINAMENTO | CAPTURADA | economia, regiões, nascimento |
| LOD-001 | [Mundo distante](SIMULACAO_DISTANTE.md) | EM_REFINAMENTO | CAPTURADA | snapshots, reconciliação |
| ENV-001 | [Ecologia e ameaças](ECOLOGIA_E_AMEACAS.md) | EM_REFINAMENTO | CAPTURADA | recursos, segurança, eventos |
| UI-001 | [Interface e jogador](INTERFACE_E_JOGADOR.md) | EM_REFINAMENTO | CAPTURADA | diálogo, compatibilidade |

## Disciplina
- Nova ideia casual entra **no documento central** já apropriado; criar arquivo novo somente se o domínio realmente não existir.
- Uma V2 pode permanecer capturada enquanto V1 está validada. Versões independentes.
- Cada status alterado precisa registrar evidência ou decisão. Não transformar uma hipótese em fato ou código testado.
- Duas ideias no máximo `EM_IMPLEMENTACAO`; priorizar integração de versões já implementadas.
- Uma ideia não implementada não deve ganhar fake screenshot ou números inventados de desempenho.

## Próximas decisões a refinar
GEN-001 raio de busca seguro; AI-001 taxa de replanejamento; DIA-001 cobertura linguística; CON-001 limites de risco; POP-001 calendários/biologia; LOD-001 convergência e transações; ENV-001 ataque justo; UI-001 toque Android condicionado à viabilidade nativa.
