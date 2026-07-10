# FalconCDT Engagement Platform — Arquitectura

## Propòsit

Descriure l’arquitectura pública i sanititzada de FalconCDT Engagement Platform sense exposar detalls privats d’implementació ni informació confidencial de clients.

## Estil arquitectònic

El producte actual utilitza una arquitectura lleugera per capes en PHP amb MySQL/MariaDB.

```text
Rutes web
    ↓
Controllers
    ↓
Services
    ↓
Repositories / Providers
    ↓
MySQL + integracions externes
```

Responsabilitats:

- els controllers coordinen requests i responses;
- els services contenen les regles de negoci;
- els repositories contenen l’accés SQL;
- els providers aïllen serveis externs;
- les views no executen SQL directament.

## Model de desplegament

El producte utilitza un model white-label multi-instància.

```text
Instància Client A
├── aplicació
├── base de dades
├── branding
├── regles
└── configuració de notificacions

Instància Client B
├── aplicació
├── base de dades
├── branding
├── regles
└── configuració de notificacions
```

No és una arquitectura multi-tenant amb base compartida.

### Per què

El model prioritza:

- aïllament operatiu simple;
- configuració específica per client;
- límits de fallada més clars;
- rollback més fàcil de raonar;
- menor complexitat durant la validació del producte.

El cost és la duplicació del treball de desplegament i actualització.

## Flux principal de dades

```text
Participant
    │
    ▼
UI de pronòstics
    │
    ▼
Validació backend del deadline
    │
    ▼
Persistència del pronòstic
    │
    ├── auditoria
    └── enforcement de bloqueig

Proveïdor oficial de resultats
    │
    ▼
Capa de normalització / sincronització
    │
    ▼
Estat oficial a MySQL
    │
    ▼
Servei de scoring
    │
    ▼
Leaderboard per fase
    │
    ▼
Rànquing públic
```

## Model de fases

```text
Fase
  ├── partits/esdeveniments
  ├── context de scoring
  ├── leaderboard
  ├── guanyador
  └── configuració del premi
```

Les fases permeten períodes de rànquing independents sense eliminar puntuacions històriques.

## Separació de fonts de resultats

```text
Proveïdor oficial
    │
    ├── estat final
    ├── marcador oficial
    ├── trigger de scoring
    └── impacte en rànquing

Proveïdor d’enriquiment
    │
    ├── estat live
    ├── minut
    ├── seu
    ├── àrbitre
    ├── esdeveniments
    ├── estadístiques
    └── alineacions
```

Un proveïdor secundari no pot sobreescriure la veritat oficial de scoring.

## Arquitectura de notificacions

```text
Esdeveniment de domini / acció programada
        ↓
Plantilla de notificació
        ↓
Cua específica per canal
        ↓
Processador
        ├── Email
        ├── Telegram
        └── Canals futurs
```

## Límit d’automatització

n8n es tracta com a orquestrador extern.

```text
Schedule n8n
    ↓
HTTPS request
    ↓
Endpoint protegit
    ↓
Servei d’aplicació
    ↓
Dades de domini + cues de notificació
```

L’aplicació manté la propietat sobre scoring, fases, rànquing, guanyadors, regles de notificació i auditoria.

## Límits de seguretat

```text
Internet
   │
   ▼
Restriccions de capa web
   │
   ├── bloqueig de rutes privades
   ├── bloqueig d’execució a uploads
   └── bloqueig d’extensions sensibles
   │
   ▼
Autenticació / autorització
   │
   ├── rutes admin
   └── rutes participant
   │
   ▼
Capa de serveis
   │
   ▼
Base de dades
```

## Arquitectura operativa

Inclou:

- seqüenciació de patches;
- backups;
- rollback;
- checklist de seguretat;
- validació de desplegament;
- checkpoints de release;
- verificació per ambient.

## Triggers d’evolució

### Multi-tenancy
Quan el nombre de clients i el cost operatiu justifiquin un control plane compartit.

### Cues/workers dedicats
Quan volum, reintents o latència superin el model actual.

### Desplegament containeritzat
Quan el drift d’ambients o el cost d’actualitzar múltiples instàncies sigui dominant.

### Observabilitat centralitzada
Quan l’escala i els incidents requereixin mètriques, tracing i alertes estructurades.
