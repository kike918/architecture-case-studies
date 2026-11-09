# MicroPOS — Registre d’Evidència

## Propòsit

Separar decisions arquitectòniques d’evidència de laboratori, pilot i futures afirmacions de producte.

## Escala

- **Baseline documentat** — direcció aprovada per a implementació.
- **Laboratori planificat** — validació hardware/software definida però no executada.
- **Prototip** — implementació experimental.
- **Pilot pendent** — requereix ús real.
- **Pilot validat** — ús controlat completat.
- **Validat en producció** — no reclamat actualment.

## Matriu

| Capacitat | Nivell |
|---|---|
| Arquitectura edge/offline-first | Baseline documentat |
| Node Raspberry Pi | Laboratori planificat |
| Venda local | Abast MVP del pilot |
| Persistència local | Baseline documentat |
| Transactional outbox | Baseline documentat |
| Sync idempotent | Baseline documentat |
| Impressió | Laboratori/pilot pendent |
| Caixa | Abast MVP |
| Inventari mínim | Abast MVP |
| Scripts de backup | Implementació planificada |
| Scripts de diagnòstic | Implementació planificada |
| Adapter Dolibarr | Prototip planificat |
| Adapter Odoo | Prototip planificat |
| n8n | Rol arquitectònic definit |
| Pilot negoci simple | Planificat |
| Pilot operació complexa | Fase posterior |
| Validació productiva | No reclamada |

## Evidència requerida

Abans d’afirmar maduresa s’ha de demostrar venda sense Internet, commit local durable, recuperació després de reinici, sincronització sense duplicats, backlog visible, backup i restore exitosos, impressió estable, diagnòstic útil i reconciliació ERP explícita.

## Reconciliació de la web comercial i el POS edge — 2026-11-09

Aquesta matriu anterior descriu el **POS edge planificat**. Cal valorar per separat les capacitats de la web comercial:

| Capacitat | Font consultada (només lectura) | Evidència / límits |
|---|---|---|
| Web comercial multilingüe | `MicroPos-web@dev/README.md`, `ROADMAP.md` | Astro SSG ES/EN/CA documentat i superfície comercial publicada; no és una prova de totes les pàgines en viu |
| Mini CRM i API | Mateixes fonts | PHP/SQLite, contactes comercials, activitats i API v1 documentats |
| Pagaments | Mateixes fonts | Fluxos manuals/parcials i Bold documentats; proves de Bold no demostren tots els cobraments reals |
| Outbox i integració n8n | Mateixes fonts | Proves reals d'API i webhooks amb n8n documentades per al CRM web; no certifiquen la sincronització del POS edge |
| Distribució a Hostinger | `MicroPos-web@dev/HOSTINGER-DEPLOYMENT.md` | Artefactes INSTALL/UPDATE i preservació de dades documentats; generar paquets no prova un desplegament |
| POS Raspberry Pi | Documents de l'arquitectura edge i `PILOT_PLAN.ca.md` | **Concept** / pilot planificat; sense evidència inspeccionada d'execució real |

**Condicions per augmentar maduresa:** verificar el SHA i un smoke públic d'una versió comercial concreta; completar una prova controlada de vendes offline, impressió, reinici, sincronització idempotent, restauració real i conciliació ERP abans d'anomenar el POS edge **Pilot** o **Deployed**.

Aquesta és una revisió documental i no una auditoria de salut productiva en temps real.
## Disciplina d’afirmacions

No s’ha d’afirmar fiabilitat offline productiva, maduresa d’integració ERP ni estabilitat de camp de Raspberry Pi fins que es demostri.
