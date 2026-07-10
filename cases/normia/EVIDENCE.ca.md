# Normia — Registre d’Evidència

## Propòsit

Separar arquitectura documentada, prototips de referència, implementació en curs i validació futura. Normia encara no es presenta com a validat en producció.

## Escala d’evidència

- **Baseline documentat** — definició aprovada per a implementació.
- **Prototip de referència** — referència UX o de flux, no comportament productiu.
- **Implementació en curs** — bootstrap o codi actiu.
- **Pilot pendent** — requereix validació operacional real.
- **Fase posterior** — seqüenciada després del Golden Flow.
- **Validat en producció** — no reclamat actualment.

## Matriu

| Capacitat | Nivell | Base pública segura |
|---|---|---|
| Definició de producte | Baseline documentat | Master consolidat i baseline de projecte |
| Arquitectura MVP | Baseline documentat | Arquitectura congelada; canvis estructurals requereixen ADR i aprovació humana |
| Principis UX mobile-first i task-driven | Baseline documentat | Principis de producte definits |
| Prototip UX | Prototip de referència | v0.1 explícitament no productiu |
| Discovery del pilot | En curs | Sprint 0 i aixecament real |
| Monòlit modular | Baseline / bootstrap en curs | Disseny Laravel documentat |
| Single-tenant per instal·lació | Baseline arquitectònic | Estratègia MVP definida |
| Rols i permisos | Baseline de domini | Operator, Supervisor, Admin i Auditor definits |
| Execució de tasques | Golden Flow definit | Vertical slice especificat |
| Control de temperatura | Golden Flow definit | Mesura, perfil i avaluació especificats |
| Gestió de desviacions | Model de domini definit | Paths conforme/no conforme definits |
| Contenció | Model de domini definit | Diferenciada de l’acció correctiva |
| Cicle CAPA | Model de domini definit | Estats explícits definits |
| Verificació supervisor | Model de domini definit | Cicle aprovar/retornar especificat |
| Cicle documental | Baseline de domini | Estats i versionat definits |
| Storage sensible privat | Baseline arquitectònic | Patró d’accés controlat definit |
| Audit events | Baseline arquitectura/domini | Esdeveniments candidats i separació de ledger definits |
| Audit ledger local | Arquitectura definida | Implementació pendent |
| Hash chain | Fase posterior | Després del flux operacional |
| Merkle batching | Fase posterior | Arquitectura definida |
| Polygon testnet | Fase posterior | Arquitectura definida |
| Polygon producció | Fase posterior | Requereix validació prèvia |
| Telegram Bot/Mini App | Arquitectura de canal definida | Utilitat operacional pendent de validar |
| n8n | Límit arquitectònic definit | Implementació i operació pendents de validar |
| Validació productiva | No reclamada | Evidència encara insuficient |

## Evidència requerida per aprovar el Golden Flow

- funciona en un telèfon real;
- permisos Operator/Supervisor correctes;
- rutes conforme i no conforme completes;
- no es destrueix historial;
- tests de domini i permisos;
- audit events generats des del backend;
- errors sense estats impossibles;
- revisió humana;
- documentació alineada amb la implementació.

## Disciplina d’afirmacions

El cas pot descriure arquitectura, modelatge de domini i direcció d’implementació. No ha d’afirmar certificació regulatòria, millora del compliment, acceptació d’auditoria, escala productiva o verificació blockchain productiva sense evidència suficient.
