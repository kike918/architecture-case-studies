# MicroPOS — Registro de Evidencia

## Propósito

Separar decisiones arquitectónicas de evidencia de laboratorio, piloto y futuras afirmaciones de producto.

## Escala

- **Baseline documentado** — dirección aprobada para implementación.
- **Laboratorio planificado** — validación hardware/software definida pero no ejecutada.
- **Prototipo** — implementación experimental.
- **Piloto pendiente** — requiere uso real.
- **Piloto validado** — uso controlado completado.
- **Validado en producción** — no reclamado actualmente.

## Matriz

| Capacidad | Nivel |
|---|---|
| Arquitectura edge/offline-first | Baseline documentado |
| Nodo Raspberry Pi | Laboratorio planificado |
| Venta local | Alcance MVP del piloto |
| Persistencia local | Baseline documentado |
| Transactional outbox | Baseline documentado |
| Sync idempotente | Baseline documentado |
| Impresión | Laboratorio/piloto pendiente |
| Caja | Alcance MVP |
| Inventario mínimo | Alcance MVP |
| Scripts de backup | Implementación planificada |
| Scripts de diagnóstico | Implementación planificada |
| Adapter Dolibarr | Prototipo planificado |
| Adapter Odoo | Prototipo planificado |
| n8n | Rol arquitectónico definido |
| Piloto negocio simple | Planificado |
| Piloto operación compleja | Fase posterior |
| Validación productiva | No reclamada |

## Evidencia requerida

Antes de afirmar madurez se debe demostrar venta sin Internet, commit local durable, recuperación tras reinicio, sincronización sin duplicados, backlog visible, backup y restore exitosos, impresión estable, diagnóstico útil y reconciliación ERP explícita.

## Disciplina de afirmaciones

No se debe afirmar confiabilidad offline productiva, madurez de integración ERP ni estabilidad de campo de Raspberry Pi hasta demostrarlo.
