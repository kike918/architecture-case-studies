# DCP Flow — Registro de evidencia

**Fecha de revisión:** 2026-11-09. **Tipo:** Caso de metodología/gobierno (no despliegue de producto). **Evidencia:** método documentado y referencias históricas seleccionadas.

| Afirmación | Fuente canónica consultada solo en lectura | Estado y límite |
|---|---|---|
| DCP Flow es un método único y Engineering System es su capa técnica | `dcp-flow/README.md` y `DOCUMENTATION.es.md` | Estructura normativa documentada; no un segundo framework |
| Evaluar antes de construir | `standards/solution-discovery-gate.es.md` | Standard EVOLVING; gobierna ADOPT/CONFIGURE/INTEGRATE/EXTEND/BUILD |
| Quality Gates contextuales | `standards/quality-gates.es.md` | Modelo de riesgos y evidencia documentado; no implica ejecución en todos los proyectos |
| Aislamiento entre stacks | `blueprints/README.es.md`, `ai/skills/routing.es.md` | Blueprints Laravel, Astro/Web, Fullstack TypeScript y ERP; skills elegibles según contexto |
| Madurez de TypeScript | `blueprints/fullstack-typescript/README.es.md` | EVOLVING; no es el stack predeterminado universal |
| Reutilización y aprendizaje documentados | `ai/reference-evidence/2026-10-12-cross-project-experience.md` | Referencia fechada, no prueba de operación actual ni de mejoras cuantificadas |
| Proyección pública no normativa | `dcp-flow-docs/README.md` | El micrositio explica sin sustituir la metodología canónica |

## Gates de futuras mejoras

- [x] Fuentes estructurales y normativas inspeccionadas.
- [x] Caso bilingüe con alcance explícito.
- [ ] Medir de forma independiente tiempos de entrega, defectos, costo y reutilización.
- [ ] Verificar cada release antes de atribuir resultados a la metodología.
- [ ] Auditar periódicamente paridad de idiomas y micrositio.

**Importante:** los cinco niveles estándar de evidencia (Concept/Prototype/Pilot/Deployed/Production validated) describen madurez de productos/sistemas. Este caso de método no debe etiquetarse `Production validated` solo porque algunos proyectos estén desplegados.
