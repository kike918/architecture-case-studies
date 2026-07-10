# FalconCDT Engagement Platform — Seguridad y Privacidad

## Alcance

Este documento resume principios públicos y sanitizados de seguridad y privacidad. No expone infraestructura privada, credenciales, endpoints internos ni configuraciones confidenciales de clientes.

## 1. Autenticación y autorización

La aplicación separa responsabilidades de participantes y administradores.

Principios:

- sesiones autenticadas para áreas protegidas;
- rutas administrativas protegidas por roles;
- rutas de participante sin privilegios administrativos;
- estado de cuenta con impacto sobre acceso;
- acciones privilegiadas auditables.

## 2. Gestión de secretos

El repositorio no debe contener:

- archivos `.env`;
- credenciales SMTP;
- tokens Telegram;
- secretos de automatización;
- API keys;
- backups privados;
- logs productivos;
- archivos subidos por usuarios.

Los secretos permanecen fuera del control de versiones.

## 3. Hardening de capa web

El modelo de despliegue incorpora reglas para:

- bloquear acceso directo a rutas privadas;
- impedir ejecución de scripts en directorios de uploads;
- bloquear extensiones sensibles y archivos de metadatos;
- reducir exposición accidental de configuración y documentación operativa.

## 4. Protección de endpoints de automatización

Los workflows externos usan endpoints protegidos en lugar de acceso directo a la base productiva.

Controles:

- secreto compartido de automatización;
- restricción opcional por IP;
- autorización en capa de aplicación;
- credenciales de base de datos fuera de n8n.

## 5. Logging y redacción

Los logs no deben convertirse en un almacén secundario de secretos.

Principios:

- redacción de valores sensibles conocidos;
- evitar dumps de credenciales;
- separar debugging de logs seguros para producción;
- mantener debug productivo deshabilitado.

## 6. Privacidad de participantes

```text
Ranking público
        ≠
Historial detallado público de pronósticos
```

Un participante puede aparecer en la clasificación agregada sin exponer automáticamente su comportamiento detallado.

## 7. Proveedores externos

Las APIs externas son límites de confianza.

- claves fuera del repositorio;
- payloads normalizados antes del uso de dominio;
- proveedores secundarios sin capacidad de sobrescribir la verdad oficial de scoring;
- degradación segura cuando falla una integración opcional.

## 8. Uploads y contenido

- bloqueo de ejecución en uploads;
- separación entre código y archivos generados/subidos;
- sanitización allowlist para contenido HTML enriquecido.

## 9. Riesgos operativos

- drift entre configuración SQL local y hosting;
- patches no aplicados;
- diferencias de timezone;
- errores de credenciales de notificación;
- caídas de proveedores externos;
- fallos en procesamiento de colas;
- activación accidental de debug en producción.

Estos riesgos se gestionan con checkpoints de release, checklists, validación por ambiente y procedimientos de rollback.

## 10. Límite de divulgación pública

Este caso no publica:

- credenciales productivas;
- endpoints privados;
- rutas internas de servidor;
- detalles de esquema innecesarios;
- configuraciones privadas de clientes;
- logs productivos;
- datos personales de participantes.
