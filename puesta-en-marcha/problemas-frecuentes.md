---
description: Errores esperables al levantar el entorno o consultar la capa semántica.
icon: life-ring
---

# Problemas frecuentes

## El frontend no arranca bien con `npm run dev`

### Qué hacer

1. Ejecuta `npm run build`.
2. Luego vuelve a ejecutar `npm run dev`.

### Cuándo aplica

* Cuando el frontend falla al iniciar en local.

## Fuseki arranca pero la consulta semántica no devuelve lo esperado

### Revisa esto

* Que Fuseki esté activo.
* Que exista el dataset `atencion_medica`.
* Que el dataset sea `Persistent (TDB2)`.
* Que se haya cargado `atencion-medica.ttl`.

## El grafo parece desactualizado

### Síntomas

* La operación clínica funciona.
* La búsqueda semántica no refleja cambios recientes.

### Qué hacer

* Ejecuta `POST /api/v1/semantic/bulk-load`.

### Cuándo conviene hacerlo

* Tras cambios de datos históricos.
* Tras restauraciones.
* Si falló la sincronización incremental.

## Se crea una cita pero falla la parte semántica

### Posible causa

* Falla de conectividad con `msvc-web-semantica`.

### Qué revisar

* Estado del servicio semántico.
* Estado de Fuseki.
* Endpoints de integración alineados.

## Consultas SPARQL fallan por entrada inválida

### Revisa esto

* El body debe incluir `query`.
* Si falta `query`, la respuesta esperada es `400`.

## El historial o estado de citas no responde desde paciente

### Posible causa

* Dependencia no disponible en `msvc-cita`.

### Qué revisar

* Disponibilidad del servicio de citas.
* Conectividad entre servicios.

## En desarrollo los datos se comportan raro tras reinicios

### Punto importante

`msvc-paciente` usa `ddl-auto=create-drop` en desarrollo.

### Implicación

* No es una configuración de producción.
* Los datos locales pueden no persistir como esperas.

{% hint style="warning" %}
Si el problema mezcla operación clínica y búsqueda semántica, revisa primero el flujo transaccional. Luego valida la sincronización hacia Fuseki.
{% endhint %}
