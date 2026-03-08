---
description: Guía rápida para encontrar el módulo correcto antes de modificar código.
icon: wrench
---

# Qué servicio tocar según el cambio

## Si cambias pacientes

Revisa primero:

* [msvc-paciente](msvc-paciente.md)
* [Matriz de dependencias por servicio](matriz-de-dependencias-por-servicio.md)

### Suele impactar

* historial médico,
* historial de citas,
* validaciones de cita,
* sincronización semántica indirecta.

## Si cambias médicos

Revisa primero:

* [msvc-medico](msvc-medico.md)
* [Matriz de dependencias por servicio](matriz-de-dependencias-por-servicio.md)

### Suele impactar

* agenda médica,
* especialidades,
* validaciones de cita,
* consultas semánticas por especialidad.

## Si cambias citas

Revisa primero:

* [msvc-cita](msvc-cita.md)
* [Integración entre microservicios](integracion-entre-microservicios.md)
* [Impacto de cambios por tipo de modificación](../desarrollo/impacto-de-cambios-por-tipo-de-modificacion.md)

### Suele impactar

* disponibilidad,
* solapes,
* detalle enriquecido,
* sincronización semántica.

## Si cambias diagnósticos

Revisa primero:

* [msvc-diagnostico](msvc-diagnostico.md)
* [Impacto de cambios por tipo de modificación](../desarrollo/impacto-de-cambios-por-tipo-de-modificacion.md)

### Suele impactar

* contexto de cita y paciente,
* sincronización del grafo,
* consultas semánticas clínicas.

## Si cambias integración

Revisa primero:

* [Integración entre microservicios](integracion-entre-microservicios.md)
* [Matriz de dependencias por servicio](matriz-de-dependencias-por-servicio.md)

## Si cambias semántica

Revisa primero:

* [Visión general de la capa semántica](../capa-semantica/vision-general-de-la-capa-semantica.md)
* [Sincronización con Fuseki](../capa-semantica/sincronizacion-con-fuseki.md)
* [Checklist de consistencia semántica](../capa-semantica/checklist-de-consistencia-semantica.md)

## Si cambias frontend

Revisa primero:

* [Aplicación web](../frontend/aplicacion-web.md)
* [Pantallas y APIs consumidas](../frontend/pantallas-y-apis-consumidas.md)

{% hint style="info" %}
Si dudas entre varios módulos, empieza por el que posee el dato y luego sigue a sus consumidores directos.
{% endhint %}
