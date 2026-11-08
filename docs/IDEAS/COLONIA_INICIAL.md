# GEN-001 — Laboratório Trio da Cabana

## V1 — EM_REFINAMENTO
**Objetivo:** disponibilizar um cenário permanente, rápido e reproduzível para testar família, romance, tarefas, diálogo, construção e persistência em single-player offline.

### Dados de fixture
- **A**: irmão/irmã biológico(a) de B. Inicialmente solteiro(a), sem romance predeterminado com o jogador.
- **B**: irmão/irmã biológico(a) de A; vínculo romântico inicial com C.
- **C**: não possui parentesco biológico com A/B; vínculo romântico inicial com B.
- Os três são adultos na fixture romântica inicial, evitando ambiguidades. Identidades, sexo, gênero, visual, habilidades, idades adultas e nomes podem ser parametrizados por fixture, sem limitar emprego ou personalidade por gênero.
- Relação A↔C é independente, podendo tornar-se amizade, rivalidade ou outra relação coerente.
- NPCs têm vontade própria; nunca tornar romance do jogador obrigatório ou programar aceitação automática.

### Semântica de existência
**Uma vez por WorldId**: criar exatamente um `GenesisId` e três `NpcId` após localizar posição segura. EntityHandles são efêmeros: ao relogar, **materializar os mesmos registros**, não gerar pessoas novas.
NPCs não precisam estar eternamente no chunk inicial: podem sair para trabalhar/migrar; não teleportar ao spawn. Morte legítima fica registrada; o laboratório pode ser reinicializado somente por ferramenta de desenvolvimento explícita em cópia isolada do save.

### Seleção da cabana
Tentar dentro do chunk inicial/alcance de renderização; checar apoio firme, espaço para porta, cama, acesso, bioma adequado, água/lava/precipício, colisão com estruturas e alterações de jogador. Se não houver espaço, busca determinística em raio pequeno configurável, registrando justificativa. Nunca forçar sobrescrita para manter "mesmo chunk" a qualquer custo.

### Máquina de estados Genesis
`NOT_SEEN -> SITE_CANDIDATE -> RESERVED -> BUILDING -> READY`, com `BLOCKED` / `RECOVERING`.
- `NOT_SEEN`: mundo não inicializado; operação determinística por `WorldId`.
- `SITE_CANDIDATE`: posição válida calculada, ainda sem efeitos.
- `RESERVED`: área registrada, com `OperationId` exclusivo.
- `BUILDING`: aplicar estrutura, registrar blocos por lote e compensação.
- `READY`: IDs da cabana e moradores confirmados.
- `RECOVERING`: crash no meio; inspecionar blocos existentes e journal, completar ou reverter sem duplicar.
- `BLOCKED`: falta de lugar seguro ou hook não disponível; emitir diagnóstico, preservar save.

### Testes obrigatórios
100x abrir mesmo mundo -> 1 cabana, 3 IDs e relações corretas; 2 mundos -> fixtures isoladas; morte/reload preserva morte; mudança de residência não "reseta"; mundo antigo cheio de estruturas não é destruído; crash entre reserva e build é recuperável; reiniciar durante nomeação não duplica entidade.

### Limites
A cabana de laboratório tem **3** moradores por escolha de teste, exceção ao futuro preset cabana normal **1–2**. Não iniciar centenas de assentamentos ou gerar entidades pelo mundo nesta etapa.

## V2 — CAPTURADA
Personalidades iniciais configuráveis, rotinas de manhã/noite, ocupações diferenciadas, animações sociais e visual variado. Não implementar antes de estabilizar V1 e seus testes.
