# SipDolce Labs — Arquitectura de plataforma editorial CoffeeTech

🌐 **Idiomas:** [English](README.md) · Español

**Estado:** Caso público de arquitectura sanitizado. **Evidencia:** despliegue v1 en Hostinger documentado; cambios editoriales y de portafolio posteriores integrados en `dev` y **sin promoción a un nuevo release productivo** en el corte del 9 de noviembre de 2026. La web pública y la rama de integración no representan el mismo estado de release.

## 1. Resumen ejecutivo
SipDolce Labs es una web pública bilingüe de investigación y divulgación sobre ciencia del café, CoffeeTech y experimentación. La arquitectura evita tratar un sitio editorial como SaaS, ERP, motor de recetas o tienda virtual. Astro/TypeScript genera contenido estático y un componente PHP/SQLite acotado procesa contacto, boletines y propuestas de colaboración.

## 2. Contexto y problema
Una plataforma de conocimiento cafetero debe agregar recetas, medios, proyectos y contenidos científicos sin reconstruir páginas por cada entrada. Los formularios requieren persistencia confiable; los contenidos y las imágenes exigen procedencia y derechos; los mockups ilustrativos no deben presentarse como resultados logrados.

## 3. Restricciones
- Contenido bilingüe ES/EN y URLs estables.
- Hosting compartido y operación sostenible para un equipo pequeño.
- Conservar diseño y catálogos TypeScript existentes.
- Separar páginas públicas estáticas de datos transaccionales privados.
- Distinguir logos aprobados de mockups conceptuales.
- Evitar afirmaciones científicas, comerciales o legales no verificadas.
- Releases versionados, aprobación humana y recuperación.

## 4. Drivers arquitectónicos
**Simplicidad, agilidad editorial, accesibilidad, privacidad, reproducibilidad, procedencia y bajo costo operativo.**

## 5. Límites del sistema
Dentro del sitio: páginas estáticas, plantillas, catálogos tipados, idiomas, metadatos SEO y activos autorizados. Un companion independiente conserva los envíos y gestiona eventos pendientes para integraciones externas. Fuera del sitio: Tazario Recipes como producto separado, herramientas de podcast en evaluación, proveedores multimedia, fuentes científicas y titulares de derechos.

## 6. Diagrama lógico sanitizado
```text
          Editores / contenido revisado
                       |
           Catálogos TypeScript ES/EN
                       |
               Build Astro SSG
                       |
          Páginas estáticas + SEO
                 + medios autorizados
                       |
                 Navegador público
                       |
          Contacto / boletines / propuestas
                       |
                Companion PHP
                  |         |
           SQLite privado   Outbox
                              |
                       Integraciones externas
```
El modelo omite rutas internas, endpoints concretos, secretos y topología privada.

## 7. Decisiones y trade-offs
| Decisión | Por qué | Alternativa / limitación |
|---|---|---|
| Astro estático | Publicación rápida y de mantenimiento reducido | Cada cambio editorial requiere revisión y build |
| Catálogos TypeScript tipados | Los datos y plantillas existentes funcionan | La edición concurrente no técnica es más exigente |
| Preservar plantillas y slugs | Evitar reescrituras y enlaces rotos | Hay que validar idiomas y esquemas |
| PHP y SQLite privada para formularios | Persistencia transaccional sobre hosting existente | Exige respaldos, aislamiento y operación |
| Outbox de integración | Desacoplar envíos y servicios externos | Reintentos y entregas necesitan supervisión |
| No introducir CMS por defecto | Evitar modelos duplicados y mayor superficie de administración | Reconsiderar si el volumen editorial lo justifica |
| Tazario Recipes independiente | Preservar dominios y ciclos de despliegue | Una integración futura requiere contrato propio |

## 8. Alternativas consideradas
Las Content Collections Markdown/Zod existen como capacidad, pero **no alimentan los catálogos editoriales vigentes**. Adoptar CMS, base de datos editorial o reescribir la aplicación añadiría migraciones y operación sin necesidad demostrada. Herramientas de recetas, podcast y video son candidatos de evaluación, **no integraciones productivas certificadas**.

## 9. Seguridad, privacidad y derechos
La documentación describe almacenamiento privado separado de los archivos estáticos, formularios controlados, mecanismos relacionados con consentimiento y revisión de contenidos legales y de derechos. Eso no implica certificación de seguridad o legal. Los logos originales se distinguen de materiales ilustrativos; cada imagen externa y afirmación científica requiere su propia validación.

## 10. Entrega y operación
DCP Flow gobierna ramas temporales, revisión, pruebas según riesgo y aprobación de release. El flujo contempla generar artefactos estáticos, conservar los datos transaccionales, desplegar en hosting, comprobar comportamiento público y mantener rollback. La v1 pública está documentada como cerrada. Las mejoras CoffeeTech posteriores de SLL-WEB-01 están integradas en `dev`, **todavía no publicadas como nuevo release**.

## 11. Ingeniería asistida por IA
La IA puede proponer textos, estructuras bilingües, cambios y verificaciones, pero la exactitud, identidad visual, licencias, aprobación editorial y autorización de despliegue son responsabilidad humana. Una imagen conceptual no es prueba de que un proyecto o evento exista.

## 12. Evidencia y validación
Consultar el [registro de evidencia](EVIDENCE.es.md). El checkpoint del 9 de noviembre documenta el cierre de v1, un build Astro de 138 páginas y pruebas del backend, además de cambios posteriores en desarrollo. Son resultados reportados por la fuente y **no ejecutados de nuevo durante esta revisión documental**.

## 13. Resultados y aprendizajes
El resultado es una plataforma editorial con componente transaccional acotado, no un CMS construido sin necesidad. Separar la edición de contenidos de la persistencia de integraciones reduce acoplamiento. TypeScript-first es una decisión reversible según métricas de operación editorial. Una web publicada y los cambios de desarrollo deben informarse por separado.

## 14. Preguntas abiertas
1. ¿Qué SHA y smoke público acreditarán el próximo release Hostinger?
2. ¿Qué volumen editorial justificaría nuevas herramientas?
3. ¿Qué fuentes e imágenes requieren validación adicional de procedencia y licencias?
4. ¿Qué flujos de accesibilidad, privacidad y consentimiento tienen comprobación independiente?
5. ¿Cuándo se justificaría una integración API con Tazario Recipes?

## Nota de publicación
Caso sanitizado basado en documentación técnica consultada en lectura. No expone código privado, secretos, rutas internas, envíos de usuarios ni contenidos gráficos no autorizados.
