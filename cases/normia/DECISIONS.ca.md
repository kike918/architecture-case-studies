# Normia — Decisions d’Arquitectura

## ADR-001 — Monòlit modular per a l’MVP

**Decisió:** utilitzar un monòlit modular en Laravel abans de considerar microserveis.

**Per què:** el producte encara valida els límits del domini mitjançant un pilot real. Una arquitectura distribuïda afegiria costos de desplegament, observabilitat i consistència abans d’estabilitzar el domini.

**Trade-offs:** la disciplina modular s’ha de mantenir dins d’un únic codebase.

---

## ADR-002 — Single-tenant per instal·lació

**Decisió:** una instal·lació aïllada per client durant l’MVP.

**Per què:** límits de privacitat més simples, menys complexitat i ownership operatiu més clar.

**Trade-offs:** treball duplicat de desplegament i upgrades.

---

## ADR-003 — MySQL com a font de veritat operacional

**Decisió:** tasques, controls, desviacions, accions correctives i semàntica d’auditoria viuen a la base de dades de l’aplicació.

**Per què:** l’operació diària ha de continuar encara que Telegram, n8n o blockchain no estiguin disponibles.

---

## ADR-004 — Laravel governa les regles; els canals comparteixen serveis

**Decisió:** web, QR, Telegram Bot i Mini App invoquen serveis comuns d’aplicació.

**Per què:** una única implementació de permisos, conformitat, transicions d’estat i esdeveniments d’auditoria.

---

## ADR-005 — n8n orquestra però no governa estats de domini

**Decisió:** n8n executa horaris, reintents i notificacions; Laravel manté les decisions de negoci.

**Per què:** les invariants han de romandre centralitzades i testables.

---

## ADR-006 — Auditar localment abans d’ancorar externament

**Decisió:** crear esdeveniments semàntics i un ledger local abans de Merkle batches i Polygon.

**Per què:** blockchain reforça integritat, però no substitueix context ni persistència operacional.

---

## ADR-007 — Polygon fora del camí crític

**Decisió:** l’operació sanitària continua encara que l’ancoratge es retardi o falli.

**Per què:** una operació física no pot dependre de RPC, gas, nonce o finality.

---

## ADR-008 — Sense dades personals o sensibles on-chain

**Decisió:** ancorar només compromisos criptogràfics agregats i metadades mínimes.

**Per què:** privacitat, minimització de dades i control del cicle de vida.

---

## ADR-009 — Correcció per supersessió

**Decisió:** els registres crítics tancats no se sobreescriuen ni s’eliminen silenciosament. Les correccions conserven l’original.

**Per què:** auditabilitat i reconstrucció històrica.

---

## ADR-010 — Validar el Golden Flow abans de l’expansió horitzontal

**Decisió:** prioritzar un vertical slice complet des de la tasca fins a desviació, contenció, acció correctiva, verificació i auditoria.

**Per què:** mòduls CRUD aïllats no demostren el model de producte.
