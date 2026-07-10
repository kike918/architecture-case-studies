# MicroPOS — Decisiones de Arquitectura

## ADR-001 — Camino transaccional offline-first
**Decisión:** la venta se confirma localmente antes de sincronizar con cloud.

## ADR-002 — Raspberry Pi como nodo edge opcional
**Decisión:** validar Raspberry Pi como nodo local de servicios durante el piloto.

## ADR-003 — MicroPOS independiente del ERP
**Decisión:** Odoo y Dolibarr son destinos de integración, no el motor transaccional edge.

## ADR-004 — Transactional Outbox
**Decisión:** crear el evento outbox en la misma transacción local que la venta.

## ADR-005 — Procesamiento idempotente en cloud
**Decisión:** cada evento sincronizado tiene identidad idempotente y manejo seguro de duplicados.

## ADR-006 — n8n para workflows no críticos
**Decisión:** n8n programa, notifica y coordina integraciones, pero no gobierna la venta local.

## ADR-007 — Scripts como activos de producto
**Decisión:** provisioning, diagnóstico, backup, restore, sync e integraciones se versionan y prueban.

## ADR-008 — Validar simplicidad antes de expandir
**Decisión:** probar ventas, caja, inventario mínimo, impresión, offline, restore y sync antes de ampliar horizontalmente el producto.
