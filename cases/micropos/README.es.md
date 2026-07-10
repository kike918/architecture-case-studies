# MicroPOS

🌐 **Idiomas:** [English](README.md) · Español · [Català](README.ca.md)

**Estado:** Baseline arquitectónico publicado; piloto edge con Raspberry Pi planificado. Los adapters ERP y scripts operativos están definidos como objetivos de implementación, no como capacidades productivas validadas.

## Resumen ejecutivo

MicroPOS es una arquitectura POS ligera para pequeños negocios y entornos de baja conectividad. La hipótesis central es que un negocio debe poder vender, imprimir, cerrar caja, preservar datos locales y recuperarse de pérdida de conectividad sin depender de una conexión continua a la nube.

La arquitectura propuesta usa una Raspberry Pi como nodo edge opcional para el piloto, persistencia operacional local, sincronización mediante outbox, scripts para provisión y recuperación, y adapters para Odoo y Dolibarr en lugar de acoplar el core POS a un solo ERP.

**Nivel de evidencia:** baseline arquitectónico + piloto de hardware planificado. Offline, sincronización, impresión, recuperación y adapters ERP requieren implementación y validación de campo.

## Problema

MicroPOS debe soportar:

- ventas locales sin Internet;
- impresión y operación de caja;
- recuperación tras reinicio o corte eléctrico;
- sincronización eventual;
- prevención de duplicados;
- backup y restore;
- diagnóstico remoto simple;
- integración ERP opcional según madurez del negocio.

## Arquitectura resumida

```text
Dispositivos del negocio
        │
        ▼
┌─────────────────────────┐
│ Raspberry Pi Edge Node  │
│ MicroPOS local          │
│ Base operacional local  │
│ Transactional outbox    │
│ Sync worker             │
│ Print service           │
│ Backup agent            │
│ Health diagnostics      │
└────────────┬────────────┘
             │
       Internet intermitente
             │
             ▼
┌─────────────────────────┐
│ Servicios Cloud DCP     │
│ Sync API                │
│ n8n                     │
│ Monitoring              │
│ Backups                 │
│ Integraciones           │
└────────────┬────────────┘
             │
       ┌─────┴─────┐
       ▼           ▼
      Odoo      Dolibarr
```

## Decisión ERP

MicroPOS permanece independiente:

```text
MicroPOS Core
      │
      ├── Adapter Odoo
      ├── Adapter Dolibarr
      ├── CSV Import / Export
      └── API / Webhooks
```

Odoo y Dolibarr son destinos de integración, no el motor transaccional del nodo edge.

## Piloto Raspberry Pi

### Fase A — baseline del nodo

- Raspberry Pi OS Lite;
- empaquetado reproducible;
- MicroPOS;
- base local;
- impresión;
- health checks;
- backups;
- arranque automático.

### Fase B — escenarios de operación

- venta normal;
- venta offline;
- apertura y cierre de caja;
- impresión;
- reinicio inesperado;
- pérdida y retorno de Internet;
- backlog de sincronización;
- duplicados;
- conflicto de stock;
- backup y restore real.

### Fase C — sincronización

```text
Transacción local
       ↓
Commit local
       ↓
Outbox event
       ↓
Sync worker
       ↓
Cloud API
       ↓
Procesamiento idempotente
       ↓
ACK
       ↓
Marcar sincronizado
```

## Scripts operativos

```text
scripts/
├── install/
├── ops/
├── backup/
├── sync/
└── integrations/
    ├── odoo/
    └── dolibarr/
```

## Alcance MVP del piloto

- ventas;
- caja;
- inventario mínimo;
- clientes básicos;
- offline;
- backup/restore;
- sincronización;
- diagnóstico;
- auditoría mínima.

## Dirección de producto

```text
MicroPOS Start
software + configuración + catálogo inicial + capacitación + soporte

MicroPOS Edge
Raspberry Pi + operación local + backup + impresión + monitoreo + soporte remoto

MicroPOS Business
MicroPOS + ERP + automatización + dashboards + CRM/integraciones
```

## Documentos relacionados

- [`ARCHITECTURE.es.md`](ARCHITECTURE.es.md)
- [`DECISIONS.es.md`](DECISIONS.es.md)
- [`PILOT_PLAN.es.md`](PILOT_PLAN.es.md)
- [`ERP_STRATEGY.es.md`](ERP_STRATEGY.es.md)
- [`SCRIPTS_CATALOG.es.md`](SCRIPTS_CATALOG.es.md)
- [`EVIDENCE.es.md`](EVIDENCE.es.md)

---

MicroPOS se documenta como arquitectura edge/offline-first y programa piloto, no como plataforma POS validada en producción.
