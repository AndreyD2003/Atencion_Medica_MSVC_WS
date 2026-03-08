---
description: Agenda clínica, validación de disponibilidad y sincronización semántica.
icon: calendar-days
---

# msvc-cita

## Responsabilidad

Es el núcleo de agenda clínica. Orquesta creación y consulta de citas, valida disponibilidad y sincroniza eventos relevantes hacia la capa semántica.

## Endpoints principales

* `GET /citas`
* `GET /citas/{id}`
* `GET /citas/con-detalle/{id}`
* `GET /citas/paciente/{id}`
* `GET /citas/medico/{id}`
* `POST /citas`
* `PUT /citas/{id}`
* `DELETE /citas/{id}`
* `DELETE /citas/{id}/force`

## Contrato principal de entrada

### `CitaEntity`

* `fechaCita`: obligatoria.
* `horaInicio`: obligatoria.
* `horaFin`: obligatoria.
* `motivo`: obligatorio.
* `estado`: obligatorio.
* `pacienteId`: obligatorio.
* `medicoId`: obligatorio.

## Respuesta enriquecida

### `CitaDetalle`

* `cita`
* `paciente`
* `medico`
* `diagnosticos`

## Reglas de negocio

* Evita solapamiento de horarios por médico y paciente.
* Valida existencia y estado de paciente y médico.
* Normaliza fecha y hora antes de persistir.
* Sincroniza con `msvc-web-semantica` después de guardar o actualizar.

## Dependencias

### Internas

* `CitaController`
* `CitaServiceImpl`
* `CitaRepository`

### Externas

* `msvc-paciente`
* `msvc-medico`
* `msvc-diagnostico`
* `msvc-web-semantica`
* MySQL

## Versión y runtime

* Spring Boot `3.5.9`
* Spring Cloud OpenFeign `2025.0.1`
* Java `25`
* MySQL Connector/J gestionado por Spring Boot `3.5.9`

## Casos de uso reales

* Programación de consulta médica.
* Consulta de una cita con contexto completo.
* Listado de citas por paciente.

## Ejemplo

```bash
curl -X POST http://localhost:8081/citas \
  -H "Content-Type: application/json" \
  -d "{
    \"fechaCita\":\"2026-03-15\",
    \"horaInicio\":\"09:00:00\",
    \"horaFin\":\"09:30:00\",
    \"motivo\":\"Dolor torácico\",
    \"estado\":\"PROGRAMADA\",
    \"pacienteId\":1,
    \"medicoId\":1
  }"
```

{% hint style="warning" %}
Es el punto con más integración. Si falla la sincronización semántica, revisa la conectividad con `msvc-web-semantica`.
{% endhint %}
