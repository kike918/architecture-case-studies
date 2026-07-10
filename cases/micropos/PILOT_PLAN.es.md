# MicroPOS — Plan Piloto Raspberry Pi

## Objetivo

Validar si una Raspberry Pi puede operar como nodo edge estable para MicroPOS en un entorno de negocio con conectividad limitada.

## Fase A — Baseline del nodo

Instalar y validar:

- Raspberry Pi OS Lite;
- empaquetado reproducible;
- aplicación MicroPOS;
- base local;
- arranque automático;
- servicio de impresión;
- health checks;
- backup local;
- diagnóstico.

Medir:

- recuperación después de reboot;
- RAM y CPU;
- almacenamiento;
- temperatura;
- reinicio de servicios;
- tiempo de respuesta local;
- recuperación desatendida.

## Fase B — Escenarios operativos

Ejecutar con evidencia:

1. venta normal;
2. venta sin Internet;
3. apertura de caja;
4. cierre de caja;
5. impresión;
6. pérdida de red durante operación;
7. varias horas offline;
8. reconexión y sync del backlog;
9. intentos duplicados;
10. conflicto de stock;
11. reboot inesperado;
12. creación de backup;
13. restore completo en ambiente limpio.

## Fase C — Sincronización

Validar persistencia de outbox, retry policy, idempotencia, ACK, dead-letter handling, reporte de reconciliación y visibilidad de eventos pendientes/fallidos.

## Secuencia

```text
Laboratorio Raspberry
      ↓
Piloto controlado en negocio simple
      ↓
Revisión de evidencia
      ↓
Piloto en operación más compleja
      ↓
Decisión de productización
```

## Criterios de salida

El piloto solo se considera exitoso si las ventas continúan offline, un reinicio no pierde ventas confirmadas, el sync duplicado no duplica transacciones, el backup puede restaurarse, la impresión es estable y el backlog es visible y reconciliable.
