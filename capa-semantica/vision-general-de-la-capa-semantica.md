---
description: Rol de la web semántica dentro del sistema.
icon: brain
---

# Visión general de la capa semántica

## Qué hace esta capa

Convierte datos clínicos transaccionales en conocimiento semántico. Con eso habilita consultas avanzadas por SPARQL y por lenguaje natural.

### Aportes concretos

* Define un vocabulario formal del dominio médico.
* Representa entidades como tripletas RDF.
* Aplica restricciones OWL.
* Ejecuta consultas declarativas sobre relaciones clínicas.
* Expone una interfaz amigable para usuarios no expertos.

### Endpoints principales

* `GET /api/v1/semantic/buscar?texto=...`
* `POST /api/v1/semantic/sync`
* `POST /api/v1/semantic/sync/diagnostico`
* `POST /api/v1/semantic/bulk-load`
* `POST /api/v1/semantic/sparql`

### Dependencias internas

* `SemanticController`
* `SemanticServiceImpl`
* `BulkSyncService`
* `FusekiRepository`
* `QueryParser`
* `SparqlBuilder`

### Dependencias externas

* Apache Jena Fuseki
* `msvc-paciente`
* `msvc-medico`
* `msvc-cita`
* `msvc-diagnostico`

### Stack relevante

* Spring Boot `3.5.9`
* Spring Cloud OpenFeign `2025.0.1`
* Java `25`
* Jena `5.3.0`
* Lucene `9.9.1`
* OWL API `5.1.20`

## Casos de uso reales

* Preguntar por disponibilidad médica.
* Ver ranking de médicos con más citas.
* Filtrar citas por especialidad, estado, DNI o rango temporal.

{% hint style="info" %}
Esta capa depende del estado de Fuseki y de que el grafo esté alineado con los datos operativos.
{% endhint %}
