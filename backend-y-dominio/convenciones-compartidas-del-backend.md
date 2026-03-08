---
description: Patrones repetidos en los microservicios y cómo leerlos rápido.
icon: layer-group
---

# Convenciones compartidas del backend

## Estructura repetida

Todos los microservicios siguen la misma idea:

* `Controller`: expone HTTP.
* `Service`: aplica reglas de negocio.
* `Repository`: persiste datos.
* `ClientRest`: integra con otros servicios cuando hace falta.

## Reglas que se repiten

### Validación en backend

Aunque el frontend valide, la fuente de verdad está en backend.

### DTOs y entidades

Los DTOs se separan de entidades cuando se necesita componer datos o evitar acoplamiento de API.

### Borrado lógico

* Paciente, médico y diagnóstico documentan borrado lógico por defecto.
* El borrado físico aparece con endpoints `force`.

### Integración síncrona

La composición de datos se hace por OpenFeign.

## Qué debes revisar cuando tocas un módulo

1. Contrato HTTP.
2. Validaciones de entrada.
3. Dependencias Feign.
4. Impacto en frontend.
5. Impacto en capa semántica si cambia el dominio.

## Señales de alto impacto

* Cambios en enums clínicos.
* Cambios en endpoints remotos.
* Cambios en estructuras de cita o diagnóstico.
* Cambios en especialidades o estados.

## Lectura rápida por criticidad

* `msvc-cita`: mayor acoplamiento.
* `msvc-web-semantica`: mayor sensibilidad a consistencia.
* `msvc-paciente` y `msvc-medico`: maestros operativos.
* `msvc-diagnostico`: puente entre consulta clínica y conocimiento semántico.
