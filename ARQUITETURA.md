# Arquitetura do Atlas

## Visão geral

O Atlas é dividido em três camadas independentes:

1. **CONTEXTO** — tudo o que o sistema precisa saber para agir.
2. **MEMÓRIA** — tudo o que aconteceu.
3. **HABILIDADES** — como o sistema age.

Além disso, o sistema é executado por **5 perfis Hermes Agent** (1 Orchestrator + 4 workers) e mantido por **13 cron jobs** que rodam 24/7.

## 1. Camada de Contexto

Arquivos de constituição, regras e perfis que orientam o comportamento do sistema:

- `SOUL.md` — propósito, valores e restrições invioláveis.
- `RULES.md` — regras operacionais.
- `AGENTS.md` — definição dos 5 perfis de agente.
- `ORCHESTRATOR.md` — system prompt e lógica de roteamento.
- `USER_COMPACT.md` / `USER_FULL.md` — perfil do usuário.

## 2. Camada de Memória

### Curto prazo

Registros diários, alertas ativos, contexto da semana e tendências em formação. Atualizado pelos 13 cron jobs.

### Longo prazo

Dossiês históricos por pilar, padrões detectados e decisões arquivadas.

## 3. Camada de Habilidades

Cada skill é um conjunto de instruções e contexto especializado, padronizado em `SKILL.md`. São 11 skills custom ativas.

## Execução multi-agente

| Perfil | Função |
|---|---|
| `atlas-orchestrator` | Roteia, prioriza e decide quando chamar workers |
| `atlas-p1-monitor` | Worker do pilar Saúde |
| `atlas-p4-analista` | Worker analítico do pilar Finanças |
| `atlas-p4-operacional` | Worker operacional do pilar Finanças |
| `atlas-p2-dev` | Worker do pilar Desenvolvimento (Fase 2) |

## Cron jobs 24/7

- Heartbeats cross-pilar
- Daily writer
- Weekly consolidator
- Cross-pilar triggers
- Sincronização com GitHub
- Outras rotinas de manutenção de memória

## Fluxo típico de interação

1. Usuário envia mensagem via Telegram.
2. Hermes Agent recebe e injeta contexto.
3. Orchestrator identifica o pilar e a skill adequada.
4. Skill processa a solicitação e atualiza a memória.
5. Resposta é enviada ao usuário.
6. `daily-writer` e `atlas-handoff` garantem persistência.

## Decisões documentadas

O sistema possui **22 ADRs** (Architecture Decision Records) rastreando escolhas importantes, como a migração do pipeline Python de 6 passos, a adoção do Hermes Agent e a separação em 5 pilares.

## Princípios de design

- **Privacidade por padrão**: dados pessoais permanecem fora deste repositório público.
- **Markdown como fonte da verdade**: tudo é legível, versionável e portátil.
- **Mínima fricção, máxima autonomia**: o sistema deve reduzir carga cognitiva.
- **Decisões baseadas em evidências**: mudanças importantes exigem ADRs.
