# Normia

🌐 **Idiomas:** [English](README.md) · Español · [Català](README.ca.md)

**Estado:** Caso de arquitectura e implementación en progreso. Sprint 0, bootstrap técnico y discovery del piloto están en curso.

## Resumen ejecutivo

Normia es un sistema digital de control sanitario, cumplimiento documental, ejecución operativa y auditoría verificable para operaciones de alimentos.

El producto se diseña desde un piloto real y no desde una abstracción SaaS genérica. El problema central es conectar controles planificados con evidencia de ejecución, gestión de desviaciones, contención, acciones correctivas, verificación del supervisor e integridad histórica.

La arquitectura actual es un monolito modular Laravel con MySQL como fuente de verdad operacional, UX web mobile-first, contexto QR, Telegram como canal, n8n como orquestador y anclaje agregado opcional de evidencia de auditoría en Polygon PoS.

**Nivel de evidencia:** baseline de arquitectura + prototipo UX de referencia + implementación en curso. No validado en producción.

## Contexto y problema

Una operación pequeña debe poder reconstruir:

```text
PLANEAR → PROGRAMAR → ASIGNAR → EJECUTAR → REGISTRAR → EVALUAR
→ DETECTAR → CONTENER → CORREGIR → VERIFICAR → CONSULTAR → EXPORTAR → AUDITAR
```

Para cada control relevante, Normia debe responder qué debía hacerse, quién, cuándo, qué resultado hubo, si existió desviación, qué contención y corrección se aplicaron, quién verificó y si la evidencia conserva integridad histórica.

Una aplicación de CRUDs y checklists aislados no satisface esta definición.

## Drivers arquitectónicos

- claridad operativa;
- trazabilidad;
- auditabilidad;
- privacidad;
- mantenibilidad;
- usabilidad móvil;
- estados de dominio explícitos;
- resiliencia ante fallos externos;
- integridad de evidencia;
- evolución consciente de costos.

## Arquitectura resumida

```text
Usuarios
  │
  ├── Web / Móvil
  ├── Contexto QR
  └── Telegram Bot / Mini App
          │
          ▼
        Laravel
          │
   Application Services
          │
      Domain Rules
          │
  ┌───────┼───────────┐
  ▼       ▼           ▼
MySQL  Storage      Audit Service
       privado          │
                        ▼
                    Hash Chain
                        │
                        ▼
                  Merkle Batches
                        │
                        ▼
                   Anchor Adapter
                        │
                        ▼
                    Polygon PoS
```

## Golden Flow prioritario

```text
LOGIN → HOY → TAREA → EQUIPO/QR → TEMPERATURA → EVALUACIÓN

CUMPLE → COMPLETAR → AUDIT EVENT

NO CUMPLE → DESVIACIÓN → CONTENCIÓN → ACCIÓN CORRECTIVA
→ EVIDENCIA → VERIFICACIÓN SUPERVISOR → CIERRE → AUDIT EVENTS
```

El flujo no se considera validado con pantallas o CRUDs aislados.

## Decisiones clave

- monolito modular antes que microservicios;
- single-tenant por instalación para el MVP;
- MySQL como fuente de verdad operacional;
- Laravel gobierna reglas y estados;
- Web, QR y Telegram comparten servicios de aplicación;
- n8n orquesta pero no gobierna el dominio;
- audit ledger local antes de blockchain;
- Polygon fuera del camino crítico;
- ningún dato personal o sensible on-chain;
- correcciones por supersesión, no sobrescritura silenciosa.

## Desarrollo asistido por IA

```text
Kike + Codex
backend · dominio · persistencia · autorización · tests · audit · Polygon

Paull + Antigravity
UX · mobile-first · Livewire/Blade/Filament · browser E2E · QA

Branches separadas → PR → cross-review → develop → UAT → main
```

La IA no aprueba producción ni reemplaza revisión humana.

## Evidencia actual

| Capacidad | Nivel |
|---|---|
| Definición de producto | Baseline documentado |
| Arquitectura MVP | Baseline congelado |
| Golden Flow | Definido, implementación pendiente |
| Prototipo UX | Referencia no productiva |
| Discovery del piloto | En curso |
| Monolito modular | Baseline / bootstrap en curso |
| Flujo tarea-temperatura-desviación | Vertical slice planificado |
| CAPA y verificación | Modelo de dominio definido |
| Audit ledger | Arquitectura definida, implementación pendiente |
| Merkle batching | Fase posterior |
| Anclaje Polygon | Fase posterior |
| Validación productiva | No reclamada |

## Aprendizajes iniciales

- un checklist no es el dominio;
- ejecución y conformidad son conceptos distintos;
- contención y acción correctiva no son equivalentes;
- blockchain no demuestra verdad física;
- los canales no deben duplicar reglas;
- la excepción importa tanto como el check verde;
- el piloto real debe guiar la generalización.

## Documentos relacionados

- [`ARCHITECTURE.es.md`](ARCHITECTURE.es.md)
- [`DECISIONS.es.md`](DECISIONS.es.md)
- [`SECURITY_AND_PRIVACY.es.md`](SECURITY_AND_PRIVACY.es.md)
- [`EVIDENCE.es.md`](EVIDENCE.es.md)

---

Este caso distingue explícitamente arquitectura documentada, prototipos de referencia, implementación en curso y validación futura. Normia no se presenta como validado en producción.
