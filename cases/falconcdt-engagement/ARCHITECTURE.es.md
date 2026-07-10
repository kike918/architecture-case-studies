# FalconCDT Engagement Platform — Arquitectura

## Propósito

Describir la arquitectura pública y sanitizada de FalconCDT Engagement Platform sin exponer detalles privados de implementación ni información confidencial de clientes.

## Estilo arquitectónico

El producto actual utiliza una arquitectura ligera por capas en PHP respaldada por MySQL/MariaDB.

```text
Rutas web
    ↓
Controllers
    ↓
Services
    ↓
Repositories / Providers
    ↓
MySQL + integraciones externas
```

Las responsabilidades se separan de forma intencional:

- los controllers coordinan requests y responses;
- los services contienen reglas de negocio;
- los repositories contienen acceso SQL;
- los providers aíslan servicios externos;
- las views no ejecutan SQL directamente.

## Modelo de despliegue

El producto usa actualmente un modelo white-label multi-instancia.

```text
Instancia Cliente A
├── aplicación
├── base de datos
├── branding
├── reglas
└── configuración de notificaciones

Instancia Cliente B
├── aplicación
├── base de datos
├── branding
├── reglas
└── configuración de notificaciones
```

No es una arquitectura multi-tenant con base compartida.

### Por qué

El modelo prioriza:

- aislamiento operativo más simple;
- configuración específica por cliente más segura;
- límites de fallo más claros;
- rollback más sencillo de razonar;
- menor complejidad mientras se valida el producto.

El costo es la duplicación del trabajo de despliegue y actualización.

## Flujo principal de datos

```text
Participante
    │
    ▼
UI de pronósticos
    │
    ▼
Validación backend de deadline
    │
    ▼
Persistencia del pronóstico
    │
    ├── auditoría
    └── enforcement de bloqueo

Proveedor oficial de resultados
    │
    ▼
Capa de normalización / sincronización
    │
    ▼
Estado oficial en MySQL
    │
    ▼
Servicio de scoring
    │
    ▼
Leaderboard por fase
    │
    ▼
Ranking público
```

## Modelo de fases

La arquitectura trata las fases como límites de primer nivel.

```text
Fase
  ├── partidos/eventos
  ├── contexto de scoring
  ├── leaderboard
  ├── ganador
  └── configuración de premio
```

Esto permite tener periodos de ranking independientes sin eliminar puntajes históricos.

## Separación de fuentes de resultados

La arquitectura diferencia verdad oficial de enriquecimiento opcional.

```text
Proveedor oficial
    │
    ├── estado final
    ├── marcador oficial
    ├── trigger de scoring
    └── impacto en ranking

Proveedor de enriquecimiento
    │
    ├── estado live
    ├── minuto
    ├── sede
    ├── árbitro
    ├── eventos
    ├── estadísticas
    └── alineaciones
```

Un proveedor secundario no puede sobrescribir la verdad oficial de scoring.

## Arquitectura de notificaciones

```text
Evento de dominio / acción programada
        ↓
Plantilla de notificación
        ↓
Cola específica por canal
        ↓
Procesador
        ├── Email
        ├── Telegram
        └── Canales futuros
```

Objetivos:

- separación por canal;
- reutilización de plantillas;
- reintentos controlados;
- visibilidad operativa;
- posibilidad de procesamiento manual cuando sea necesario.

## Límite de automatización

n8n se trata como orquestador externo.

```text
Schedule n8n
    ↓
HTTPS request
    ↓
Endpoint de automatización protegido
    ↓
Servicio de aplicación
    ↓
Datos de dominio + colas de notificación
```

n8n no debe conectarse directamente a la base productiva para flujos core.

La aplicación conserva la propiedad sobre:

- scoring;
- estado de fases;
- ranking;
- ganadores;
- reglas de generación de notificaciones;
- auditoría.

## Límites de seguridad

```text
Internet
   │
   ▼
Restricciones en capa web
   │
   ├── bloqueo de rutas privadas
   ├── bloqueo de ejecución en uploads
   └── bloqueo de extensiones sensibles
   │
   ▼
Autenticación / autorización
   │
   ├── rutas admin
   └── rutas participante
   │
   ▼
Capa de servicios
   │
   ▼
Base de datos
```

Los endpoints de automatización agregan un límite adicional mediante secreto de automatización y restricciones de red opcionales.

## Arquitectura operativa

La arquitectura incluye como activos de primer nivel:

- secuenciación de patches de base de datos;
- backups;
- rollback;
- checklist de seguridad;
- validación de despliegue;
- checkpoints de release;
- verificación específica por ambiente.

## Triggers de evolución

### Multi-tenancy

Considerarlo cuando el número de clientes, el costo de despliegue y la consistencia de configuración justifiquen un control plane compartido.

### Cues/workers dedicados

Considerarlos cuando el volumen de notificaciones, los reintentos o los requisitos de latencia superen el modelo actual.

### Despliegue containerizado

Considerarlo cuando el drift de ambientes o el costo de actualizar múltiples instancias se vuelva dominante.

### Observabilidad centralizada

Considerarla cuando el volumen de incidentes o la escala requieran métricas, tracing y alertas estructuradas.
