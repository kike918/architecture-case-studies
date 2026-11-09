# Casos de Estudio de Arquitectura

🌐 **Idiomas:** [English](README.md) · Español

Casos de estudio públicos y sanitizados sobre arquitectura de software, restricciones reales de negocio, trade-offs técnicos y entrega práctica de productos digitales.

> Este repositorio documenta cómo se enmarcan los problemas, cómo se diseñan arquitecturas y cómo se evalúan decisiones técnicas. No expone código fuente privado, credenciales, datos confidenciales de clientes ni detalles propietarios de implementación.

## Propósito

Presentar trabajo seleccionado de arquitectura en productos digitales, sistemas empresariales, aplicaciones offline-first, plataformas de engagement, automatización, distribución controlada y trazabilidad.

Cada caso explica contexto de negocio, restricciones, drivers arquitectónicos, límites del sistema, decisiones principales, alternativas, trade-offs, seguridad, evidencia y aprendizajes.

## Roadmap de casos

| Caso | Estado | Enfoque |
|---|---|---|
| [FalconCDT Engagement Platform](cases/falconcdt-engagement/README.es.md) | Publicado v1 | White-label engagement, scoring, notificaciones y operación |
| [DCP DownloadGate](cases/dcp-downloadgate/README.es.md) | Publicado; evidencia desplegada | Distribución controlada de archivos privados, accesos temporales, límites protegidos en hosting y auditabilidad |
| [MicroPOS](cases/micropos/README.es.md) | Web comercial/mini CRM documentados; baseline POS edge publicado, piloto Raspberry Pi pendiente | Operación comercial Astro/PHP/SQLite y, por separado, POS offline-first y adapters ERP propuestos |
| [Normia](cases/normia/README.es.md) | Baseline arquitectónico publicado; desarrollo pausado | Operación alimentaria, cumplimiento, acciones correctivas y auditoría verificable |

Los casos se publican progresivamente. Un baseline arquitectónico no se presenta como implementación terminada ni validación productiva hasta que exista evidencia.

## Casos adicionales publicados y candidatos

Los siguientes casos incluyen trabajos técnicos publicados y candidatos todavía sin publicar. Publicación no equivale a validación productiva:

| Caso / candidato | Estado editorial | Enfoque arquitectónico |
|---|---|---|
| [Rewi v0.2.1](cases/rewi/README.es.md) | Caso publicado — Desplegado (2026-11-03); no validado en producción | SaaS Laravel de fidelización, aislamiento de negocios, integraciones por ámbito, colas y evidencia de release |
| [Tazario Recipes](cases/tazario-recipes/README.es.md) | Caso de arquitectura publicado — despliegue GCP preparado, producción sin verificar | Monorepo React/Hono/Drizzle, atribución MIT, persistencia aislada, plan de despliegue y límites de evidencia |
| [DCP Flow](cases/dcp-flow/README.es.md) | Caso metodológico publicado — aplicación documentada, resultados no cuantificados | Gobierno humano + IA, evaluación de soluciones, blueprints por stack, skills y gates basados en evidencia |
| [SipDolce Labs](cases/sipdolce-labs/README.es.md) | Caso publicado — web v1 desplegada; cambios posteriores en desarrollo | Astro/TypeScript SSG bilingüe, companion PHP/SQLite y gobierno editorial |

Ser candidato no equivale a un caso publicado ni a validación productiva. La [documentación DCP Flow](https://dcpflow.digitalconsultingplus.co/) proporciona contexto metodológico público.

## Principios de publicación

- Evidencia antes que afirmaciones.
- Decisiones antes que diagramas.
- Contexto antes que tecnología.
- Trade-offs antes que hype.
- Sanitización antes de publicar.
- Nada de datos confidenciales.
- Nada de credenciales o secretos productivos.
- Nada de detalles de cliente sin autorización.

## Ciclo de vida

```text
Candidato
   ↓
Revisión de evidencia
   ↓
Borrador sanitizado
   ↓
Revisión de arquitectura
   ↓
Revisión pública
   ↓
Publicado
   ↓
Actualizado cuando cambia la evidencia
```

## Estado

**Fase:** FalconCDT, DCP DownloadGate y Rewi tienen casos publicados con evidencia de despliegue y distintos niveles de validación; Normia continúa pausado y el piloto Raspberry Pi de MicroPOS sigue planificado. Tazario Recipes tiene arquitectura publicada y despliegue preparado, sin operación productiva confirmada.  
**Siguiente hito:** Actualizar la evidencia al cerrar nuevos releases y pilotos controlados, incluido el próximo release editorial de SipDolce Labs y el laboratorio edge de MicroPOS.
