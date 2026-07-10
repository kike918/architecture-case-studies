# MicroPOS — Arquitectura

## Propósito

Definir la arquitectura pública edge/offline-first de MicroPOS y del piloto con Raspberry Pi.

## Estilo arquitectónico

MicroPOS separa el camino transaccional de la disponibilidad del ERP externo.

```text
POS UI
  ↓
Servicio de aplicación local
  ↓
Base operacional local
  ↓
Transactional Outbox
  ↓
Sync Worker
  ↓
Cloud Sync API
  ↓
Capa de integración
  ├── Adapter Odoo
  └── Adapter Dolibarr
```

## Responsabilidades edge

El nodo Raspberry Pi del piloto será responsable de:

- disponibilidad local;
- persistencia transaccional;
- impresión;
- persistencia de outbox;
- reintentos de sincronización;
- backups locales;
- recuperación de arranque;
- diagnóstico y health checks.

## Responsabilidades cloud

- recepción de eventos sincronizados;
- procesamiento idempotente;
- monitoreo central;
- backup remoto;
- agregación de reporting;
- integración ERP;
- orquestación no crítica con n8n.

## Modelo de sincronización

Una venta se completa localmente antes del ACK cloud.

```text
BEGIN LOCAL TRANSACTION
  ├── guardar venta
  ├── guardar pago
  ├── registrar movimiento local de stock
  └── agregar evento outbox
COMMIT

Sync worker
  ↓
POST con idempotency key
  ↓
Cloud valida y procesa
  ↓
ACK
  ↓
Outbox marca sincronizado
```

## Supuestos de fallo

La arquitectura asume que Internet puede desaparecer durante horas, la energía puede fallar, los requests pueden duplicarse, las APIs ERP pueden caer, la impresora puede desconectarse y puede ser necesario restaurar almacenamiento local.

## Principio operativo

> Vender localmente, persistir con seguridad, sincronizar de forma idempotente y reconciliar explícitamente.
