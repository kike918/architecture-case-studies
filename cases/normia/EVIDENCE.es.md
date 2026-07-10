# Normia — Registro de Evidencia

## Propósito

Separar arquitectura documentada, prototipos de referencia, implementación en curso y validación futura. Normia no se presenta todavía como validado en producción.

## Escala de evidencia

- **Baseline documentado** — definición aprobada para implementación.
- **Prototipo de referencia** — referencia UX o de flujo, no comportamiento productivo.
- **Implementación en curso** — bootstrap o código activo.
- **Piloto pendiente** — requiere validación operacional real.
- **Fase posterior** — secuenciada después del Golden Flow.
- **Validado en producción** — no reclamado actualmente.

## Matriz

| Capacidad | Nivel | Base pública segura |
|---|---|---|
| Definición de producto | Baseline documentado | Master consolidado y baseline de proyecto |
| Arquitectura MVP | Baseline documentado | Arquitectura congelada; cambios estructurales requieren ADR y aprobación humana |
| Principios UX mobile-first y task-driven | Baseline documentado | Principios de producto definidos |
| Prototipo UX | Prototipo de referencia | v0.1 explícitamente no productivo |
| Discovery del piloto | En curso | Sprint 0 y levantamiento real |
| Monolito modular | Baseline / bootstrap en curso | Diseño Laravel documentado |
| Single-tenant por instalación | Baseline arquitectónico | Estrategia MVP definida |
| Roles y permisos | Baseline de dominio | Operator, Supervisor, Admin y Auditor definidos |
| Ejecución de tareas | Golden Flow definido | Vertical slice especificado |
| Control de temperatura | Golden Flow definido | Medición, perfil y evaluación especificados |
| Gestión de desviaciones | Modelo de dominio definido | Paths conforme/no conforme definidos |
| Contención | Modelo de dominio definido | Diferenciada de acción correctiva |
| Ciclo CAPA | Modelo de dominio definido | Estados explícitos definidos |
| Verificación supervisor | Modelo de dominio definido | Ciclo aprobar/devolver especificado |
| Ciclo documental | Baseline de dominio | Estados y versionado definidos |
| Storage sensible privado | Baseline arquitectónico | Patrón de acceso controlado definido |
| Audit events | Baseline arquitectura/dominio | Eventos candidatos y separación de ledger definidos |
| Audit ledger local | Arquitectura definida | Implementación pendiente |
| Hash chain | Fase posterior | Después del flujo operacional |
| Merkle batching | Fase posterior | Arquitectura definida |
| Polygon testnet | Fase posterior | Arquitectura definida |
| Polygon producción | Fase posterior | Requiere validación previa |
| Telegram Bot/Mini App | Arquitectura de canal definida | Utilidad operacional pendiente de validar |
| n8n | Límite arquitectónico definido | Implementación y operación pendientes de validar |
| Validación productiva | No reclamada | Evidencia aún insuficiente |

## Evidencia requerida para aprobar Golden Flow

- funciona en teléfono real;
- permisos Operator/Supervisor correctos;
- rutas conforme y no conforme completas;
- no se destruye historial;
- tests de dominio y permisos;
- audit events generados desde backend;
- errores sin estados imposibles;
- revisión humana;
- documentación alineada con implementación.

## Disciplina de afirmaciones

El caso puede describir arquitectura, modelado de dominio y dirección de implementación. No debe afirmar certificación regulatoria, mejora de cumplimiento, aceptación de auditoría, escala productiva o verificación blockchain productiva sin evidencia suficiente.
