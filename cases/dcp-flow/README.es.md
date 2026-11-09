# DCP Flow — Arquitectura de una metodología de ingeniería humano + IA

🌐 **Idiomas:** [English](README.md) · Español

**Estado:** Caso público sanitizado de metodología y gobierno de ingeniería. **Clasificación de evidencia:** método documentado y aplicado con evidencias seleccionadas de proyectos; no implica adopción universal, certificación independiente ni mejora de productividad medida.

## 1. Resumen ejecutivo

DCP Flow es la metodología versionada de Digital Consulting Plus para transformar problemas empresariales en resultados revisados y respaldados por evidencia, acumulando conocimiento de ingeniería. Su **Engineering System** materializa la dimensión técnica mediante estándares transversales, blueprints por contexto, skills reutilizables, Quality Gates, decisiones documentadas y gobierno de repositorios. Kai puede interpretar y operar el método, pero no constituye una autoridad independiente.

Este es un caso sobre la **arquitectura de un método de ingeniería**, no sobre un SaaS desplegado. El diseño de gobierno está documentado y diversas prácticas han sido utilizadas en proyectos distintos, con límites de evidencia específicos para cada uno.

## 2. Contexto y problema

La IA puede acelerar la escritura de código, pero también favorecer desvíos arquitectónicos, afirmaciones sin pruebas o mezcla de supuestos técnicos incompatibles. Una empresa que desarrolla SaaS, webs editoriales, aplicaciones TypeScript y sistemas ERP necesita reglas reutilizables sin imponer un runtime único.

El problema consiste en hacer trazables las decisiones de tecnología y reutilización, alinear a los agentes con el contexto real del proyecto, escoger pruebas proporcionales al riesgo y mantener responsabilidad humana en cambios sensibles.

## 3. Restricciones

- Cada producto tiene límites de dominio, runtime, hosting y regulación distintos.
- Antes de construir, se evalúan productos existentes, especialmente open source.
- La verdad del proyecto, Git y las pruebas ejecutadas prevalecen sobre resúmenes y planes no ejecutados.
- Separación explícita entre normas y manuales explicativos.
- Los asistentes no autorizan por sí solos merges, cambios de seguridad ni releases productivos.
- Las skills son guías contextuales, no comandos universales.
- La documentación y las evidencias deben ser sostenibles para un equipo pequeño.

## 4. Drivers arquitectónicos

**Coherencia de gobierno, trazabilidad, reproducibilidad, mantenibilidad, relevancia contextual, seguridad del cambio y responsabilidad humana.**

## 5. Límites del sistema y cadena de autoridad

```text
                   Intención aprobada por humano
                              |
                        Método DCP Flow
                              |
                     Constitución / Standards
                              |
                  Stack Blueprint seleccionado
                    + perfil runtime/deploy
                              |
                 Verdad del proyecto + ADR aceptado
                              |
                 Skills elegibles / herramientas
                              |
                   Implementación y evidencia
                              |
                  Quality Gates según riesgo
                              |
                       Aceptación humana
                              |
                  Aprendizaje y evolución
```

Es un modelo lógico de **autoridad de decisión**, no de infraestructura. El Human Handbook y el micrositio son proyecciones explicativas **no normativas**. El catálogo de herramientas/MCP informa, pero su existencia no concede permisos ni altera los estándares canónicos.

## 6. Decisiones, alternativas y trade-offs

| Decisión | Justificación | Alternativa y compromiso |
|---|---|---|
| Una metodología transversal | Evitar sistemas competidores de gobierno | Marcos independientes por equipo generan ambigüedad |
| Solution Discovery Gate antes de construir | Evitar rehacer capacidades maduras | Construir siempre simplifica el inicio, pero encarece el mantenimiento |
| ADOPT / CONFIGURE / INTEGRATE / EXTEND / BUILD | Registrar decisiones evaluadas y no preferencias por generar código | Una secuencia mecánica ignora contexto y riesgos |
| Blueprints por stack | Preservar convenciones nativas Laravel, Astro, TypeScript y ERP | Una plantilla universal produce contaminación entre stacks |
| Proveedor después del stack | GCP o un hosting no definen arquitectura de aplicación | Elegir primero el proveedor puede sesgar el diseño |
| Skills seleccionadas por contexto | Cargar solo conocimiento útil para tarea y runtime | Cargar todo introduce ruido y contradicciones |
| Gates según riesgo y evidencia | Ajustar pruebas al impacto de fallos | Checklists fijos pueden provocar falsa seguridad |
| Gate humano de release | Mantener responsabilidad por consecuencias reales | Promoción autónoma reduce fricción pero elimina control apropiado |

## 7. Modelo de entrega y operación

La ruta canónica sigue problema → discovery/evaluación de soluciones → clasificación de producto → blueprint/runtime → contexto del proyecto → skills pertinentes → implementación → Quality Gates según riesgo → evidencia/PR → decisión humana. El gobierno habitual diferencia ramas de trabajo, integración y baseline estable aceptada.

Los estados de los Quality Gates son **PASS / FAIL / NOT RUN / NOT APPLICABLE / BLOCKED**. Una prueba sin ejecutar no puede declararse PASS. Los veredictos expresan preparación para revisión humana, no autorización automática.

Cada entorno utiliza un perfil de runtime y proveedor apropiado. Una dependencia TypeScript en Laravel o una isla React en Astro no cambia por sí misma la clasificación de la aplicación.

## 8. Seguridad, privacidad y gobierno de IA

Las fuentes contemplan autorización, secretos, migraciones, cadena de suministro, ejecución y evidencia según riesgo. Las acciones sensibles requieren aprobación humana. Se omiten credenciales de agentes, inventarios privados y rutas de acceso a servidores.

Las reglas documentadas no equivalen a controles técnicamente impuestos en todos los repositorios; su cumplimiento real depende de permisos y ejecución.

## 9. Ingeniería asistida por IA

La IA puede explorar alternativas, proponer cambios, ejecutar verificaciones y resumir evidencias dentro del alcance aprobado. Kai actúa como orquestador bajo DCP Flow; no reemplaza decisiones normativas ni aceptación humana. Las skills son conocimiento operativo gobernado, no una segunda metodología.

## 10. Evidencia y validación

Ver el [registro de evidencia](EVIDENCE.es.md). La fuente canónica respalda la taxonomía de decisiones, el catálogo de blueprints, el proceso de evaluación y los Quality Gates. Los registros históricos incluyen contextos Laravel SaaS, PHP ligero y webs Astro, con límites explícitos. El blueprint de aplicación Fullstack TypeScript permanece **EVOLVING** mientras se acumula evidencia reproducible de foundation, CI y release.

No hay base aquí para afirmar mejoras cuantificadas de tiempos de entrega, defectos, costos ni cumplimiento universal.

## 11. Resultados y aprendizajes

- Una metodología puede gobernar diferentes stacks **sin mezclar sus reglas técnicas**.
- La evaluación de soluciones existentes debe preceder a la implementación.
- Hay que separar lo obligatorio, lo construido y lo efectivamente observado.
- Un checklist aparentemente verde no demuestra calidad si faltan pruebas críticas.
- El contenido público debe explicar la fuente canónica, no competir con ella.

## 12. Preguntas abiertas

1. ¿Qué métricas comparables demostrarían mejoras en tiempo de entrega y defectos?
2. ¿Qué blueprints tienen evidencias suficientes para avanzar desde EVOLVING?
3. ¿Con qué frecuencia reconciliar catálogos y enlaces con experiencia real?
4. ¿Cuál es la evidencia mínima proporcional para proyectos de distinto tamaño?
5. ¿Cómo reforzar validaciones automatizadas sin reemplazar la revisión humana?

## Nota editorial

El caso describe una metodología documentada y aplicaciones históricas seleccionadas. No reproduce código privado, datos de clientes, secretos ni infraestructura interna. Consultar la [documentación pública de DCP Flow](https://dcpflow.digitalconsultingplus.co/) para la guía publicada vigente.
