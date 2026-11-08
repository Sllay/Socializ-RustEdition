# Fluxo eficiente de Codex

## Papéis
- Usuário: escolhe direção de gameplay e aprova mudanças de escopo.
- Assistente: formaliza ideias, contradições, estados, regras, critérios, prompts precisos e revisa evidências.
- Codex: implementa, testa, atualiza docs pertinentes e reporta fatos; não decide mecânicas não aprovadas sozinho.

## Uma tarefa por vez
1. Identificar ID/versão do domínio e o menor conjunto de arquivos relevantes.
2. Preparar plano curto com riscos e teste de aceitação.
3. Alterar o mínimo; não reescrever diretórios inteiros nem criar novos agentes automaticamente.
4. Rodar testes permitidos e registrar saída.
5. Revisar diff, regressão, estado das ideias e bloqueios.
6. Entregar relatório; criar commit apenas se autorizado na tarefa.

## Contexto e subagentes
- Ler `AGENTS.md` + documento específico + contrato/arquitetura essencial; evitar varrer todos os arquivos.
- Relatórios anteriores são evidência histórica, **não** prova do estado atual do checkout.
- Subagentes desativados por padrão. Usar somente para revisão independente ou bateria paralela claramente delimitada; sem agentes aninhados, sem duplicar tarefas.
- Se executor offline/sem recursos, apresentar bloqueio preciso; não inventar teste, branch, diff ou uso de MCP.

## Conexões e segurança
Não instalar MCP Horizon nem conectar ao jogo no início da Fase 0. Estudar opções no documento específico e trazer decisão ao usuário. Mudanças em dados persistentes exigem fixtures e backups, sem tocar em saves reais.

## Critério de conclusão
Uma tarefa é concluída quando código/artefato existe, testes são executados ou marcados com motivo de bloqueio, documentos e evidências estão atualizados, e o usuário consegue auditar o que mudou.
