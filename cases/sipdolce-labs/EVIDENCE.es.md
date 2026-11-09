# SipDolce Labs — Registro de evidencia

**Corte:** 2026-11-09. Repositorio de producto consultado solo en lectura.

| Afirmación | Fuente consultada | Evidencia y límite |
|---|---|---|
| v1 pública desplegada | `sipdolcelabs-web@dev/README.md`, `ai/CURRENT_STATE.md` | Release v1 cerrado en `main`, Hostinger operativo según documento; no se verificó el runtime en vivo durante esta revisión |
| Arquitectura editorial Astro/TS | `docs/ARCHITECTURE.md`, ADR-0002 | SSG y catálogos tipados; colecciones Markdown/Zod no alimentan los catálogos vigentes |
| Companion transaccional | Arquitectura, runbook y estado | PHP/SQLite WAL y outbox documentados; no es CMS ni producto aparte |
| Build y pruebas | `ai/CURRENT_STATE.md` | 138 páginas estáticas y 36 pruebas backend reportadas PASS; no se ejecutaron de nuevo aquí |
| Cambios CoffeeTech posteriores | `README.md`, `ai/CURRENT_STATE.md` | SLL-WEB-01 integrado en `dev`, sin promoción a nuevo release Hostinger en el corte revisado |
| Derechos y aspectos legales | `docs/ASSET_PROVENANCE.md`, `docs/LEGAL_AND_TRUST.md`, estado actual | Los archivos históricos contienen dudas legales anteriores; el checkpoint posterior confirma identificación de entidad. No demuestra cierre de toda revisión de licencias y privacidad |
| Sistemas de recetas/podcast | ADR-0002 y estado actual | Evaluación de herramientas independientes; no acredita integración productiva |

## Compuertas pendientes
- [x] Separar v1 publicada de cambios posteriores en `dev`.
- [x] Respetar límites TypeScript-first y PHP/SQLite.
- [ ] Confirmar SHA del siguiente release y smoke público Hostinger.
- [ ] Verificar derechos, textos legales y accesibilidad según afirmaciones.
- [ ] Verificar integraciones antes de publicitarlas como productivas.

**Clasificación:** Web v1 desplegada (documentado); nuevas funciones editoriales en desarrollo; no se afirma validación productiva sostenida.
