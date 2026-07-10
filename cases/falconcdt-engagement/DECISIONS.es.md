# FalconCDT Engagement Platform — Decisiones de Arquitectura

## ADR-001 — Multi-instancia antes que multi-tenancy

**Contexto:** el producto debía soportar diferentes despliegues B2B con branding, participantes, premios, reglas y calendarios distintos.

**Decisión:** usar instancias white-label independientes en lugar de una base de datos compartida multi-tenant.

**Razones:** mayor aislamiento, menor complejidad inicial, cambios específicos por cliente más seguros y rollback más claro.

**Trade-offs:** despliegues duplicados, más coordinación de patches y riesgo de drift de configuración.

**Condición de reversión:** reconsiderar cuando el número de clientes y el costo de mantenimiento superen el costo de introducir un control plane compartido y aislamiento tenant.

---

## ADR-002 — MySQL como fuente runtime de verdad

**Contexto:** los proveedores externos entregan resultados, pero scoring y ranking requieren comportamiento determinista y auditable.

**Decisión:** normalizar datos externos en MySQL antes de usarlos para scoring y ranking.

**Razones:** determinismo, auditoría, menor acoplamiento con APIs y consistencia del frontend.

**Trade-offs:** dependencia de sincronización, posibilidad de datos stale y necesidad de reconciliación.

---

## ADR-003 — Un proveedor oficial y proveedores secundarios de enriquecimiento

**Decisión:** un único proveedor decide marcador y estado oficial; otros solo agregan información opcional.

**Razón principal:** dos proveedores no deben competir por el mismo hecho de negocio cuando ese hecho modifica scoring y ranking.

**Trade-offs:** dependencia del proveedor oficial y posibles fallos parciales en el enriquecimiento.

---

## ADR-004 — Arquitectura ligera por capas sin framework pesado

**Decisión:** PHP 8.2+, PDO, MySQL y límites explícitos entre Controllers, Services, Repositories, Providers y Views.

**Razones:** bajo overhead, compatibilidad con hosting práctico, control directo y evolución incremental.

**Trade-offs:** más convenciones internas y disciplina arquitectónica manual.

---

## ADR-005 — La aplicación gobierna el dominio; n8n orquesta

**Decisión:** n8n invoca endpoints HTTP protegidos, pero scoring, ranking y transiciones de fase permanecen en la aplicación.

**Razones:** mantener invariantes de dominio en un solo lugar, preservar testabilidad y evitar duplicar lógica de negocio en workflows.

**Trade-offs:** endpoints seguros, idempotencia y monitoreo de workflows siguen siendo necesarios.

---

## ADR-006 — Colas de notificación por canal

**Decisión:** generar trabajo de notificación por canal mediante plantillas y colas, con procesamiento manual como fallback operativo.

**Razones:** separar generación de entrega, permitir comportamiento por canal y habilitar reintentos y deduplicación.

**Trade-offs:** monitoreo adicional y entrega eventualmente asíncrona.

---

## ADR-007 — Ranking público sin historial público de pronósticos

**Decisión:** mostrar resultados agregados en rankings sin publicar automáticamente el historial detallado de cada participante.

**Razones:** engagement, privacidad y reducción de copia estratégica durante la competencia.

**Trade-offs:** algunas funciones sociales quedan intencionalmente limitadas.
