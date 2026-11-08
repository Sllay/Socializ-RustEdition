# CON-001 — Intrigas, escalada e combate social

## V1 — EM_REFINAMENTO

### Objetivo
Brigas não surgem por sorteio arbitrário; devem ter causa, percepção, intenção e oportunidade. Comportamentos violentos são possíveis, mas a solução mais comum deve variar entre conversa, negociação, afastamento ou intervenção.

### Gatilhos
Suspeita de roubo; dano a propriedade; promessa quebrada; ofensa interpretada; rivalidade; ciúme contextual (não automático); disputa por trabalho; agressão anterior; mentira descoberta; disputa por limites territoriais; defesa de familiar; ameaça física.

### Variáveis
Percepção do evento; confiabilidade da fonte; perdas reais; temperamento/agressividade; autocontrole; confiança; vínculo familiar; cansaço/fome; testemunhas; perigo percebido; presença de guardas; custo de violência; gravidade da ofensa; possibilidade de reparação. Escalas devem ser calibradas, não fixadas agora.

### Máquina de estados
`CALM -> NOTICE -> INVESTIGATE -> DISCUSS -> NEGOTIATE -> RESOLVED`; alternativas `WITHDRAW`, `ANGER`, `THREATEN`, `FIGHT`, `ESCAPE`, `GUARD_INTERVENTION`, `AFTERMATH`. A transição não é forçada: falta de prova pode reduzir suspeita; entrega de item pode resolver; mediação de terceiro muda probabilidades; ameaça pública pode aumentar medo/reputação negativa.

### Exemplo laboratório
C percebe ferramenta desaparecida, suspeita de A, cuja irmã B é parceira romântica de C. Se A emprestou legalmente, evidência desmonta suspeita. Se A roubou, C pode questionar, pedir devolução, buscar ajuda, retirar confiança ou brigar. B pode mediar ou defender alguém; não é compelida a tomar partido do irmão ou parceiro. Resultado alimenta memória e história.

### Combate físico
Necessita alcance, objetivo, defesa, cooldown, perigo, estado de saúde, equipamento e custo. NPC avalia risco e pode fugir, pedir socorro, tentar separar combatentes ou rendição. Combate precisa respeitar dano real do motor, morte persistente, reação de outros NPCs e normas locais. Armas ou hostilidade não aparecem magicamente.

### Pós-conflito
Reputação, laços afetivos, sanções sociais, dívida/restituição, lesão, luto e mudança de tarefas. Nunca apagar consequência simplesmente porque o NPC descarregou.

### Segurança
Proteção configurável de criações do jogador; agressão não autorizada não quebra blocos protegidos. Evitar combate repetitivo gerado por um único insulto. Um conflito termina ou entra em cooldown verificável.

### Testes
Sem prova = suspeita não vira fato; objeto devolvido pode desescalar; A/B parentesco e B/C romance coexistem com mediação; combatentes feridos podem interromper; NPC morto não reaparece; combate longe usa LOD com resultados reconciliáveis.

## V2 — CAPTURADA
Crimes investigáveis, guardas, testemunhas, justiça local, duelistas, facções, guerras, consequências políticas e reconciliação longa. Não implementar V2 como efeito oculto da V1.
