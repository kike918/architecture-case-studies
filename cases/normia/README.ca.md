# Normia

🌐 **Idiomes:** [English](README.md) · [Español](README.es.md) · Català

**Estat:** Cas d’arquitectura i implementació en progrés. Sprint 0, bootstrap tècnic i discovery del pilot estan en curs.

## Resum executiu

Normia és un sistema digital de control sanitari, compliment documental, execució operativa i auditoria verificable per a operacions alimentàries.

El producte es dissenya a partir d’un pilot real i no des d’una abstracció SaaS genèrica. El problema central és connectar controls planificats amb evidència d’execució, gestió de desviacions, contenció, accions correctives, verificació del supervisor i integritat històrica.

L’arquitectura actual és un monòlit modular Laravel amb MySQL com a font de veritat operacional, UX web mobile-first, context QR, Telegram com a canal, n8n com a orquestrador i ancoratge agregat opcional d’evidència d’auditoria a Polygon PoS.

**Nivell d’evidència:** baseline d’arquitectura + prototip UX de referència + implementació en curs. No validat en producció.

## Context i problema

Una operació petita ha de poder reconstruir:

```text
PLANIFICAR → PROGRAMAR → ASSIGNAR → EXECUTAR → REGISTRAR → AVALUAR
→ DETECTAR → CONTENIR → CORREGIR → VERIFICAR → CONSULTAR → EXPORTAR → AUDITAR
```

Per a cada control rellevant, Normia ha de respondre què s’havia de fer, qui, quan, quin resultat hi va haver, si va existir una desviació, quina contenció i correcció es van aplicar, qui va verificar i si l’evidència conserva integritat històrica.

Una aplicació de CRUDs i checklists aïllats no satisfà aquesta definició.

## Drivers arquitectònics

- claredat operativa;
- traçabilitat;
- auditabilitat;
- privacitat;
- mantenibilitat;
- usabilitat mòbil;
- estats de domini explícits;
- resiliència davant fallades externes;
- integritat de l’evidència;
- evolució conscient dels costos.

## Arquitectura resumida

```text
Usuaris
  │
  ├── Web / Mòbil
  ├── Context QR
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
       privat           │
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

## Golden Flow prioritari

```text
LOGIN → AVUI → TASCA → EQUIP/QR → TEMPERATURA → AVALUACIÓ

COMPLEIX → COMPLETAR → AUDIT EVENT

NO COMPLEIX → DESVIACIÓ → CONTENCIÓ → ACCIÓ CORRECTIVA
→ EVIDÈNCIA → VERIFICACIÓ DEL SUPERVISOR → TANCAMENT → AUDIT EVENTS
```

El flux no es considera validat amb pantalles o CRUDs aïllats.

## Decisions clau

- monòlit modular abans que microserveis;
- single-tenant per instal·lació per a l’MVP;
- MySQL com a font de veritat operacional;
- Laravel governa regles i estats;
- Web, QR i Telegram comparteixen serveis d’aplicació;
- n8n orquestra però no governa el domini;
- audit ledger local abans de blockchain;
- Polygon fora del camí crític;
- cap dada personal o sensible on-chain;
- correccions per supersessió, no sobreescriptura silenciosa.

## Desenvolupament assistit per IA

```text
Kike + Codex
backend · domini · persistència · autorització · tests · audit · Polygon

Paull + Antigravity
UX · mobile-first · Livewire/Blade/Filament · browser E2E · QA

Branches separades → PR → cross-review → develop → UAT → main
```

La IA no aprova producció ni substitueix la revisió humana.

## Evidència actual

| Capacitat | Nivell |
|---|---|
| Definició de producte | Baseline documentat |
| Arquitectura MVP | Baseline congelat |
| Golden Flow | Definit, implementació pendent |
| Prototip UX | Referència no productiva |
| Discovery del pilot | En curs |
| Monòlit modular | Baseline / bootstrap en curs |
| Flux tasca-temperatura-desviació | Vertical slice planificat |
| CAPA i verificació | Model de domini definit |
| Audit ledger | Arquitectura definida, implementació pendent |
| Merkle batching | Fase posterior |
| Ancoratge Polygon | Fase posterior |
| Validació productiva | No reclamada |

## Aprenentatges inicials

- un checklist no és el domini;
- execució i conformitat són conceptes diferents;
- contenció i acció correctiva no són equivalents;
- blockchain no demostra veritat física;
- els canals no han de duplicar regles;
- l’excepció importa tant com el check verd;
- el pilot real ha de guiar la generalització.

## Documents relacionats

- [`ARCHITECTURE.ca.md`](ARCHITECTURE.ca.md)
- [`DECISIONS.ca.md`](DECISIONS.ca.md)
- [`SECURITY_AND_PRIVACY.ca.md`](SECURITY_AND_PRIVACY.ca.md)
- [`EVIDENCE.ca.md`](EVIDENCE.ca.md)

---

Aquest cas distingeix explícitament arquitectura documentada, prototips de referència, implementació en curs i validació futura. Normia no es presenta com a validat en producció.
