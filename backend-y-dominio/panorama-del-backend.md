---
description: Cómo se reparte el dominio entre microservicios.
icon: server
---

# Panorama del backend

## Vista general

El backend divide la atención médica por dominios. Cada microservicio concentra una responsabilidad principal.

### Módulos clínicos

* `msvc-paciente`: pacientes, historial y estado de citas.
* `msvc-medico`: médicos, especialidades y operaciones asociadas.
* `msvc-cita`: agenda clínica y coordinación operativa.
* `msvc-diagnostico`: diagnósticos vinculados a cita y paciente.

### Cómo se repiten los módulos

Cada servicio sigue una estructura por capas:

* `Controller`: expone endpoints.
* `Service`: aplica reglas de negocio.
* `Repository`: persiste datos.
* `ClientRest`: consume otros microservicios cuando hace falta.

### Integración transversal

* La composición de datos usa OpenFeign.
* `msvc-cita` es el servicio con más dependencias.
* `msvc-diagnostico` y `msvc-cita` sincronizan eventos hacia la capa semántica.

### Persistencia por dominio

* `msvc-medico`: MySQL.
* `msvc-cita`: MySQL.
* `msvc-paciente`: PostgreSQL.
* `msvc-diagnostico`: PostgreSQL.

### Stack repetido en backend

* Spring Boot `3.5.9`
* Spring Cloud OpenFeign `2025.0.1`
* Java `25`

### Qué revisar primero según tu rol

#### Si vienes del negocio

* Empieza por `msvc-cita`.
* Luego revisa pacientes, médicos y diagnósticos.

#### Si vienes de infraestructura o integración

* Empieza por integración entre microservicios.
* Luego revisa la capa semántica.
