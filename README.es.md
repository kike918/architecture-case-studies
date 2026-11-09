# Casos de Estudio de Arquitectura

🌐 **Idiomas:** [English](README.md) · Español

Casos de estudio públicos y sanitizados sobre arquitectura de software, restricciones reales de negocio, trade-offs técnicos y entrega práctica de productos digitales.

> Este repositorio documenta cómo se enmarcan los problemas, cómo se diseñan arquitecturas y cómo se evalúan decisiones técnicas. No expone código fuente privado, credenciales, datos confidenciales de clientes ni detalles propietarios de implementación.

## Propósito

Presentar trabajo seleccionado de arquitectura en productos digitales, sistemas empresariales, aplicaciones offline-first, plataformas de engagement, automatización, distribución controlada y trazabilidad.

Cada caso explica contexto de negocio, restricciones, drivers arquitectónicos, límites del sistema, decisiones principales, alternativas, trade-offs, seguridad, evidencia y aprendizajes.

## Casos publicados — 8

Los ocho casos están **publicados editorialmente**, pero tienen niveles de evidencia técnica diferentes. Consultar cada registro antes de deducir validación productiva.

| Caso | Estado editorial / técnico | Alcance |
|---|---|---|
| [FalconCDT Engagement Platform](cases/falconcdt-engagement/README.es.md) | Publicado v1 · Desplegado | Engagement white-label, scoring, notificaciones y operación |
| [DCP DownloadGate](cases/dcp-downloadgate/README.es.md) | Publicado · Desplegado (evidencia documentada) | Distribución controlada, accesos temporales y almacenamiento protegido |
| [MicroPOS](cases/micropos/README.es.md) | Publicado · web comercial documentada; POS edge Concept / piloto pendiente | Web comercial Astro/PHP/SQLite y arquitectura POS offline-first separada |
| [Normia](cases/normia/README.es.md) | Publicado · baseline Concept/prototipo; desarrollo pausado | Cumplimiento sanitario, acciones correctivas y registros verificables |
| [Rewi v0.2.1](cases/rewi/README.es.md) | Publicado · Desplegado 2026-11-03; validación sostenida pendiente | SaaS Laravel de fidelización, integraciones delimitadas, colas y release |
| [Tazario Recipes](cases/tazario-recipes/README.es.md) | Publicado · implementación documentada; despliegue preparado, no verificado | TypeScript React/Hono/Drizzle, atribución upstream y plan GCP |
| [DCP Flow](cases/dcp-flow/README.es.md) | Publicado · Metodología (madurez producto N/A); aplicación documentada | Método humano + IA, discovery, blueprints contextuales y Quality Gates |
| [SipDolce Labs](cases/sipdolce-labs/README.es.md) | Publicado · v1 Desplegada; cambios editoriales posteriores en desarrollo | Sitio editorial bilingüe Astro SSG y formularios PHP/SQLite acotados |

**No hay candidatos inéditos listados en este corte.** Todo futuro candidato requiere evidencia, sanitización, revisión arquitectónica y aprobación de publicación. Los cinco niveles técnicos están en el [Estándar de publicación](docs/PUBLICATION_STANDARD.md); los casos de metodología usan N/A.

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

**Fase:** Ocho casos públicos con madurez distinta y explícitamente delimitada. Rewi, FalconCDT y DCP DownloadGate tienen evidencia de despliegue; SipDolce Labs v1 figura desplegada; GCP Tazario y piloto edge MicroPOS siguen sin verificar; Normia está pausado; DCP Flow es una metodología.  
**Siguiente hito:** Actualizar evidencia cuando se verifiquen nuevos releases o pilotos.
