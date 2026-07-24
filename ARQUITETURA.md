# Arquitetura do Atlas

## Visão geral

O Atlas é dividido em três camadas independentes:

1. **CONTEXTO** — tudo o que o sistema precisa saber para agir.
2. **MEMÓRIA** — tudo o que aconteceu.
3. **HABILIDADES** — como o sistema age.

## 1. Camada de Contexto

Arquivos de constituição, regras e perfis que orientam o comportamento do sistema:

- `SOUL.md` — propósito, valores e restrições invioláveis.
- `RULES.md` — regras operacionais.
- `AGENTS.md` — definição dos perfis de agente.
- `ORCHESTRATOR.md` — system prompt e lógica de roteamento.
- `USER_COMPACT.md` / `USER_FULL.md` — perfil do usuário.

## 2. Camada de Memória

### Curto prazo

Registros diários, alertas ativos, contexto da semana e tendências em formação.

### Longo prazo

Dossiês históricos por pilar, padrões detectados e decisões arquivadas.

## 3. Camada de Habilidades

Cada skill é um conjunto de instruções e contexto especializado, padronizado em `SKILL.md`. Skills cobrem domínios específicos (saúde, finanças), coordenação (orchestrator, triggers) e registro (daily-writer, weekly-consolidator).

## Fluxo típico de interação

1. Usuário envia mensagem via Telegram.
2. Hermes Agent recebe e injeta contexto.
3. Orchestrator identifica o pilar e a skill adequada.
4. Skill processa a solicitação e atualiza a memória.
5. Resposta é enviada ao usuário.
6. `daily-writer` e `atlas-handoff` garantem persistência.

## Princípios de design

- **Privacidade por padrão**: dados pessoais permanecem fora deste repositório público.
- **Markdown como fonte da verdade**: tudo é legível, versionável e portátil.
- **Mínima fricção, máxima autonomia**: o sistema deve reduzir carga cognitiva.
- **Decisões baseadas em evidências**: mudanças importantes exigem ADRs.
