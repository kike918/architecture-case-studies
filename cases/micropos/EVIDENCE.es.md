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

## Reconciliación de evidencia: web comercial frente a POS edge (2026-11-09)

La matriz anterior corresponde a la **arquitectura objetivo edge**. La implementación `MicroPos-web` se clasifica por separado:

| Capacidad web comercial | Fuente consultada en lectura | Límite de evidencia |
|---|---|---|
| Sitio estático multilingüe | `MicroPos-web@dev/README.md` y `ROADMAP.md` | Astro ES/EN/CA documentado y URL comercial publicada; no acredita cada página en vivo |
| Leads/mini CRM | README y roadmap | PHP/SQLite, API v1 y actividades persistidas; implementación documentada |
| Pagos | README y roadmap | Flujos manuales/parciales y Bold documentados; aprobación en pruebas **no** certifica cualquier cobro productivo |
| Outbox y n8n | README y roadmap | Validaciones reales API/webhook→n8n registradas para la web; **no** prueban sincronización del POS edge |
| Artefactos de Hostinger | `MicroPos-web@dev/HOSTINGER-DEPLOYMENT.md` | Empaquetado INSTALL/UPDATE y política de preservación documentados; generar un ZIP no equivale a desplegarlo |
| POS Raspberry Pi | Caso de arquitectura y `PILOT_PLAN.md` | Planificado, sin resultados de ejecución examinados |

**Criterios:** verificar release web fechado y smoke productivo antes de ampliar afirmaciones de despliegue. Completar el piloto hardware (venta offline, impresión, reinicio, sincronización sin duplicados, restauración real y conciliación ERP) antes de elevar el nivel de evidencia edge a Piloto o Desplegado.

**Revisión documental; no prueba de salud productiva en tiempo real.**

