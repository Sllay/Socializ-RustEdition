# Rascunho de prompt — Fase 1 (AINDA NÃO AUTORIZADO)

**Dependência:** auditoria Fase 0 com revisão técnica validada e decisões sobre formatos de dados.

Criar somente núcleo Rust independente do Horizon para `WorldId`, `NpcId`, `GenesisId`, estados vitais, relacionamentos de A/B/C, relógio determinístico, eventos e round-trip de persistência de fixture. Implementar testes que demonstrem:
- 100 inicializações mesmo mundo -> exatamente três IDs e um Genesis;
- A/B irmãos biológicos, B/C casal, A solteiro no início;
- sexo/gênero não força profissão nem personalidade;
- morte/reload não ressuscita; descarregamento não apaga;
- operação repetida é idempotente;
- duas seeds/mundos isolados não vazam registros.

Não criar engine Horizon, mundo, UI, MCP, entidades, sistema de spawn físico ou servidor. Se algum contrato for impossível, registrar bloqueio e trazer decisão ao usuário. Nunca reportar runtime in-game apenas com sucesso do `cargo test`.

Estado: **RASCUNHO**, não executar automaticamente.
