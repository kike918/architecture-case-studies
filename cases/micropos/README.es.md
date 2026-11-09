# MicroPOS

🌐 **Idiomas:** [English](README.md) · Español · [Català](README.ca.md)

**Estado:** Implementación de web comercial/mini CRM documentada; baseline del POS edge publicado y piloto Raspberry Pi pendiente. Sin afirmación de validación productiva del POS edge.

## Actualización de evidencia — dos líneas distintas de MicroPOS (2026-11-09)

**No confundir la web comercial operativa con el futuro POS edge.** La documentación del repositorio separado `MicroPos-web` registra una web comercial Astro multilingüe, mini CRM PHP/SQLite, API de integración versionada, outbox/webhooks persistentes, pagos manuales y Bold, y pruebas reales de integración con n8n. Son capacidades de la **web comercial y mini CRM**, no del motor POS Raspberry Pi.

| Línea | Evidencia respaldada por los documentos revisados | No demostrado |
|---|---|---|
| Web comercial y mini CRM | Astro SSG ES/EN/CA; CRM PHP/SQLite, API v1, contratos de pagos, outbox y pruebas n8n documentadas; web comercial publicada en Hostinger | Auditoría independiente en vivo de todas las funciones, cobro productivo integral, disponibilidad o uso sostenido |
| POS edge/offline-first | Arquitectura, ADR y plan de pruebas de campo Raspberry Pi | Ventas offline ejecutadas, base POS local resiliente, impresión, recuperación de sincronización, adapters ERP o piloto Raspberry Pi aprobado |

**Relación arquitectónica:** la web comercial captura prospectos y gestiona pagos comerciales; el POS edge proyectado realizaría las ventas del establecimiento localmente. Un lead/pago de la web no equivale a una venta offline del POS. El outbox del CRM web y su validación con n8n no certifican el *outbox de sincronización edge*.

Ver el detalle en [EVIDENCE.es.md](EVIDENCE.es.md). El resto del documento describe la **arquitectura objetivo edge**, no un inventario de implementación.

## Evaluación arquitectónica — restricciones, seguridad, compromisos y dudas

**Contexto y restricciones.** Los pequeños negocios tienen presupuestos limitados, conectividad variable y poca capacidad de administrar equipos. Una web de captación comercial no demuestra que exista un libro transaccional de ventas tolerante a desconexiones.

**Seguridad y privacidad.** El mini CRM comercial gestiona prospectos y procesos asociados a pagos; el futuro POS edge gestionaría ventas locales y eventualmente datos personales. Ambos requieren permisos acotados, secretos aislados, políticas de retención, auditoría y recuperación comprobada según su entorno real. No se deben extrapolar los controles documentados en la web al POS edge no implementado.

**Alternativas y trade-offs.** Un POS solo cloud reduce mantenimiento de hardware, pero depende de Internet; instalar un ERP completo en cada nodo eleva complejidad y actualizaciones. Un core local con adapters ERP podría aportar continuidad, a costa de conflictos de sincronización, desgaste de almacenamiento, conciliación y soporte. Son hipótesis pendientes de piloto.

**Operación y preguntas abiertas.** Antes de aceptar un piloto se necesitan versiones exactas, trazas de venta offline e impresión, reinicio y restauración real, pruebas de eventos duplicados, conciliación del backlog, feedback de operadores y registro de fallos/rollback. Los diagramas y catálogos de scripts no sustituyen estas pruebas.

## Mapa de conformidad con el estándar de publicación

Los 14 temas exigidos se encuentran en el documento y sus anexos vinculados:

| Tema obligatorio | Ubicación |
|---|---|
| Contexto; problema; restricciones; drivers | Resumen, Problema y [Arquitectura](ARCHITECTURE.es.md) |
| Límites y vista arquitectónica | Arquitectura resumida, Decisión ERP y [Arquitectura](ARCHITECTURE.es.md) |
| Decisiones; alternativas; trade-offs | Decisión ERP, [Decisiones](DECISIONS.es.md), [Estrategia ERP](ERP_STRATEGY.es.md) |
| Seguridad y privacidad | [Arquitectura](ARCHITECTURE.es.md), [Evidencia](EVIDENCE.es.md) y verificación específica pendiente |
| Entrega y operación | Piloto, Scripts y [Plan piloto](PILOT_PLAN.es.md) |
| Nivel de evidencia | Actualización de las dos líneas y [Registro](EVIDENCE.es.md) |
| Aprendizajes y preguntas pendientes | Separación CRM/web versus sincronización edge; pendientes del [Plan piloto](PILOT_PLAN.es.md) |

**Nivel canónico por línea:** web comercial **Deployed** para la superficie pública documentada, sin validación productiva sostenida; POS edge **Concept**, con diseño publicado y piloto sin ejecutar. No se realizó una auditoría independiente del runtime en vivo.

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
