# Habilidades do Atlas

Este documento descreve as skills ativas do sistema.

## Domínio

### `p1-saude`
Monitoramento de indicadores de saúde mental e física, thresholds e padrões de prevenção.

### `p4-financas`
Acompanhamento semanal das operações financeiras, decisões de CFO e metas operacionais.

### `p4-validacao-financeira`
Validação de valores e transações acima de thresholds definidos.

## Coordenação

### `orchestrator`
Cérebro central: roteia interações, gerencia conflitos cross-pilar e mantém o Kanban.

### `context-injector`
Prepara e injeta o contexto necessário antes de cada interação.

### `cross-pilar-triggers`
Motor de triggers que detecta eventos em um pilar e dispara ações em outro.

### `heartbeat-coordinator`
Implementa o padrão Check-Before-Act para evitar spam e sobrecarga.

## Registro e Sincronização

### `daily-writer`
Gera registro diário e coordena commit de memória.

### `weekly-consolidator`
Produz consolidado semanal dos 5 pilares e atualiza tendências.

### `atlas-handoff`
Processo de flush entre sessões: memória curta → diário → MOC → commit.

### `atlas-backlog`
Gestão de tarefas, reconciliação com Kanban e priorização.

### `conflito-decisao`
Detecta reversões de decisão e registra ADRs quando necessário.
