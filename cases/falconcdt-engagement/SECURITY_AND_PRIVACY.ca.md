# FalconCDT Engagement Platform — Seguretat i Privacitat

## Abast

Aquest document resumeix principis públics i sanititzats de seguretat i privacitat. No exposa infraestructura privada, credencials, endpoints interns ni configuracions confidencials de clients.

## 1. Autenticació i autorització

L’aplicació separa les responsabilitats de participants i administradors.

Principis:

- sessions autenticades per a àrees protegides;
- rutes administratives protegides per rols;
- rutes de participant sense privilegis administratius;
- estat del compte amb impacte sobre l’accés;
- accions privilegiades auditables.

## 2. Gestió de secrets

El repositori no ha de contenir:

- fitxers `.env`;
- credencials SMTP;
- tokens de Telegram;
- secrets d’automatització;
- API keys;
- backups privats;
- logs de producció;
- fitxers pujats pels usuaris.

Els secrets es mantenen fora del control de versions.

## 3. Hardening de la capa web

El model de desplegament incorpora regles per:

- bloquejar l’accés directe a rutes privades;
- impedir l’execució de scripts als directoris d’uploads;
- bloquejar extensions sensibles i fitxers de metadades;
- reduir l’exposició accidental de configuració i documentació operativa.

## 4. Protecció d’endpoints d’automatització

Els workflows externs utilitzen endpoints protegits en lloc d’accés directe a la base de dades productiva.

Controls:

- secret compartit d’automatització;
- restricció opcional per IP;
- autorització a la capa d’aplicació;
- credencials de base de dades fora de n8n.

## 5. Logging i redacció

Els logs no s’han de convertir en un magatzem secundari de secrets.

Principis:

- redacció de valors sensibles coneguts;
- evitar dumps de credencials;
- separar debugging de logs segurs per producció;
- mantenir el debug de producció desactivat.

## 6. Privacitat dels participants

```text
Rànquing públic
        ≠
Historial detallat públic de pronòstics
```

Un participant pot aparèixer a la classificació agregada sense exposar automàticament el seu comportament detallat.

## 7. Proveïdors externs

Les APIs externes són límits de confiança.

- claus fora del repositori;
- payloads normalitzats abans de l’ús de domini;
- proveïdors secundaris sense capacitat de sobreescriure la veritat oficial de scoring;
- degradació segura quan falla una integració opcional.

## 8. Uploads i contingut

- bloqueig d’execució als uploads;
- separació entre codi i fitxers generats o pujats;
- sanitització allowlist per a contingut HTML enriquit.

## 9. Riscos operatius

- drift entre configuració SQL local i hosting;
- patches no aplicats;
- diferències de timezone;
- errors de credencials de notificació;
- caigudes de proveïdors externs;
- fallades en el processament de cues;
- activació accidental del debug en producció.

Aquests riscos es gestionen amb checkpoints de release, checklists, validació per ambient i procediments de rollback.

## 10. Límit de divulgació pública

Aquest cas no publica:

- credencials productives;
- endpoints privats;
- rutes internes de servidor;
- detalls d’esquema innecessaris;
- configuracions privades de clients;
- logs de producció;
- dades personals de participants.
