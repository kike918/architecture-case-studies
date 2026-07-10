# MicroPOS — Pla Pilot Raspberry Pi

## Objectiu

Validar si una Raspberry Pi pot operar com a node edge estable per a MicroPOS en un entorn de negoci amb connectivitat limitada.

## Fase A — Baseline del node

Instal·lar i validar Raspberry Pi OS Lite, empaquetat reproduïble, MicroPOS, base local, arrencada automàtica, impressió, health checks, backup local i diagnòstic.

Mesurar recuperació després de reboot, RAM, CPU, emmagatzematge, temperatura, reinici de serveis, resposta local i recuperació desatesa.

## Fase B — Escenaris operatius

Executar amb evidència:

1. venda normal;
2. venda sense Internet;
3. obertura de caixa;
4. tancament de caixa;
5. impressió;
6. pèrdua de xarxa durant l’operació;
7. diverses hores offline;
8. reconnexió i sync del backlog;
9. intents duplicats;
10. conflicte d’estoc;
11. reboot inesperat;
12. creació de backup;
13. restore complet en un ambient net.

## Fase C — Sincronització

Validar persistència de l’outbox, retry policy, idempotència, ACK, dead-letter handling, informe de reconciliació i visibilitat dels esdeveniments pendents o fallits.

## Seqüència

```text
Laboratori Raspberry
      ↓
Pilot controlat en negoci simple
      ↓
Revisió d’evidència
      ↓
Pilot en operació més complexa
      ↓
Decisió de productització
```

## Criteris de sortida

El pilot només es considera exitós si les vendes continuen offline, un reinici no perd vendes confirmades, el sync duplicat no duplica transaccions, el backup es pot restaurar, la impressió és estable i el backlog és visible i reconciliable.
