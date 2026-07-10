# FalconCDT Engagement Platform — Registro de Evidencia

## Propósito

Este registro relaciona afirmaciones públicas del caso con niveles explícitos de evidencia. Es deliberadamente conservador: los elementos de roadmap no se presentan como capacidades completadas.

## Escala de evidencia

- **Concepto** — idea documentada o dirección arquitectónica.
- **Prototipo** — implementado experimentalmente, aún sin uso operativo.
- **Piloto** — validado en uso real controlado.
- **Desplegado** — presente en un despliegue operativo.
- **Validado en producción** — verificado repetidamente en operación productiva con evidencia más fuerte.

## Matriz de capacidades

| Capacidad | Nivel de evidencia | Base pública segura |
|---|---|---|
| Registro y login | Desplegado | Checkpoint operativo documenta registro, login, sesiones y roles |
| Dashboard y perfil | Desplegado | Dashboard, perfil y preferencias documentados |
| Captura de pronósticos | Desplegado | Flujo operativo documentado |
| Validación de deadlines | Desplegado | Validación backend y bloqueo automático documentados |
| Scoring por fase | Desplegado | Scoring y ranking por fase operativos |
| Rankings independientes por fase | Desplegado | Separación de fases documentada |
| Ranking público con historial privado | Desplegado | Separación documentada |
| Gestión admin de participantes | Desplegado | Operaciones CRUD y estados documentados |
| Administración de pagos/registro | Desplegado | Operaciones administrativas documentadas |
| Administración de partidos/eventos | Desplegado | CRUD y filtros documentados |
| Auditoría de pronósticos | Desplegado | Vistas globales y por pronóstico documentadas |
| Auditoría general | Desplegado | Audit log de aplicación documentado |
| Cierre de fases | Desplegado / validado en release | Cierre formal y validación documentados |
| Ganadores y premios | Desplegado / validado en release | Declaración, notificación y premios documentados |
| Email | Desplegado | SMTP probado y procesamiento en cola documentado |
| Telegram | Desplegado | Integración individual/grupo y cola documentadas |
| Plantillas editables | Desplegado | Templates multicanal documentados |
| Resumen diario admin | Desplegado | Email/Telegram con deduplicación documentados |
| Dashboard de automatizaciones | Desplegado | Ejecución manual y visibilidad de runs documentadas |
| Endpoints protegidos | Desplegado | Protección por automation secret documentada |
| Sync de resultados oficiales | Desplegado | Sincronización externa y normalización en MySQL documentadas |
| Detalle enriquecido opcional | Implementado / dependiente de integración | Integración secundaria con fallback documentada |
| Exportables CSV | Desplegado | Exportables admin documentados |
| Configuración white-label | Desplegado baseline | Branding y configuración comercial documentados |
| Modelo multi-instancia | Desplegado | Aislamiento por despliegue documentado |
| Multi-tenancy compartido | No implementado | Excluido explícitamente de la arquitectura actual |
| Orquestación n8n productiva | Parcial | Endpoints y workflows documentados; despliegue/configuración aún dependientes del ambiente |
| WhatsApp Bridge | Roadmap | Stub preparado; no se presenta como canal productivo |
| Hardening UX responsive global | Roadmap | Trabajo pendiente explícito |

## Límites de evidencia

Este registro público no expone:

- código fuente privado;
- URLs productivas que deban permanecer privadas;
- credenciales o tokens;
- datos reales de participantes;
- configuraciones confidenciales de clientes;
- secretos de infraestructura.

## Disciplina de afirmaciones

El caso puede afirmar que la plataforma fue desplegada y usada operativamente, pero no debe afirmar escala, ingresos, mejora de conversión, crecimiento de usuarios o uptime sin evidencia validada y autorización para publicar.
