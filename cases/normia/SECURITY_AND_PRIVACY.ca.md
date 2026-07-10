# Normia — Seguretat i Privacitat

## Abast

Aquest document resumeix principis públics i sanititzats de seguretat i privacitat de l’arquitectura base de Normia. No representa validació productiva.

## Identitat i autorització

Normia distingeix rols operatius com Operator, Supervisor, Admin i Auditor/Verifier.

Principis:

- permisos diferents per rol;
- l’operador no verifica la seva pròpia acció crítica;
- el supervisor revisa desviacions i evidències correctives;
- l’auditor/verificador pot consultar integritat sense modificar l’operació;
- les accions sensibles generen evidència d’auditoria quan correspon.

## Fitxers sensibles

Certificats, registres mèdics i documents personals han de viure en storage privat.

```text
Request
  ↓
Autenticació
  ↓
Política d’autorització
  ↓
Validació de sensibilitat
  ↓
Accés temporal o stream controlat
  ↓
Auditoria quan correspongui
```

No s’han d’utilitzar URLs públiques permanents per a documents sensibles.

## Minimització de dades

- cap dada personal o sensible on-chain;
- blockchain emmagatzema compromisos criptogràfics agregats;
- els registres operatius continuen off-chain;
- els canals externs reben només el context mínim necessari.

## Integritat històrica

Els registres crítics tancats no s’eliminen ni se sobreescriuen silenciosament.

```text
Registre original
      ↓
Correcció supersessora
      ↓
Estat efectiu actual
```

L’original continua sent reconstruïble.

## Seguretat dels canals

Web, QR i Telegram són canals d’accés, no dominis separats.

Tots han de reutilitzar:

- context d’identitat;
- polítiques d’autorització;
- serveis d’aplicació;
- validació de domini;
- regles de generació d’auditoria.

Un QR aporta context, no autorització per si mateix.

## Seguretat de l’automatització

n8n no governa estats de negoci.

Els endpoints d’aplicació han de gestionar:

- autenticació de la crida;
- idempotència;
- validació;
- invocació del servei de negoci;
- resultat auditable.

## Límit de seguretat blockchain

Riscos rellevants:

- custòdia de la clau del signer;
- nonce;
- enviament duplicat;
- fallada RPC;
- transacció revertida;
- confusió entre `tx_hash` i finality.

Regles:

- `tx_hash` no és confirmació;
- no embolcallar RPC extern dins de transaccions MySQL llargues;
- dispatch idempotent;
- protecció anti-duplicat a aplicació i contracte;
- l’operació continua si l’anchor falla.

## Límit de divulgació pública

No es publiquen:

- claus privades;
- credencials de wallet;
- secrets RPC;
- documents mèdics o personals;
- documents confidencials del pilot;
- endpoints privats;
- codi font privat;
- dades reals d’usuaris.
