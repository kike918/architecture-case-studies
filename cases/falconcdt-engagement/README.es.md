# FalconCDT Engagement Platform

🌐 **Idiomas:** [English](README.md) · Español · [Català](README.ca.md)

**Estado:** Caso publicado — resumen público y sanitizado de arquitectura basado en una plataforma B2B white-label de engagement operativa.

## Resumen ejecutivo

FalconCDT Engagement Platform evolucionó desde una implementación real de pronósticos hacia una plataforma B2B reutilizable para marcas, negocios, comunidades y campañas privadas.

El reto arquitectónico principal no era solamente registrar pronósticos. Era soportar un modelo operativo reutilizable con registro de participantes, zona privada de usuario, administración, deadlines, scoring, rankings por fase, mensajería, notificaciones, auditoría, branding y despliegues para diferentes clientes sin introducir prematuramente una arquitectura SaaS multi-tenant compleja.

La solución actual utiliza una arquitectura ligera PHP/MySQL con separación entre servicios y repositorios, despliegues white-label independientes por instancia, colas de notificación, endpoints de automatización protegidos y separación explícita entre la fuente oficial de resultados y proveedores secundarios de enriquecimiento visual.

**Nivel de evidencia:** `Desplegado`, con uso operativo y hardening orientado a producción; algunas integraciones y mejoras UX continúan en roadmap.

## Problema

La plataforma debía reconciliar dos necesidades:

1. **Reutilización de producto:** scoring, ranking, administración, notificaciones y auditoría compartidos.
2. **Aislamiento por cliente:** branding, reglas, participantes, premios, configuración y calendarios operativos diferentes.

La arquitectura también debía mantenerse operable por un equipo pequeño y desplegable en infraestructura práctica sin sobredimensionar prematuramente el producto.

## Restricciones principales

- equipo pequeño;
- necesidad de entrega rápida;
- personalización real por cliente;
- baja justificación inicial para multi-tenancy;
- restricciones de hosting;
- APIs externas con límites y diferencias;
- privacidad del historial de pronósticos;
- necesidad de scoring y auditoría verificables;
- confiabilidad variable del cron del hosting;
- canales de notificación con fallos diferentes;
- secretos fuera del control de versiones.

## Drivers arquitectónicos

- simplicidad de despliegue;
- aislamiento operativo;
- auditabilidad;
- mantenibilidad;
- claridad de fuentes de datos;
- automatización controlada;
- privacidad;
- extensibilidad sin sobrearquitectura;
- control de costos.

## Arquitectura resumida

```text
Participantes / Admins
        │
        ▼
 Aplicación Web
 PHP + HTML/CSS/JS
        │
        ├── Controllers
        ├── Services
        ├── Repositories
        ├── Providers
        └── Views
        │
        ▼
 MySQL / MariaDB
 fuente de verdad operacional
        │
        ├── scoring y rankings
        ├── fases y ganadores
        ├── colas de notificación
        ├── configuración
        └── auditoría

Integraciones externas
        │
        ├── proveedor oficial de resultados
        ├── proveedor opcional de enriquecimiento
        ├── SMTP
        ├── Telegram
        └── n8n como orquestador
```

## Decisiones clave

- multi-instancia antes que multi-tenancy;
- MySQL como fuente runtime de verdad;
- un único proveedor oficial para decisiones de scoring;
- proveedores secundarios solo para enriquecimiento;
- reglas de negocio en servicios;
- SQL en repositorios;
- notificaciones por plantillas y colas;
- n8n como orquestador, no como dueño del dominio;
- endpoints de automatización protegidos;
- ranking público separado del historial privado de pronósticos.

## Seguridad y privacidad

- secretos fuera de Git;
- debug productivo deshabilitado;
- rutas privadas protegidas;
- ejecución de scripts bloqueada en uploads;
- secretos conocidos redactados de logs;
- endpoints de automatización protegidos;
- ranking público sin exponer automáticamente el historial detallado del participante;
- acciones administrativas sensibles auditables.

## Evidencia

| Capacidad | Nivel |
|---|---|
| Registro y autenticación | Desplegado |
| Pronósticos y deadline enforcement | Desplegado |
| Scoring y ranking por fase | Desplegado |
| Módulos administrativos | Desplegado |
| Cierre de fases, ganadores y premios | Desplegado / validado en release |
| Email | Desplegado |
| Telegram | Desplegado |
| Resumen diario admin | Desplegado |
| Sincronización de resultados oficiales | Desplegado |
| Detalle enriquecido opcional | Implementado, dependiente de integración |
| Orquestación n8n | Parcial |
| WhatsApp Bridge | Roadmap |
| Hardening responsive global | Roadmap |
| Multi-tenancy compartido | No implementado por decisión arquitectónica |

## Resultados públicos seguros

La evidencia permite afirmar que la plataforma evolucionó de una dinámica real de engagement hacia una base de producto multi-instancia reutilizable sin introducir complejidad SaaS prematura.

No se publican afirmaciones no verificadas sobre ingresos, conversión, crecimiento de usuarios, disponibilidad o escala.

## Aprendizajes

### Multi-instancia puede ser la decisión correcta al inicio
Separar despliegues por cliente puede ser preferible cuando todavía se están validando diferencias operativas reales.

### Una sola fuente debe decidir la verdad oficial
Los proveedores secundarios pueden enriquecer la experiencia, pero no deben competir por modificar el mismo hecho de negocio.

### Automatización no es sinónimo de dominio
n8n puede disparar procesos y notificaciones; scoring, ranking y estados permanecen en la aplicación.

### Operación también es arquitectura
Backups, rollback, patches y checkpoints de release forman parte del diseño técnico real.

### La privacidad importa también en productos de engagement
Un ranking público no obliga a exponer el historial detallado del participante.

## Próximas preguntas arquitectónicas

- ¿Cuándo el costo de múltiples instancias justifica multi-tenancy?
- ¿Qué configuraciones deben vivir en datos, código o automatización de despliegue?
- ¿Cuándo las notificaciones requieren workers dedicados?
- ¿Cuándo conviene migrar a despliegues containerizados?
- ¿Qué nivel de observabilidad se justifica por evidencia operativa?
- ¿Cómo generalizar el producto más allá de pronósticos deportivos sin debilitar el dominio?

## Documentos relacionados

- [`ARCHITECTURE.es.md`](ARCHITECTURE.es.md)
- [`DECISIONS.es.md`](DECISIONS.es.md)
- [`SECURITY_AND_PRIVACY.es.md`](SECURITY_AND_PRIVACY.es.md)
- [`EVIDENCE.es.md`](EVIDENCE.es.md)

---

Este caso excluye intencionalmente credenciales, endpoints privados, datos confidenciales de clientes y código fuente propietario.
