---
description: Diagnósticos clínicos y sincronización hacia el grafo semántico.
icon: notes-medical
---

# msvc-diagnostico

## Responsabilidad

Gestiona diagnósticos clínicos y su relación con citas y pacientes. También sincroniza el diagnóstico hacia la capa semántica.

## Endpoints principales

* `GET /diagnosticos`
* `GET /diagnosticos/{id}`
* `GET /diagnosticos/con-detalle/{id}`
* `GET /diagnosticos/cita/{id}`
* `GET /diagnosticos/paciente/{id}`
* `POST /diagnosticos`
* `PUT /diagnosticos/{id}`
* `DELETE /diagnosticos/{id}`
* `DELETE /diagnosticos/{id}/force`

## Contrato principal de entrada

### `DiagnosticoEntity`

* `descripcion`: obligatoria.
* `tipoDiagnostico`: obligatorio.
* `fechaDiagnostico`: obligatoria.
* `citaId`: obligatorio.
* `pacienteId`: obligatorio.

## Respuesta enriquecida

### `DiagnosticoDetalle`

* `diagnostico`
* `cita`
* `paciente`

## Reglas de negocio

* El borrado es lógico por defecto.
* La creación y actualización sincronizan el diagnóstico en la capa semántica.
* Las referencias de cita y paciente se validan vía servicios remotos cuando aplica.

## Dependencias

### Internas

* `DiagnosticoController`
* `DiagnosticoServiceImpl`
* `DiagnosticoRepository`

### Externas

* `msvc-cita`
* `msvc-paciente`
* `msvc-web-semantica`
* PostgreSQL

## Versión y runtime

* Spring Boot `3.5.9`
* Spring Cloud OpenFeign `2025.0.1`
* Java `25`
* PostgreSQL Driver gestionado por Spring Boot `3.5.9`

## Casos de uso reales

* Registro de diagnóstico posterior a una consulta.
* Consulta de diagnósticos por cita.
* Historial de diagnósticos por paciente.

## Ejemplo

```bash
curl -X POST http://localhost:8082/diagnosticos \
  -H "Content-Type: application/json" \
  -d "{
    \"descripcion\":\"Hipertensión arterial controlada\",
    \"tipoDiagnostico\":\"ENFERMEDAD_CRONICA\",
    \"fechaDiagnostico\":\"2026-03-10T10:30:00.000Z\",
    \"citaId\":1,
    \"pacienteId\":1
  }"
```

{% hint style="warning" %}
Los cambios en la estructura del diagnóstico impactan ontología y consultas SPARQL.
{% endhint %}
