# Rewi — Arquitectura SaaS de fidelización digital

🌐 **Idiomas:** [English](README.md) · Español

**Estado:** Caso público de arquitectura sanitizado. **Nivel de evidencia: Desplegado** (release productivo documentado el 3 de noviembre de 2026). **No validado en producción** según el estándar del repositorio: las evidencias revisadas no acreditan operación sostenida, cobertura funcional completa ni restauración real de respaldo productivo.

## 1. Resumen ejecutivo

Rewi es un SaaS de fidelización para pequeños negocios, con campañas de sellos digitales, tarjetas de clientes y redención de recompensas. Su arquitectura separa las operaciones por negocio, la administración de plataforma, las identidades de integración y las notificaciones en segundo plano. El desafío consiste en soportar procesos comerciales reales, proteger los límites entre negocios y mantener trazables los despliegues.

La documentación interna registra el **despliegue de v0.2.1 el 3 de noviembre de 2026**, con comprobaciones de salud de la aplicación y entrega de imágenes de campañas. Este caso explica decisiones y límites de evidencia, sin publicar código privado.

## 2. Contexto

Una plataforma de fidelización coordina campañas, clientes, progreso y recompensas. Paralelamente, la operación de plataforma gestiona planes, cuotas y ciclo de vida de negocios. Las integraciones y comunicaciones asíncronas exigen límites claros: ningún integrador debe seleccionar arbitrariamente datos de otro negocio, y enviar una notificación no equivale a confirmar una transacción.

## 3. Problema y restricciones

Se necesitan límites de datos por negocio en las interfaces y APIs; eventos y operaciones auditables; controles de planes y consumo; configuración segura de proveedores; trabajo asíncrono confiable y despliegues gestionables por un equipo pequeño.

Las restricciones incluyen presupuesto operativo, entregas incrementales, privacidad de datos empresariales y personales, dependencia de proveedores y necesidad de conservar historial verificable.

## 4. Drivers arquitectónicos

**Aislamiento entre negocios, integridad de recompensas, seguridad, mantenibilidad, observabilidad, despliegue controlado y trazabilidad.** No todos los flujos comparten el mismo grado de validación.

## 5. Límites del sistema

- **Dominio negocio:** campañas, asociación de clientes, tarjetas, sellos, recompensas y redenciones.
- **Control de plataforma:** planes, cuotas, gobierno de negocios y acciones administrativas privilegiadas.
- **Integraciones:** credenciales y contratos distintos para negocio y plataforma.
- **Procesamiento asíncrono:** notificaciones, eventos de salida, reintentos y tareas programadas.
- **Proveedores externos:** mensajería, pagos y hosting; las transacciones de fidelización mantienen su autoridad en el dominio del producto.

## 6. Arquitectura lógica sanitizada

```text
       Negocios / clientes          Operadores de plataforma
                |                             |
                +-------- Interfaz web -------+
                              |
                      Capa de aplicación
                       Laravel / Livewire
                              |
                    Acciones y políticas
                              |
                +-------------+-------------+
                |             |             |
          Fidelización   Control plataforma APIs integración
                |             |             |
                +--------- PostgreSQL ------+
                              |
                      Trabajos / eventos
                              |
                   Workers y scheduler
                              |
                     Proveedores externos

       Límite: despliegue controlado con contenedores y proxy
```

Es un diagrama conceptual; no describe hosts, direcciones, topología sensible ni detalles internos de implementación.

## 7. Decisiones, alternativas y compromisos

| Decisión | Justificación | Alternativa / compromiso |
|---|---|---|
| Laravel con Livewire/Blade | Unificar operaciones de dominio y experiencia web en una aplicación mantenible | SPA separada sumaría superficie de integración y despliegue |
| Acciones de dominio para escrituras | Reutilizar reglas entre interfaz e integraciones | Exige disciplina y pruebas para evitar rutas que eludan las acciones |
| Credenciales por negocio | Resolver el negocio desde la identidad, sin aceptar identificadores arbitrarios | Mayor gobierno de credenciales, cuotas y permisos |
| API administrativa separada | Evitar confundir automatización de plataforma con un negocio regular | Límites estrictos de privilegios y auditoría |
| Idempotencia y consultas acotadas | Reducir efectos duplicados y lecturas indiscriminadas | Mayor complejidad de reintentos y clientes |
| Colas, workers y scheduler | Desacoplar proveedores de las transacciones del negocio | Monitoreo, reintentos y fallos operativos |
| Contenedores y gates de release | Reproducibilidad y trazabilidad del despliegue | Mantenimiento y pruebas de restauración pendientes |

No se atribuyen mejoras de rendimiento no medidas.

## 8. Alternativas consideradas

Microservicios separados o frontend SPA independiente permitirían despliegues autónomos, pero aumentarían la carga operativa sin justificación suficiente en la fase documentada. Integrar proveedores directamente en las solicitudes simplificaría el primer desarrollo, a costa de acoplar disponibilidad y latencia. Se priorizaron límites asíncronos cuando aplica.

## 9. Seguridad y privacidad

Las APIs de integración y plataforma tienen identidades diferentes. Sus contratos documentan scopes, consultas acotadas, idempotencia para operaciones específicas y trazabilidad. Se omiten formatos de credenciales, endpoints productivos, nombres internos y mecanismos sensibles de defensa.

La protección de contactos, consentimiento, permisos de mensajería y términos de proveedores requiere revisión independiente. Documentar controles no constituye una prueba de penetración, auditoría completa de privacidad ni activación universal de integraciones.

## 10. Entrega y operación

El producto tiene releases versionados, cambios revisados y etapas diferenciadas de aceptación. Para v0.2.1, la evidencia privada registra imagen construida y desplegada, migración aditiva de imágenes aplicada, salud de aplicación HTTP 200, workers y scheduler activos y entrega de una imagen pública después de corregir una ruta de almacenamiento persistente.

Es evidencia de un corte fechado, no un monitor de disponibilidad en tiempo real.

## 11. Gobierno de ingeniería asistida por IA

DCP Flow organiza el trabajo humano + IA por stacks y contextos, con compuertas de calidad, registros de evidencia y aprobación humana. La IA no sustituye pruebas ejecutadas, revisión de seguridad ni autorización de despliegues.

## 12. Evidencia y validación

Consultar el [registro de evidencia](EVIDENCE.es.md). El release del 3 de noviembre de 2026 respalda **Desplegado** y entrega de imágenes verificada. Hay pruebas funcionales anteriores y checks locales en otras actas, pero las notas revisadas **no** demuestran una regresión integral posterior al incidente, restauración productiva comprobada ni operación sostenida con usuarios reales.

## 13. Resultados y lecciones aprendidas

- Despliegue, health check y smoke test de medios son evidencia concreta, pero no certificación productiva total.
- Las colas y proveedores externos requieren límites operativos explícitos.
- La resolución de negocio por credencial y el uso de acciones de dominio disminuyen rutas alternativas que podrían saltarse reglas.
- Los volúmenes persistentes y las rutas del proxy deben verificarse durante el release.
- Verificar archivos de backup no equivale a restaurarlos.

No se atribuyen métricas de adopción, conversión, ingresos, latencia o disponibilidad sin registros.

## 14. Preguntas pendientes

1. ¿Qué periodo y métricas de uso sostenido permitirán declarar **Validado en producción**?
2. ¿Qué evidencia publicable documenta una restauración real de backup?
3. ¿Qué pruebas completas por rol y proveedor se ejecutaron sobre el SHA desplegado?
4. ¿Qué ajustes de retención, consentimiento y mensajería requieren revisión?
5. ¿Qué límites de carga, colas o fallos justificarían evolucionar la arquitectura?

## Nota de publicación

Caso arquitectónico sanitizado, no espejo del código ni auditoría exhaustiva de seguridad. No se publican credenciales, infraestructura privada, datos de clientes, rutas internas ni instrucciones privilegiadas. La aprobación editorial no implica que todas las pruebas técnicas estén cerradas.
