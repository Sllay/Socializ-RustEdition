# Procedimento de ideias e versões

A documentação não deve virar um cemitério de pequenas ideias nem um GDD impossível de manter.

## Onde registrar
1. Consultar `docs/IDEAS/INDEX.md` e o documento central do domínio.
2. Se assunto já existe, acrescentar seção nova à V1/V2 relevante.
3. Criar novo documento **apenas** quando não há domínio adequado.
4. GDD recebe uma frase de escopo; arquitetura recebe apenas contratos compartilhados; detalhes de estados e casos ficam em IDEAS.
5. Cada entrada contém ID, data, versão, estado, cenário, variáveis, estados, transições, falhas, limites, métricas e testes.

## Estados permitidos por versão
`CAPTURADA` -> `EM_REFINAMENTO` -> `V1_ESPECIFICADA` -> `EM_IMPLEMENTACAO` -> `IMPLEMENTADA_PENDENTE_INTEGRACAO` -> `INTEGRADA_PENDENTE_VALIDACAO` -> `VALIDADA`.
Extras: `BLOQUEADA`, `DESCARTADA`, `SUBSTITUIDA`.

A versão pode ser V1, V2, V3 etc.; `V1_ESPECIFICADA` é nome histórico do status de especificação e vale também para V2. Nunca alterar estado sem evidência.

## Políticas de priorização
- Limite inicial: no máximo 2 versões em `EM_IMPLEMENTACAO`.
- Versão implementada aguardando integração recebe prioridade sobre abrir novas frentes não essenciais.
- Se bloqueada, registrar causa, evidência e condição para desbloquear, não chamar de concluída.
- Antes de encerrar um ciclo, revisar índice, referências cruzadas e se há versões órfãs.

## Modelo de entrada
```text
ID / Versão / Estado / Data
Hipótese e benefício para experiência
Entradas observáveis e conhecimento disponível
Estados e transições (incluindo falhas)
Regras de integridade e recursos
Consequências em sistemas externos
Casos limite: morte, reload, distância, conflito
Testes: unitários, propriedade e game (quando aplicável)
Dependências, riscos, questões em aberto
Evidência/commit e próxima tarefa
```
