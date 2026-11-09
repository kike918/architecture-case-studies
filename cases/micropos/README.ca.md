# MicroPOS

🌐 **Idiomes:** [English](README.md) · [Español](README.es.md) · Català

**Estat:** web comercial i mini CRM implementats segons la documentació; arquitectura POS edge publicada com a baseline, pilot Raspberry Pi pendent. No es reclama validació productiva del POS edge.

## Actualització d'evidència — dues línies diferenciades (2026-11-09)

La web comercial i el mini CRM documentats a `MicroPos-web` són una línia diferent del motor POS edge proposat. No s'han de confondre els seus resultats.

| Línia | Evidència documentada | Encara no demostrat |
|---|---|---|
| Web comercial i mini CRM | Web Astro SSG ES/EN/CA, PHP/SQLite, API v1, pagaments manuals/Bold, outbox/webhooks i proves reals d'integració amb n8n | Auditoria independent de totes les funcions productives, cobraments live generalitzats o disponibilitat sostinguda |
| POS edge/offline-first | Arquitectura, ADR, estratègia ERP i pla de pilot Raspberry Pi | Venda offline real, impressió fiable, persistència i restauració, sincronització sense duplicats, adaptadors ERP i pilot completat |

La web comercial gestiona clients potencials i pagaments comercials; el POS edge previst gestionaria les vendes locals del negoci. El bon funcionament d'un webhook del mini CRM **no** valida la sincronització de vendes del POS edge.

**Escala canònica de maduresa:** web comercial — evidència documental d'implementació i desplegament de la superfície pública (**Deployed**, limitada a la web; sense validació productiva sostinguda). POS edge — **Concept** amb disseny documentat, i pilot encara no executat.

Llegiu [EVIDENCE.ca.md](EVIDENCE.ca.md) per consultar les limitacions. La resta del document descriu l'arquitectura objectiu del POS edge, no un inventari de components en producció.

## Revisió arquitectònica — restriccions, seguretat i qüestions obertes

**Context i restriccions.** Els petits negocis tenen pressupostos limitats, connexió variable i poca capacitat d'administrar hardware. Una web de captació comercial no demostra que existeixi un registre de vendes local resilient.

**Seguretat i privadesa.** El mini CRM tracta dades de contactes comercials i processos associats a pagaments; el POS edge previst tractaria vendes locals i possiblement dades personals. Cada línia necessita permisos delimitats, secrets aïllats, retenció, auditoria i recuperació comprovada. Els controls de la web no validen automàticament els del POS edge.

**Alternatives i compromisos.** Un POS només cloud exigeix connectivitat; executar un ERP complet a cada node incrementa el manteniment. Un nucli de transaccions locals amb adaptadors ERP podria donar continuïtat, però afegeix conflictes de sincronització, desgast del disc, conciliació i suport. Cal validar-ho al pilot.

**Lliurament i preguntes pendents.** Per acceptar el pilot fan falta versions de hardware/software, proves de venda offline i impressió, reinici, restauració real, idempotència, conciliació de cues, observacions d'usuaris i registre de fallades. El diagrama i el catàleg de scripts no són evidència d'execució.

## Mapa de conformitat amb l'estàndard de publicació

Els 14 temes obligatoris s'expliquen en aquest document i en els annexos vinculats:

| Tema | Ubicació |
|---|---|
| Context; problema; restriccions; drivers | Resum, Problema i [Arquitectura](ARCHITECTURE.ca.md) |
| Límits del sistema i arquitectura | Arquitectura resumida, Decisió ERP i [Arquitectura](ARCHITECTURE.ca.md) |
| Decisions; alternatives; compromisos | Decisió ERP, [Decisions](DECISIONS.ca.md), [Estratègia ERP](ERP_STRATEGY.ca.md) |
| Seguretat i privadesa | [Arquitectura](ARCHITECTURE.ca.md), [Evidència](EVIDENCE.ca.md) i revisió específica pendent |
| Lliurament i operacions | Pilot, Scripts i [Pla pilot](PILOT_PLAN.ca.md) |
| Nivell d'evidència | Actualització de les dues línies i [Registre](EVIDENCE.ca.md) |
| Lliçons i qüestions pendents | Distinció entre CRM web i sincronització edge; proves del [Pla pilot](PILOT_PLAN.ca.md) |

**Nivell canònic per línia:** web comercial **Deployed** segons la publicació documentada, sense validació productiva sostinguda; POS edge **Concept**, disseny publicat i pilot no executat. Aquesta revisió no és una auditoria independent de l'entorn en viu.

## Resum executiu

MicroPOS és una arquitectura POS lleugera per a petits negocis i entorns de baixa connectivitat. La hipòtesi central és que un negoci ha de poder vendre, imprimir, tancar caixa, preservar dades locals i recuperar-se de la pèrdua de connectivitat sense dependre d’una connexió contínua al núvol.

L’arquitectura proposada utilitza una Raspberry Pi com a node edge opcional per al pilot, persistència operacional local, sincronització mitjançant outbox, scripts per a provisió i recuperació, i adapters per a Odoo i Dolibarr en lloc d’acoblar el core POS a un únic ERP.

**Nivell d’evidència:** baseline arquitectònic + pilot de hardware planificat. Offline, sincronització, impressió, recuperació i adapters ERP requereixen implementació i validació de camp.

## Problema

MicroPOS ha de suportar:

- vendes locals sense Internet;
- impressió i operació de caixa;
- recuperació després de reinici o tall elèctric;
- sincronització eventual;
- prevenció de duplicats;
- backup i restore;
- diagnòstic remot simple;
- integració ERP opcional segons la maduresa del negoci.

## Arquitectura resumida

```text
Dispositius del negoci
        │
        ▼
┌─────────────────────────┐
│ Raspberry Pi Edge Node  │
│ MicroPOS local          │
│ Base operacional local  │
│ Transactional outbox    │
│ Sync worker             │
│ Print service           │
│ Backup agent            │
│ Health diagnostics      │
└────────────┬────────────┘
             │
       Internet intermitent
             │
             ▼
┌─────────────────────────┐
│ Serveis Cloud DCP       │
│ Sync API                │
│ n8n                     │
│ Monitoring              │
│ Backups                 │
│ Integracions            │
└────────────┬────────────┘
             │
       ┌─────┴─────┐
       ▼           ▼
      Odoo      Dolibarr
```

## Decisió ERP

MicroPOS es manté independent:

```text
MicroPOS Core
      │
      ├── Adapter Odoo
      ├── Adapter Dolibarr
      ├── CSV Import / Export
      └── API / Webhooks
```

Odoo i Dolibarr són destins d’integració, no el motor transaccional del node edge.

## Pilot Raspberry Pi

### Fase A — baseline del node

- Raspberry Pi OS Lite;
- empaquetat reproduïble;
- MicroPOS;
- base local;
- impressió;
- health checks;
- backups;
- arrencada automàtica.

### Fase B — escenaris d’operació

- venda normal;
- venda offline;
- obertura i tancament de caixa;
- impressió;
- reinici inesperat;
- pèrdua i retorn d’Internet;
- backlog de sincronització;
- duplicats;
- conflicte d’estoc;
- backup i restore real.

### Fase C — sincronització

```text
Transacció local
       ↓
Commit local
       ↓
Outbox event
       ↓
Sync worker
       ↓
Cloud API
       ↓
Processament idempotent
       ↓
ACK
       ↓
Marcar sincronitzat
```

## Scripts operatius

```text
scripts/
├── install/
├── ops/
├── backup/
├── sync/
└── integrations/
    ├── odoo/
    └── dolibarr/
```

## Abast MVP del pilot

- vendes;
- caixa;
- inventari mínim;
- clients bàsics;
- offline;
- backup/restore;
- sincronització;
- diagnòstic;
- auditoria mínima.

## Direcció de producte

```text
MicroPOS Start
software + configuració + catàleg inicial + formació + suport

MicroPOS Edge
Raspberry Pi + operació local + backup + impressió + monitoratge + suport remot

MicroPOS Business
MicroPOS + ERP + automatització + dashboards + CRM/integracions
```

## Documents relacionats

- [`ARCHITECTURE.ca.md`](ARCHITECTURE.ca.md)
- [`DECISIONS.ca.md`](DECISIONS.ca.md)
- [`PILOT_PLAN.ca.md`](PILOT_PLAN.ca.md)
- [`ERP_STRATEGY.ca.md`](ERP_STRATEGY.ca.md)
- [`SCRIPTS_CATALOG.ca.md`](SCRIPTS_CATALOG.ca.md)
- [`EVIDENCE.ca.md`](EVIDENCE.ca.md)

---

MicroPOS es documenta com una arquitectura edge/offline-first i programa pilot, no com una plataforma POS validada en producció.
