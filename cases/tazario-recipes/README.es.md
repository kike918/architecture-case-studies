# Tazario Recipes by SipDolce — Caso de arquitectura

🌐 **Idiomas:** [English](README.md) · Español

**Estado:** Caso de arquitectura sanitizado publicado (revisión humana de divulgación aprobada el 2026-11-09). **Nivel de evidencia:** arquitectura y preparación de despliegue documentadas; despliegue productivo y operación sostenida **no verificados**. El código del producto permanece privado.

## 1. Resumen ejecutivo

Tazario Recipes adapta la base [BrewForm](https://github.com/Ardakilic/BrewForm), de licencia MIT, para construir un producto de recetas y conocimiento de café de especialidad de SipDolce Labs. El problema de ingeniería consiste en adaptar una aplicación existente a una identidad, contenidos bilingües, recursos editoriales y modelo operativo propios sin perder procedencia, datos históricos ni mantenibilidad.

La solución utiliza un monorepositorio TypeScript con cliente React/Vite, API Hono, contratos de validación compartidos, persistencia con Drizzle y PostgreSQL. Se documentó un modelo de despliegue contenerizado en Google Cloud Compute Engine. **La preparación documentada no demuestra un despliegue productivo exitoso.**

## 2. Contexto y problema

Las recetas de café incluyen parámetros de preparación, equipos, variedades y descriptores sensoriales que necesitan contenido estructurado y fácil de consultar. Partir de software existente ayuda, pero cambiar la identidad del producto y extender una base de terceros introduce riesgos de integración, licencias, migración de datos y mantenimiento.

El objetivo es conservar la base útil del proyecto original y delimitar claramente el producto propio, la experiencia localizada y los datos operativos.

## 3. Restricciones

- Equipo pequeño y operación con costos controlados.
- Preservar recetas y medios históricos; prohibir reinicios destructivos y migraciones no revisadas.
- Separar activos y código propios de cualquier contribución al proyecto original.
- Conservar la licencia MIT y respetar las licencias independientes del contenido de terceros.
- Ofrecer español e inglés sin confundir traducciones con validación productiva.
- Aislar servicios de desarrollo/prueba de los servicios de producción.
- No revelar código privado, secretos, topología específica ni datos personales.

## 4. Drivers arquitectónicos

**Mantenibilidad, procedencia, integridad de datos, privacidad, localización, operación predecible y despliegue controlado.** Se prioriza la simplicidad frente a microservicios o complejidad prematura.

## 5. Límites del sistema

**Interno:** experiencia web y dominio de recetas/catálogo; API y autorización; esquemas compartidos; persistencia relacional; medios cargados y contenidos editoriales propios.

**Externo:** mantenimiento de BrewForm, dependencias y recursos multimedia de terceros, hosting/registro de contenedores e integraciones de comunicación según configuración.

El diagrama público omite deliberadamente rutas internas, identificadores, topología de red y detalles privilegiados.

## 6. Arquitectura general

```text
                       Usuarios
                          |
                  Aplicación web
                  React / TypeScript
                          |
                    API de aplicación
                      Hono / Node
                          |
                 Contratos compartidos
                         Zod
                          |
             +------------+------------+
             |                         |
       Acceso a datos            Adaptador de medios
       Drizzle / SQL             Almacenamiento
             |
         PostgreSQL

Límite de despliegue: proxy / TLS -> servicios de aplicación
Las herramientas de diagnóstico/prueba no pertenecen a producción.
```

Es un **diagrama lógico sanitizado**, no una especificación de red productiva ni una descripción completa de controles de confianza.

## 7. Decisiones, alternativas y compromisos

| Decisión | Motivo | Alternativa / compromiso |
|---|---|---|
| Adaptar BrewForm | Aprovechar una base funcional existente | Se hereda deuda técnica y se necesitan revisiones de cambios y licencias |
| React + TypeScript y API Hono | Mantener límites coherentes con la base tecnológica | Reescribir en Laravel añadiría costos de migración sin una necesidad demostrada |
| Contratos compartidos y Zod | Reducir divergencia de interpretación entre API y cliente | Exige mantener alineados contratos y validaciones reales |
| PostgreSQL y Drizzle | Modelo relacional y cambios de esquema versionados | El ORM no sustituye revisión de migraciones ni impacto de datos |
| Separación de ambientes | Proteger datos históricos y repetir validaciones | Más configuración operativa |
| Plan contenerizado para GCP | Empaquetado y operación controlada | El equipo debe gestionar parches, respaldos, restauración y monitoreo |
| Límite explícito de contribuciones upstream | Evitar divulgar adaptaciones propietarias | Requiere aislar y revisar cada aporte genérico |

No se atribuyen resultados de rendimiento comparativo sin mediciones.

## 8. Seguridad y privacidad

Los permisos de API, las sesiones, la separación de secretos, la protección de datos y el aislamiento de bases de pruebas requieren validación ejecutable independiente. Un nombre visible no acredita permisos administrativos. La estrategia documental separa servicios de desarrollo y despliegue y prohíbe operaciones destructivas no autorizadas.

**Deuda abierta de privacidad:** la fuente interna documenta pendientes para auditar el consentimiento de registro y diferenciar el aviso de cookies del bloqueo efectivo de rastreadores opcionales. No deben declararse resueltos sin código y pruebas. Se omiten detalles sensibles de implementación.

## 9. Entrega y operación

DCP Flow establece gobierno de ingeniería según el contexto, ramas temporales, compuertas de calidad y aceptación humana. El proyecto privado documenta un despliegue en GCP Compute Engine con proxy, contenedores, servicios de aplicación, PostgreSQL y medios persistentes. El manual cubre configuración, restauración y verificación de salud.

**El manual de despliegue no constituye evidencia de despliegue, restauración, monitoreo ni recuperación de incidentes ejecutados correctamente en GCP.**

## 10. Ingeniería asistida por IA y gobernanza

La IA puede apoyar discovery, implementación, pruebas y documentación, pero las decisiones finales, la interpretación de evidencias, la revisión de licencias y la aprobación de despliegue requieren supervisión humana. Las contribuciones a BrewForm deben originarse separadas del código y activos propios y revisarse antes de publicarlas.

## 11. Evidencia y validación

Consultar el [registro de evidencia](EVIDENCE.es.md). Clasificación respaldada: **arquitectura documentada / despliegue preparado**. Hay trabajo técnico y local descrito en fuentes privadas, pero la evidencia pública revisada aquí **no** demuestra piloto externo controlado, despliegue exitoso en GCP, restauración de respaldo probada ni operación productiva sostenida.

## 12. Resultados

El resultado concreto es una arquitectura de producto documentada y un procedimiento operativo para despliegue. No se afirman métricas no verificadas de disponibilidad, adopción, latencia, certificación de seguridad o impacto comercial.

## 13. Lecciones aprendidas

- Adaptar software abierto requiere límites explícitos de propiedad intelectual, marca y contribuciones.
- Conservar datos y aislar pruebas es tan importante como rediseñar la interfaz.
- Documentos y compuertas deben separar intención, implementación y resultados observados.
- Disponer de un manual de despliegue es un hito, no un certificado de éxito productivo.
- Las imágenes requieren trazabilidad de licencia propia; la licencia del software original no cubre todo el contenido.

## 14. Preguntas abiertas

1. ¿Qué SHA desplegado en GCP y smoke test exitoso serán aceptados?
2. ¿Qué evidencia de **restauración** de respaldos podrá publicarse?
3. ¿Qué controles de consentimiento y bloqueo de rastreadores tienen pruebas ejecutadas?
4. ¿Todas las imágenes editoriales publicadas tienen procedencia, autorización y atribución?
5. ¿Cómo y cuándo evaluar nuevas versiones de BrewForm?
6. ¿Qué evidencia de monitoreo, incidentes y uso real justificará un nivel superior?

## Nota de publicación

Este es un caso sanitizado publicado. No reproduce código propietario, valores internos de infraestructura, datos personales, rutas internas, secretos, registros de clientes ni detalles sensibles de seguridad. La aprobación humana de publicación se otorgó el 2026-11-09; las evidencias técnicas pendientes continúan explícitamente sin verificar.
