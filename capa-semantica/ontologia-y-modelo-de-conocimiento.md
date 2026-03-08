---
description: Clases, propiedades y restricciones del dominio médico.
icon: diagram-project
---

# Ontología y modelo de conocimiento

## Fundamento semántico

La ontología `atencion-medica.ttl` define clases, propiedades y restricciones del dominio.

### Clases principales

* `med:Paciente`
* `med:Medico`
* `med:Cita`
* `med:Diagnostico`

### Propiedades de datos

* DNI
* nombres
* especialidad
* fecha de cita
* estado de cita
* descripción diagnóstica

### Propiedades de objeto

* `med:citaAgendadaPara`
* `med:atendidaPor`
* `med:generaDiagnostico`

### Restricciones OWL

Se usan restricciones de cardinalidad calificada. El objetivo es asegurar una relación médico y paciente por cita.

## Cómo se representa la información

La capa semántica trabaja con tripletas RDF.

* sujeto
* predicado
* objeto

## Qué implica esto en el proyecto

* El vocabulario debe mantenerse alineado con los enums transaccionales.
* Los cambios en especialidades, estados o tipos clínicos impactan consultas.
* Las consultas semánticas dependen de nombres y relaciones consistentes.

{% hint style="warning" %}
Si cambias la ontología, también debes revisar el parser y las consultas construidas.
{% endhint %}
