# Rewi v0.2.1 — Registro público de evidencia

**Corte:** 2026-11-09. **Clasificación:** Desplegado; **no** validado en producción.

| Afirmación | Fuente privada consultada (solo lectura) | Evidencia documentada | Límite |
|---|---|---|---|
| Despliegue de v0.2.1 | Notas `docs/releases/v0.2.1.md`; checkpoint `ai/CURRENT_STATE.md` | Deploy productivo documentado el 2026-11-03 | Corte documental, no auditoría en vivo |
| Salud operativa básica | Mismas notas | Aplicación healthy, health HTTP 200; workers y scheduler iniciados | No demuestra disponibilidad sostenida ni cobertura de todos los flujos |
| Imágenes de campañas | Mismas notas | Ruta de medios corregida, JPEG HTTP 200 y visualización en navegador | No certifica todos los formatos, roles o campañas |
| Cambios de esquema y despliegue | Mismas notas | Migración aditiva registrada como aplicada; build PASS | No implica regresión completa de todas las funcionalidades |
| Integridad de respaldos | Mismas notas | Verificación documentada de archivos, generación y tamaño | **Sin prueba documentada de restore real en PROD** |
| Integraciones y separación por negocio | `docs/integrations/API.md` privado | Contratos con scopes, identidad ligada a negocio, límites de consulta e idempotencia | Contrato disponible no implica proveedor activo |
| Gobernanza de ingeniería | Documentación privada y DCP Flow | Evidencias de aceptación e historial de checks | Pruebas PASS sobre otros SHAs no certifican el release completo |

## Criterios para subir de nivel

- [x] Estado Desplegado respaldado por evidencia de release fechada.
- [ ] Métricas sostenidas y uso real significativo.
- [ ] Ejercicio documentado de restauración de backups.
- [ ] Regresión del SHA productivo y entregas reales de proveedores según las afirmaciones.
- [ ] Revisión independiente de privacidad y seguridad antes de hablar de certificación.

**Regla editorial:** los NO-GO antiguos del README raíz del producto quedan superados por el checkpoint operativo posterior; no deben presentarse como bloqueos vigentes. No se modificó el repositorio privado.
