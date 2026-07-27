# Atlas — Sistema Cognitivo Multi-Agente

> Um copiloto pessoal que lembra, coordena e age através de agentes especializados, com memória persistente em Markdown.

---

## O problema

Modelos de linguagem esquecem o contexto a cada nova conversa. Agentes isolados resolvem tarefas pontuais, mas não conversam entre si. Ferramentas de produtividade não entendem a vida do usuário como um sistema integrado.

O resultado: repetição, perda de insights e decisões tomadas sem memória do que realmente importa.

## A solução

**Atlas** é um sistema cognitivo pessoal construído em torno de três princípios:

1. **Memória persistente** — tudo vive em Markdown versionado no GitHub.
2. **Orquestração multi-agente** — um orchestrador central roteia decisões para agentes especializados.
3. **Vida organizada em pilares** — saúde, desenvolvimento, relações, finanças e propósito, cada um com sua própria skill.

## Arquitetura multi-agente

O Atlas não é um único prompt. É um **sistema de 5 perfis Hermes Agent** trabalhando em conjunto:

| Perfil | Papel | Onde está documentado |
|---|---|---|
| `atlas-orchestrator` | Roteia interações e resolve conflitos cross-pilar | `_SISTEMA/ORCHESTRATOR.md` |
| `atlas-p1-monitor` | Worker de monitoramento de saúde | `_SISTEMA/AGENTS.md` |
| `atlas-p1-terapeutico` | Worker de apoio terapêutico | `_SISTEMA/AGENTS.md` |
| `atlas-p4-analista` | Worker analítico de finanças | `_SISTEMA/AGENTS.md` |
| `atlas-p4-operacional` | Worker de execução financeira | `_SISTEMA/AGENTS.md` |
| `atlas-p2-dev` | Worker de desenvolvimento e portfólio *(Fase 2)* | `_SISTEMA/AGENTS.md` |

Abaixo, o fluxo completo mostrando as três camadas (contexto, memória, habilidades), o gateway Hermes e a persistência em Git:

```
┌─────────────────────────────────────┐
│         USUÁRIO via Telegram        │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│      HERMES AGENT — Gateway 24/7    │
│   Telegram + Cron + Voice + LLM     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│     5 PERFIS HERMES AGENT ATIVOS    │
│  Orchestrator │ P1-Monitor│ P1-Terap│
│  P4-Analista  │ P4-Operacional      │
├─────────────────────────────────────┤
│     P2-Dev (Fase 2) — planejado     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│       ORQUESTRADOR CENTRAL          │
│  roteia · contexto · triggers · ADRs│
└──────────────┬──────────────────────┘
               │
    ┌──────────┼──────────┐
    ▼          ▼          ▼
┌───────┐  ┌───────┐  ┌──────────────┐
│CONTEXTO│  │MEMÓRIA│  │ HABILIDADES  │
│_SISTEMA│  │MEMORIA│  │ HABILIDADES/ │
│       │  │       │  │              │
│SOUL   │  │curto  │  │p1-saude      │
│RULES  │  │longo  │  │p4-financas   │
│AGENTS │  │       │  │p4-validacao  │
│ORCH   │  │13 cron│  │context-inj.  │
│USER   │  │jobs   │  │cross-pilar   │
│       │  │       │  │heartbeat     │
│22 ADRs│  │       │  │daily-writer  │
│       │  │       │  │weekly-consol.│
│       │  │       │  │atlas-handoff │
│       │  │       │  │conflito-dec. │
└───────┘  └───────┘  └──────────────┘
    │          │          │
    └──────────┴──────────┘
               │
               ▼
┌─────────────────────────────────────┐
│   RESPOSTA + PERSISTÊNCIA (Git)     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│         USUÁRIO via Telegram        │
└─────────────────────────────────────┘
```

### Onde estão documentados os componentes principais

| Componente | Localização |
|---|---|
| **5 perfis Hermes Agent** | `_SISTEMA/AGENTS.md` |
| **System prompt do Orchestrator** | `_SISTEMA/ORCHESTRATOR.md` |
| **Constituição e regras** | `_SISTEMA/SOUL.md` e `_SISTEMA/RULES.md` |
| **13 cron jobs** | `_SISTEMA/BOOTSTRAP.md` e `_SISTEMA/ORCHESTRATOR.md` |
| **22 ADRs** | `MEMORIA/curto_prazo/decisoes/` |
| **Memória curta prazo** | `MEMORIA/curto_prazo/` |
| **Memória longo prazo** | `MEMORIA/longo_prazo/` |
| **Skills custom** | `HABILIDADES/<skill-name>/SKILL.md` |

## Infraestrutura em Produção

| Componente | Quantidade |
|---|---|
| **Perfis Hermes Agent** | 5 (1 Orchestrator + 4 workers especializados) |
| **Skills custom** | 11 (formato SKILL.md) |
| **Cron jobs 24/7** | 13 (heartbeats, daily writer, triggers cross-pilar) |
| **ADRs documentadas** | 22 (decisões de arquitetura rastreadas e versionadas) |
| **Pilares ativos** | P1 (Saúde) + P4 (Finanças) |
| **Interface** | Telegram (gateway nativo) |
| **Stack** | VPS Linux + Hermes Agent + GitHub + Telegram |
| **LLM** | DeepSeek V4 Pro + Gemini 2.5 Flash (fallback) |
| **Hospedagem** | Integrator Linux Pura — 4 vCPU · 5.8 GB RAM · 99 GB SSD · Ubuntu 26.04 LTS |

## Habilidades ativas

| Skill | Função |
|---|---|
| `orchestrator` | Roteia interações, resolve conflitos cross-pilar e mantém o Kanban |
| `p1-saude` | Monitoramento de indicadores de saúde mental e física |
| `p4-financas` | Acompanhamento semanal de operações e decisões financeiras |
| `p4-validacao-financeira` | Validação de valores e transações acima de thresholds |
| `context-injector` | Prepara contexto antes de cada interação |
| `cross-pilar-triggers` | Motor de triggers que conecta eventos entre pilares |
| `heartbeat-coordinator` | Padrão anti-spam Check-Before-Act |
| `daily-writer` | Registro diário + commit automático |
| `weekly-consolidator` | Consolidado semanal dos 5 pilares |
| `atlas-handoff` | Processo de sincronização entre sessões |
| `conflito-decisao` | Detecção de reversões e registro de ADRs |

## Demonstração

[](https://www.youtube.com/watch?v=OhnpdTJnuYs)

*Tour pelo repositório atlas-portifolio e visão geral da arquitetura do sistema (90s).*

## Roadmap

- ✅ **Fase 1 (ativo)** — P1 (Saúde) e P4 (Finanças) operacionais. 5 perfis, 13 cron jobs, 22 ADRs.
- 📅 **Fase 2** — P2 (Desenvolvimento). Perfil `atlas-p2-dev`, portfólio comercial, AIaaS.
- 📅 **Fase 3** — P3 (Relações) e P5 (Propósito).

## Tecnologias e integrações

- Markdown + GitHub como base de memória persistente
- Hermes Agent como harness de execução
- Telegram como canal principal de interação
- GitHub Actions / cron para rotinas automáticas

## Sobre o autor

**Lucas Lemos** — contador em transição para desenvolvedor de agentes de IA. Construindo o Atlas como portfólio, laboratório e sistema pessoal de suporte estratégico.

- LinkedIn: [Lucas Lemos](http://www.linkedin.com/in/lucas-lemos-268294111)
- Email: lucas.lml.altas@gmail.com

---

*Este repositório é a versão pública de apresentação do projeto. A instância pessoal permanece privada por conter dados sensíveis.*
