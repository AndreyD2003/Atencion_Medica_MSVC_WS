---
description: Qué revisar cuando tocas contratos, enums, ontología o flujos.
icon: hammer
---

# Impacto de cambios por tipo de modificación

## Si cambias un endpoint

Revisa:

* clientes Feign,
* servicios frontend,
* documentación del módulo,
* consumidores directos.

## Si cambias un enum clínico

Revisa:

* formularios del frontend,
* validaciones backend,
* parser semántico,
* filtros y sugerencias,
* ontología y consultas.

### Casos especialmente sensibles

* especialidad,
* estado de cita,
* tipo de diagnóstico.

## Si cambias la estructura de cita

Revisa:

* `msvc-cita`,
* integración con paciente y médico,
* detalle enriquecido,
* sincronización con `msvc-web-semantica`,
* consultas semánticas asociadas.

## Si cambias la estructura de diagnóstico

Revisa:

* `msvc-diagnostico`,
* sincronización del diagnóstico,
* ontología,
* consultas SPARQL.

## Si cambias la ontología

Revisa:

* `QueryParser`,
* `SparqlBuilder`,
* vocabulario usado en consultas,
* necesidad de `bulk-load`,
* documentación de la capa semántica.

## Si cargas o restauras datos históricos

Revisa:

* coherencia entre bases transaccionales,
* estado del grafo,
* ejecución de `bulk-load`.

## Si cambias configuración local

Revisa:

* proxy de Vite,
* URLs de Feign,
* diferencias entre desarrollo y otros ambientes.

## Regla práctica

Cuanto más cerca esté el cambio de `cita`, `diagnóstico` o la ontología, mayor es el impacto transversal.
