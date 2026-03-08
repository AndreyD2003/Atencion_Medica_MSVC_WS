---
description: Guía rápida para elegir el tipo de consulta semántica.
icon: code-compare
---

# Cuándo usar búsqueda natural y cuándo SPARQL

## Usa búsqueda natural cuando

* Quieres consultar sin conocer SPARQL.
* Necesitas filtrar por especialidad, estado, DNI o fecha.
* Buscas rankings o disponibilidad dentro de patrones ya soportados.

### Endpoint

* `GET /api/v1/semantic/buscar?texto=...`

### Ejemplos ya documentados

* `citas de cardiologia de hoy`
* `top 5 medicos con mas citas`

## Usa SPARQL cuando

* Necesitas control total sobre la consulta.
* Quieres definir explícitamente el patrón RDF.
* Vas a inspeccionar entidades o propiedades concretas del grafo.

### Endpoint

* `POST /api/v1/semantic/sparql`

### Requisito mínimo

* El body debe incluir `query`.

## Diferencia práctica

### Búsqueda natural

* Más accesible.
* Depende de patrones del parser.
* Tiene menos control fino.

### SPARQL directo

* Más flexible.
* Requiere conocer el modelo semántico.
* Te expone más al costo de consultas abiertas.

## Recomendación operativa

* Empieza por búsqueda natural.
* Usa SPARQL cuando el caso salga del patrón conocido.
* Si el resultado no refleja datos nuevos, revisa primero la sincronización del grafo.
