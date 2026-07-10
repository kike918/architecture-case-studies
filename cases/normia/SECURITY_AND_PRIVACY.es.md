# Normia — Seguridad y Privacidad

## Alcance

Este documento resume principios públicos y sanitizados de seguridad y privacidad de la arquitectura base de Normia. No representa validación productiva.

## Identidad y autorización

Normia distingue roles operativos como Operator, Supervisor, Admin y Auditor/Verifier.

Principios:

- permisos distintos por rol;
- el operador no verifica su propia acción crítica;
- el supervisor revisa desviaciones y evidencias correctivas;
- el auditor/verificador puede consultar integridad sin modificar la operación;
- acciones sensibles generan evidencia de auditoría cuando corresponde.

## Archivos sensibles

Certificados, registros médicos y documentos personales deben vivir en storage privado.

```text
Request
  ↓
Autenticación
  ↓
Política de autorización
  ↓
Validación de sensibilidad
  ↓
Acceso temporal o stream controlado
  ↓
Auditoría cuando aplique
```

No se deben usar URLs públicas permanentes para documentos sensibles.

## Minimización de datos

- ningún dato personal o sensible on-chain;
- blockchain almacena compromisos criptográficos agregados;
- registros operativos permanecen off-chain;
- canales externos reciben solo el contexto mínimo necesario.

## Integridad histórica

Los registros críticos cerrados no se eliminan ni sobrescriben silenciosamente.

```text
Registro original
      ↓
Corrección supersesora
      ↓
Estado efectivo actual
```

El original permanece reconstruible.

## Seguridad de canales

Web, QR y Telegram son canales de acceso, no dominios separados.

Todos deben reutilizar:

- contexto de identidad;
- políticas de autorización;
- servicios de aplicación;
- validación de dominio;
- reglas de generación de auditoría.

Un QR aporta contexto, no autorización por sí mismo.

## Seguridad de automatización

n8n no gobierna estados de negocio.

Los endpoints de aplicación deben manejar:

- autenticación de la llamada;
- idempotencia;
- validación;
- invocación del servicio de negocio;
- resultado auditable.

## Límite de seguridad blockchain

Riesgos relevantes:

- custodia de llave del signer;
- nonce;
- envío duplicado;
- fallo RPC;
- transacción revertida;
- confusión entre `tx_hash` y finality.

Reglas:

- `tx_hash` no es confirmación;
- no envolver RPC externos en transacciones MySQL largas;
- dispatch idempotente;
- protección anti-duplicado en aplicación y contrato;
- operación continúa si el anchor falla.

## Límite de divulgación pública

No se publican:

- llaves privadas;
- credenciales de wallet;
- secretos RPC;
- documentos médicos o personales;
- documentos confidenciales del piloto;
- endpoints privados;
- código fuente privado;
- datos reales de usuarios.
