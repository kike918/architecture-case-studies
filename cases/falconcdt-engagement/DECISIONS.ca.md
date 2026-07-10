# FalconCDT Engagement Platform — Decisions d’Arquitectura

## ADR-001 — Multi-instància abans que multi-tenancy

**Context:** el producte havia de suportar diferents desplegaments B2B amb branding, participants, premis, regles i calendaris diferents.

**Decisió:** utilitzar instàncies white-label independents en lloc d’una base compartida multi-tenant.

**Raons:** més aïllament, menys complexitat inicial, canvis específics per client més segurs i rollback més clar.

**Trade-offs:** desplegaments duplicats, més coordinació de patches i risc de drift de configuració.

**Condició de reversió:** reconsiderar quan el nombre de clients i el cost de manteniment superin el cost d’introduir un control plane compartit i aïllament tenant.

---

## ADR-002 — MySQL com a font runtime de veritat

**Context:** els proveïdors externs lliuren resultats, però scoring i rànquing requereixen comportament determinista i auditable.

**Decisió:** normalitzar dades externes a MySQL abans d’utilitzar-les per scoring i rànquing.

**Raons:** determinisme, auditoria, menys acoblament amb APIs i consistència del frontend.

**Trade-offs:** dependència de sincronització, possibilitat de dades obsoletes i necessitat de reconciliació.

---

## ADR-003 — Un proveïdor oficial i proveïdors secundaris d’enriquiment

**Decisió:** un únic proveïdor decideix marcador i estat oficial; altres només afegeixen informació opcional.

**Raó principal:** dos proveïdors no han de competir pel mateix fet de negoci quan aquest fet modifica scoring i rànquing.

**Trade-offs:** dependència del proveïdor oficial i possibles fallades parcials en l’enriquiment.

---

## ADR-004 — Arquitectura lleugera per capes sense framework pesat

**Decisió:** PHP 8.2+, PDO, MySQL i límits explícits entre Controllers, Services, Repositories, Providers i Views.

**Raons:** baix overhead, compatibilitat amb hosting pràctic, control directe i evolució incremental.

**Trade-offs:** més convencions internes i disciplina arquitectònica manual.

---

## ADR-005 — L’aplicació governa el domini; n8n orquestra

**Decisió:** n8n invoca endpoints HTTP protegits, però scoring, rànquing i transicions de fase continuen dins de l’aplicació.

**Raons:** mantenir invariants de domini en un sol lloc, preservar testabilitat i evitar duplicar lògica de negoci en workflows.

**Trade-offs:** encara calen endpoints segurs, idempotència i monitoratge dels workflows.

---

## ADR-006 — Cues de notificació per canal

**Decisió:** generar treball de notificació per canal mitjançant plantilles i cues, amb processament manual com a fallback operatiu.

**Raons:** separar generació i lliurament, permetre comportament específic per canal i habilitar reintents i deduplicació.

**Trade-offs:** monitoratge addicional i lliurament eventualment asíncron.

---

## ADR-007 — Rànquing públic sense historial públic de pronòstics

**Decisió:** mostrar resultats agregats en rànquings sense publicar automàticament l’historial detallat de cada participant.

**Raons:** engagement, privacitat i reducció de còpia estratègica durant la competició.

**Trade-offs:** algunes funcionalitats socials queden intencionadament limitades.
