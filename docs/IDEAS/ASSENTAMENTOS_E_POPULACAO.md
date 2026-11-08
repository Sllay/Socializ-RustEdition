# POP-001 — Assentamentos esparsos, demografia e sociedades

## V1 — EM_REFINAMENTO

### Presets de população na descoberta
| Tipo | População inicial | Exemplo |
|---|---:|---|
| Cabana isolada | 1–2 | lenhador, caçador, eremita |
| Tribo/acampamento | 3–6 | coleta e organização simples |
| Vila | 10–15 | agricultura, ofícios e comércio |
| Cidade | 20–30 | distribuição de trabalho e guardas |
| Capital | 30–50 | instituições, comércio e defesa |

**O Trio da Cabana (3) é exceção fixa de teste.** Os números são faixas de início, não hardcaps de civilização. Controlar expansão por suporte de recursos, espaço e orçamento de simulação.

### Geração contextual
Seed + bioma + topografia + água + recursos + distância de outros assentamentos -> candidato a estrutura; não materializar NPCs globalmente. Região `UNSEEN` preserva apenas potencial determinístico; visita inicial fixa identidade e estado. Mundo já visitado pelo jogador não recebe "passado" que sobrescreva obras.

### História sob demanda
Em região nunca descoberta, cidade pode ter trajetória inicial plausível (idade, infraestrutura, perdas, vínculos). Histórias geradas são **bootstrap**, não afirmação de 200 dias de simulação individual. Registrar origem; evitar contradizer locais/tempos já observados pelo jogador.

### Demografia
Nascimento requer adultos elegíveis, relações adequadas, espaço e condições sociais; taxas definidas por calendário/biologia ainda abertas. Crescimento tem alimentos, moradia, segurança, saúde, migração, mortalidade e envelhecimento como controles. Crianças não geram trabalhadores adultos instantaneamente. População não some por descarregamento; indivíduos podem migrar ou morrer por eventos causais.

### Migração / viajantes
Viajantes possuem origem, destino, motivo, inventário e rota. Podem visitar, comerciar, juntar-se a comunidade, fundar vila ou deixar sociedade em crise. Mudança de residência altera serviços/estoque, não ID nem vínculos familiares.

### Sociedade não linear
Cidade sem água/segurança pode perder população, sofrer revoltas, ser abandonada, voltar a ser ocupada; uma pequena vila pode estabilizar por longo tempo sem nunca virar capital. Decadência produz ruínas persistentes, não limpeza mágica.

### Testes
Seed estável -> candidatos estáveis; reentrar mundo não gera novamente; até milhares de assentamentos **potenciais** não resultam em milhares de entidades; fome impede crescimento infinito; colônia pode declinar; viajante não vira NPC duplicado.

## V2 — CAPTURADA
Governança, eleição/sucessão, cultura, leis locais, impostos, facções, colonização, refugiados, diplomacia, crises e disputas por território.
