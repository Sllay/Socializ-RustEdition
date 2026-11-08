# DIA-001 — Diálogos procedurais contextuais, sem LLM

## V1 — EM_REFINAMENTO

### Proibição de atalhos
Não usar Llama, ChatGPT, API remota ou geração textual baseada em "NPC sabe tudo". Não produzir falas aleatórias sem objetivo social. Priorizar coerência e variedade limitada, verificável em testes.

### Pipeline
1. Estado do encontro: participantes, situação, atividades, memória compartilhada, distância e privacidade.
2. Selecionar intenção `GREET | INFORM | ASK | REQUEST_HELP | OFFER_HELP | WARN | THANK | APOLOGIZE | REFUSE | QUESTION | COMFORT | COMPLAIN | END`.
3. Avaliar permissões sociais: interlocutor disponível, relação, atenção, medo, segredo, segurança, idioma/gramática.
4. Escolher ato dialógico, tom e argumentos vindos **apenas de conhecimento do personagem**.
5. Realizar frase a partir de templates gramaticamente validados e variantes de personalidade.
6. Gerar opções dinâmicas do jogador por ações disponíveis, não por listas de respostas vazias.
7. Aplicar efeitos de diálogo **apenas após escolha/confirmação**: promessa, oferta, segredo, suspeita, ajuda ou troca material.

### Sessões e interrupções
`INVITED -> ACCEPTED -> ACTIVE -> INTERRUPTED | ENDED`, com `DECLINED` e `TIMED_OUT`. Personagem possui limites de atenção: não iniciar cinco sessões simultâneas. Chegada de amigo pode levar a convite, desconhecido a silêncio e rival a recusa ou discussão. Ataque suspende e pode encerrar conversa. O jogador pode se aproximar e ver balões; conversa completa exige interação, não invasão automática.

### Exemplo
Helena é amiga do jogador, está cansada e necessita 12 tábuas: intenção `REQUEST_HELP`, tópico telhado, tom acolhedor. "Ainda bem que você apareceu. Faltam doze tábuas para terminar o telhado." A resposta "Posso trazer" cria `Commitment` rastreado; **não** inventa tábuas nem conclui obra.

### Realização linguística
Separar `DialogueAct` de `PortugueseRenderer`, com concordância, pronomes, pessoa, número, flexão, tom, variações. Evitar frases contraditórias, spoilers ou diálogos repetidos; TTL por assunto, cooldown, memória da última fala e alternativas de silêncio. Textos podem ser localizados futuramente.

### Consequências
Prometer e não cumprir modifica confiança segundo gravidade e contexto. Contar segredo altera quem sabe. Acusar sem prova pode criar rumor. Pedir desculpas pode ou não resolver conflito.

### Testes
Mesmo estado/seed -> saída determinística; falta de conhecimento impede "vi seu roubo longe"; interrupção preserva sessão; falas variam com intimidade sem alterar verdade; as opções exibidas possuem efeitos implementáveis; balões têm limites de frequência.

## V2 — CAPTURADA
Conversa de grupo, fofoca em múltiplos saltos, memória de diálogo resumida, idioma/localização, brincadeiras, mal-entendidos, negociação e mediação de conflitos.
