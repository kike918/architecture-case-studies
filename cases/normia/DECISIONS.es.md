# Normia — Decisiones de Arquitectura

## ADR-001 — Monolito modular para el MVP

**Decisión:** usar un monolito modular en Laravel antes de considerar microservicios.

**Por qué:** el producto todavía valida límites de dominio mediante un piloto real. Una arquitectura distribuida agregaría costos de despliegue, observabilidad y consistencia antes de estabilizar el dominio.

**Trade-offs:** la disciplina modular debe mantenerse dentro de un solo codebase.

---

## ADR-002 — Single-tenant por instalación

**Decisión:** una instalación aislada por cliente durante el MVP.

**Por qué:** límites de privacidad más simples, menor complejidad y ownership operativo más claro.

**Trade-offs:** trabajo duplicado de despliegue y upgrades.

---

## ADR-003 — MySQL como fuente de verdad operacional

**Decisión:** tareas, controles, desviaciones, acciones correctivas y semántica de auditoría viven en la base de la aplicación.

**Por qué:** la operación diaria debe continuar aunque Telegram, n8n o blockchain estén no disponibles.

---

## ADR-004 — Laravel gobierna las reglas; los canales comparten servicios

**Decisión:** web, QR, Telegram Bot y Mini App invocan servicios comunes de aplicación.

**Por qué:** una sola implementación de permisos, conformidad, transiciones de estado y eventos de auditoría.

---

## ADR-005 — n8n orquesta pero no gobierna estados de dominio

**Decisión:** n8n ejecuta horarios, reintentos y notificaciones; Laravel mantiene decisiones de negocio.

**Por qué:** las invariantes deben permanecer centralizadas y testeables.

---

## ADR-006 — Auditar localmente antes de anclar externamente

**Decisión:** crear eventos semánticos y un ledger local antes de Merkle batches y Polygon.

**Por qué:** blockchain fortalece integridad, pero no reemplaza contexto ni persistencia operacional.

---

## ADR-007 — Polygon fuera del camino crítico

**Decisión:** la operación sanitaria continúa aunque el anclaje se retrase o falle.

**Por qué:** una operación física no puede depender de RPC, gas, nonce o finality.

---

## ADR-008 — Sin datos personales o sensibles on-chain

**Decisión:** anclar únicamente compromisos criptográficos agregados y metadatos mínimos.

**Por qué:** privacidad, minimización de datos y control del ciclo de vida.

---

## ADR-009 — Corrección por supersesión

**Decisión:** los registros críticos cerrados no se sobrescriben ni eliminan silenciosamente. Las correcciones preservan el original.

**Por qué:** auditabilidad y reconstrucción histórica.

---

## ADR-010 — Validar Golden Flow antes de expansión horizontal

**Decisión:** priorizar un vertical slice completo desde tarea hasta desviación, contención, acción correctiva, verificación y auditoría.

**Por qué:** módulos CRUD aislados no prueban el modelo de producto.
