# FalconCDT Engagement Platform

🌐 **Idiomes:** [English](README.md) · [Español](README.es.md) · Català

**Estat:** Cas publicat — resum públic i sanititzat d’arquitectura basat en una plataforma B2B white-label d’engagement operativa.

## Resum executiu

FalconCDT Engagement Platform va evolucionar des d’una implementació real de pronòstics cap a una plataforma B2B reutilitzable per a marques, negocis, comunitats i campanyes privades.

El repte arquitectònic principal no era només registrar pronòstics. Calia suportar un model operatiu reutilitzable amb registre de participants, zona privada d’usuari, administració, deadlines, scoring, rànquings per fase, missatgeria, notificacions, auditoria, branding i desplegaments per a diferents clients sense introduir prematurament una arquitectura SaaS multi-tenant complexa.

La solució actual utilitza una arquitectura lleugera PHP/MySQL amb separació entre serveis i repositoris, desplegaments white-label independents per instància, cues de notificació, endpoints d’automatització protegits i separació explícita entre la font oficial de resultats i els proveïdors secundaris d’enriquiment visual.

**Nivell d’evidència:** `Desplegat`, amb ús operatiu i hardening orientat a producció; algunes integracions i millores UX continuen al roadmap.

## Problema

La plataforma havia de reconciliar dues necessitats:

1. **Reutilització de producte:** scoring, rànquing, administració, notificacions i auditoria compartits.
2. **Aïllament per client:** branding, regles, participants, premis, configuració i calendaris operatius diferents.

L’arquitectura també havia de mantenir-se operable per un equip petit i desplegable en infraestructura pràctica sense sobredimensionar prematurament el producte.

## Restriccions principals

- equip petit;
- necessitat de lliurament ràpid;
- personalització real per client;
- baixa justificació inicial per al multi-tenancy;
- restriccions d’hosting;
- APIs externes amb límits i diferències;
- privacitat de l’historial de pronòstics;
- necessitat de scoring i auditoria verificables;
- fiabilitat variable del cron de l’hosting;
- canals de notificació amb modes de fallada diferents;
- secrets fora del control de versions.

## Drivers arquitectònics

- simplicitat de desplegament;
- aïllament operatiu;
- auditabilitat;
- mantenibilitat;
- claredat de les fonts de dades;
- automatització controlada;
- privacitat;
- extensibilitat sense sobrearquitectura;
- control de costos.

## Arquitectura resumida

```text
Participants / Admins
        │
        ▼
 Aplicació Web
 PHP + HTML/CSS/JS
        │
        ├── Controllers
        ├── Services
        ├── Repositories
        ├── Providers
        └── Views
        │
        ▼
 MySQL / MariaDB
 font de veritat operacional
        │
        ├── scoring i rànquings
        ├── fases i guanyadors
        ├── cues de notificació
        ├── configuració
        └── auditoria

Integracions externes
        │
        ├── proveïdor oficial de resultats
        ├── proveïdor opcional d’enriquiment
        ├── SMTP
        ├── Telegram
        └── n8n com a orquestrador
```

## Decisions clau

- multi-instància abans que multi-tenancy;
- MySQL com a font runtime de veritat;
- un únic proveïdor oficial per a decisions de scoring;
- proveïdors secundaris només per a enriquiment;
- regles de negoci als serveis;
- SQL als repositoris;
- notificacions per plantilles i cues;
- n8n com a orquestrador, no com a propietari del domini;
- endpoints d’automatització protegits;
- rànquing públic separat de l’historial privat de pronòstics.

## Seguretat i privacitat

Principis públics documentats:

- secrets fora de Git;
- debug de producció desactivat;
- rutes privades protegides;
- execució de scripts bloquejada als uploads;
- secrets coneguts redactats dels logs;
- endpoints d’automatització protegits;
- rànquing públic sense exposar automàticament l’historial detallat del participant;
- accions administratives sensibles auditables.

## Evidència

| Capacitat | Nivell |
|---|---|
| Registre i autenticació | Desplegat |
| Pronòstics i deadline enforcement | Desplegat |
| Scoring i rànquing per fase | Desplegat |
| Mòduls administratius | Desplegat |
| Tancament de fases, guanyadors i premis | Desplegat / validat en release |
| Email | Desplegat |
| Telegram | Desplegat |
| Resum diari admin | Desplegat |
| Sincronització de resultats oficials | Desplegat |
| Detall enriquit opcional | Implementat, dependent de la integració |
| Orquestració n8n | Parcial |
| WhatsApp Bridge | Roadmap |
| Hardening responsive global | Roadmap |
| Multi-tenancy compartit | No implementat per decisió arquitectònica |

## Resultats públics segurs

L’evidència permet afirmar que la plataforma va evolucionar d’una dinàmica real d’engagement cap a una base de producte multi-instància reutilitzable sense introduir complexitat SaaS prematura.

No es publiquen afirmacions no verificades sobre ingressos, conversió, creixement d’usuaris, disponibilitat o escala.

## Aprenentatges

### Multi-instància pot ser la decisió correcta al principi

Separar desplegaments per client pot ser preferible mentre encara s’estan validant diferències operatives reals.

### Una única font ha de decidir la veritat oficial

Els proveïdors secundaris poden enriquir l’experiència, però no han de competir per modificar el mateix fet de negoci.

### Automatització no és sinònim de domini

n8n pot activar processos i notificacions; scoring, rànquing i estats continuen dins de l’aplicació.

### L’operació també és arquitectura

Backups, rollback, patches i checkpoints de release formen part del disseny tècnic real.

### La privacitat també importa en productes d’engagement

Un rànquing públic no obliga a exposar l’historial detallat del participant.

## Pròximes preguntes arquitectòniques

- Quan el cost de múltiples instàncies justifica multi-tenancy?
- Quines configuracions han de viure en dades, codi o automatització de desplegament?
- Quan les notificacions requereixen workers dedicats?
- Quan convé migrar a desplegaments containeritzats?
- Quin nivell d’observabilitat està justificat per l’evidència operativa?
- Com generalitzar el producte més enllà dels pronòstics esportius sense debilitar el domini?

## Documents relacionats

- [`ARCHITECTURE.ca.md`](ARCHITECTURE.ca.md)
- [`DECISIONS.ca.md`](DECISIONS.ca.md)
- [`SECURITY_AND_PRIVACY.ca.md`](SECURITY_AND_PRIVACY.ca.md)
- [`EVIDENCE.ca.md`](EVIDENCE.ca.md)

---

Aquest cas exclou intencionadament credencials, endpoints privats, dades confidencials de clients i codi font propietari.
