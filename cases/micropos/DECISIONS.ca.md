# MicroPOS — Decisions d’Arquitectura

## ADR-001 — Camí transaccional offline-first
**Decisió:** la venda es confirma localment abans de sincronitzar amb el cloud.

## ADR-002 — Raspberry Pi com a node edge opcional
**Decisió:** validar Raspberry Pi com a node local de serveis durant el pilot.

## ADR-003 — MicroPOS independent de l’ERP
**Decisió:** Odoo i Dolibarr són destins d’integració, no el motor transaccional edge.

## ADR-004 — Transactional Outbox
**Decisió:** crear l’esdeveniment outbox dins de la mateixa transacció local que la venda.

## ADR-005 — Processament idempotent al cloud
**Decisió:** cada esdeveniment sincronitzat té identitat idempotent i gestió segura de duplicats.

## ADR-006 — n8n per a workflows no crítics
**Decisió:** n8n programa, notifica i coordina integracions, però no governa la venda local.

## ADR-007 — Scripts com a actius de producte
**Decisió:** provisioning, diagnòstic, backup, restore, sync i integracions es versionen i es proven.

## ADR-008 — Validar simplicitat abans d’expandir
**Decisió:** provar vendes, caixa, inventari mínim, impressió, offline, restore i sync abans d’ampliar horitzontalment el producte.
