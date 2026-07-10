# FalconCDT Engagement Platform — Registre d’Evidència

## Propòsit

Aquest registre relaciona les afirmacions públiques del cas amb nivells explícits d’evidència. És deliberadament conservador: els elements del roadmap no es presenten com a capacitats completades.

## Escala d’evidència

- **Concepte** — idea documentada o direcció arquitectònica.
- **Prototip** — implementat experimentalment, encara sense ús operatiu.
- **Pilot** — validat en ús real controlat.
- **Desplegat** — present en un desplegament operatiu.
- **Validat en producció** — verificat repetidament en operació productiva amb evidència més forta.

## Matriu de capacitats

| Capacitat | Nivell d’evidència | Base pública segura |
|---|---|---|
| Registre i login | Desplegat | El checkpoint operatiu documenta registre, login, sessions i rols |
| Dashboard i perfil | Desplegat | Dashboard, perfil i preferències documentats |
| Captura de pronòstics | Desplegat | Flux operatiu documentat |
| Validació de deadlines | Desplegat | Validació backend i bloqueig automàtic documentats |
| Scoring per fase | Desplegat | Scoring i rànquing per fase operatius |
| Rànquings independents per fase | Desplegat | Separació de fases documentada |
| Rànquing públic amb historial privat | Desplegat | Separació documentada |
| Gestió admin de participants | Desplegat | Operacions CRUD i estats documentats |
| Administració de pagaments/registre | Desplegat | Operacions administratives documentades |
| Administració de partits/esdeveniments | Desplegat | CRUD i filtres documentats |
| Auditoria de pronòstics | Desplegat | Vistes globals i per pronòstic documentades |
| Auditoria general | Desplegat | Audit log d’aplicació documentat |
| Tancament de fases | Desplegat / validat en release | Tancament formal i validació documentats |
| Guanyadors i premis | Desplegat / validat en release | Declaració, notificació i premis documentats |
| Email | Desplegat | SMTP provat i processament en cua documentat |
| Telegram | Desplegat | Integració individual/grup i cua documentades |
| Plantilles editables | Desplegat | Templates multicanal documentats |
| Resum diari admin | Desplegat | Email/Telegram amb deduplicació documentats |
| Dashboard d’automatitzacions | Desplegat | Execució manual i visibilitat de runs documentades |
| Endpoints protegits | Desplegat | Protecció per automation secret documentada |
| Sync de resultats oficials | Desplegat | Sincronització externa i normalització a MySQL documentades |
| Detall enriquit opcional | Implementat / dependent de la integració | Integració secundària amb fallback documentada |
| Exportables CSV | Desplegat | Exportables admin documentats |
| Configuració white-label | Baseline desplegat | Branding i configuració comercial documentats |
| Model multi-instància | Desplegat | Aïllament per desplegament documentat |
| Multi-tenancy compartit | No implementat | Exclòs explícitament de l’arquitectura actual |
| Orquestració n8n productiva | Parcial | Endpoints i workflows documentats; desplegament/configuració encara dependents de l’ambient |
| WhatsApp Bridge | Roadmap | Stub preparat; no es presenta com a canal productiu |
| Hardening UX responsive global | Roadmap | Treball pendent explícit |

## Límits d’evidència

Aquest registre públic no exposa:

- codi font privat;
- URLs productives que hagin de romandre privades;
- credencials o tokens;
- dades reals de participants;
- configuracions confidencials de clients;
- secrets d’infraestructura.

## Disciplina d’afirmacions

El cas pot afirmar que la plataforma ha estat desplegada i utilitzada operativament, però no ha d’afirmar escala, ingressos, millora de conversió, creixement d’usuaris o uptime sense evidència validada i autorització per publicar.
