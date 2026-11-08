# UI-001 — Interações do jogador e interface PC/mobile

## V1 — EM_REFINAMENTO

### Alvo atual vs futuro
O único dispositivo do usuário é Android com Horizon instalado, mas o suporte `.hnmod` dessa build ainda não foi demonstrado. Priorizar **interface para toque** e testes isolados na cloud; compatibilidade PC é secundária e não substitui validação real no Android.

### Estados de interface
`NONE`: gameplay normal. `HOVER`: nome curto e indicador social se próximo e visível. `CONVERSATION`: painel de diálogo e escolhas derivadas do estado. `TRADE/TASK`: tela específica para troca ou compromisso. `CLOSED`: restaura input do jogo. Escapar, afastar-se ou ataque pode interromper conforme regra social.

### Interação
- Balões sobre NPCs próximos, com prioridade por relevância e limites de quantidade; não revelar informação privada através de balões que jogador não deveria ouvir.
- Diálogos completos apenas quando o jogador interage. Interrupções respondem ao vínculo e contexto.
- Opções só aparecem se contexto e regras permitem. Escolha confirmada gera evento concreto (promessa, oferta, pedido de ajuda, recusa) ou nada.
- Toda ação apresenta feedback: por que recusou, o que falta, onde está a tarefa, estado de relação quando visível.

### Acessibilidade e responsividade
Tela pequena: painel escalável, área de toque generosa, texto legível, rolagem e foco; PC: mouse e teclado, navegação e cancelamento. Sem bloquear controles básicos de movimento sem necessidade; respeitar configurações existentes do Horizon. Suporte a traduções/locais no futuro.

### Debug
Overlay desenvolvedor opcional por NpcId: objetivo atual, estado social, última decisão, reservas, localização, LOD, erros. Nunca mostrar esse overlay a jogadores por padrão nem alterar mundo ao inspecionar.

### Testes
Conversa não abre duplicada; opção indisponível não ativa efeito; balões não ocupam toda a tela; NPC distante não vaza segredo; teclado e mouse funcionam; design mobile não depende de hover/mouse-right. **Testes mobile reais ainda bloqueados.**

## V2 — CAPTURADA
Histórico contextual opcional, indicadores discretos de relações, atalhos de acessibilidade, UI de administração de cidade e modos de visualização de memória social.
