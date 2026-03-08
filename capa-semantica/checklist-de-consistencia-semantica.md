---
description: Qué validar para confiar en el grafo y en las consultas.
icon: clipboard-check
---

# Checklist de consistencia semántica

## Antes de confiar en una consulta semántica

Confirma esto:

* Fuseki está activo.
* El dataset `atencion_medica` existe.
* El `.ttl` fue cargado.
* La sincronización incremental no falló.
* El grafo fue reconstruido con `bulk-load` si hubo cambios históricos.

## Si cambió el dominio

### Revisa también

* enums clínicos,
* especialidades,
* estados de cita,
* tipos de diagnóstico,
* ontología,
* parser,
* consultas construidas.

## Si cambió la ontología

Debes revisar:

* `QueryParser`
* `SparqlBuilder`
* impacto en consultas SPARQL
* necesidad de `bulk-load`

## Si una consulta no devuelve resultados esperados

### Orden de revisión recomendado

1. Verifica que el dato exista en la capa transaccional.
2. Verifica que la sincronización haya ocurrido.
3. Verifica estado de Fuseki.
4. Verifica que el patrón consultado esté soportado.

## Si usas SPARQL directo

Confirma esto:

* el body incluye `query`,
* la consulta no es excesivamente abierta,
* el vocabulario usado coincide con la ontología cargada.

{% hint style="info" %}
La calidad de la búsqueda semántica depende menos del frontend y más de la alineación entre datos, sincronización, ontología y parser.
{% endhint %}
