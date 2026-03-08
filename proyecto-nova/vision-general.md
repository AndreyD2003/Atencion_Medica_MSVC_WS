---
description: Qué resuelve el proyecto y cómo se divide.
icon: compass
---

# Visión general

## NOVA en una vista

NOVA separa la atención médica por dominios. También añade una capa semántica sobre los datos operativos.

### Qué compone el sistema

* `msvc-paciente`: gestiona pacientes, historial y estado de citas.
* `msvc-medico`: gestiona médicos, especialidades y operaciones clínicas relacionadas.
* `msvc-cita`: orquesta la agenda clínica.
* `msvc-diagnostico`: gestiona diagnósticos ligados a cita y paciente.
* `msvc-web-semantica`: transforma datos clínicos en conocimiento consultable.
* `nova-frontend`: expone la operación clínica y la consulta semántica.

### Qué hace distinta a la solución

* Separa el modelo transaccional del modelo de conocimiento.
* Usa integración síncrona entre microservicios.
* Mezcla persistencia relacional y grafo semántico.
* Permite consultas por SPARQL y por lenguaje natural.

### Cómo leer esta documentación

#### Si quieres entender el proyecto rápido

1. Empieza por arquitectura.
2. Sigue con los flujos principales.
3. Revisa backend, capa semántica y frontend.

#### Si vas a desarrollar

1. Revisa puesta en marcha.
2. Consulta estructura del repositorio.
3. Entra a los módulos que vayas a tocar.
4. Cierra con contribución y estándares.

### Qué problema resuelve cada capa

* La capa transaccional registra pacientes, médicos, citas y diagnósticos.
* La capa semántica reorganiza esos datos para consultas más expresivas.
* El frontend concentra la operación diaria y el acceso a búsqueda semántica.

### Decisiones clave

* La capa semántica complementa al backend transaccional.
* La sincronización puede ser incremental o masiva.
* El frontend usa proxy de desarrollo para desacoplar puertos internos.
