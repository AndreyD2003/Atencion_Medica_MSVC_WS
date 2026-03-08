---
description: Gestión de pacientes, historial y coordinación de citas.
icon: user
---

# msvc-paciente

## Responsabilidad

Gestiona el ciclo de vida de pacientes. También expone operaciones sobre historial médico y coordinación de citas.

## Endpoints principales

* `GET /pacientes`
* `GET /pacientes/{id}`
* `GET /pacientes/{id}/citas`
* `GET /pacientes/{id}/historial-medico`
* `POST /pacientes`
* `PUT /pacientes/{id}`
* `DELETE /pacientes/{id}`
* `DELETE /pacientes/{id}/force`
* `POST /pacientes/agendar-cita`
* `PATCH /pacientes/{pacienteId}/citas/{citaId}/estado`

## Contrato principal de entrada

### `CrearPacienteDto`

* `nombres`: obligatorio.
* `apellidos`: obligatorio.
* `fechaNacimiento`: obligatoria.
* `genero`: obligatorio.
* `dni`: obligatorio, único y con regex de 8 dígitos.
* `telefono`: obligatorio y validado por regex.
* `email`: obligatorio y con formato email.
* `direccion`: obligatoria.
* `estado`: obligatorio.

## Reglas de negocio

* Valida que una cita pertenezca al paciente antes de cambiar su estado.
* Usa borrado lógico por defecto.
* Expone borrado físico mediante el endpoint `force`.

## Dependencias

### Internas

* `PacienteController`
* `PacienteServiceImpl`
* `PacienteRepository`

### Externas

* `msvc-cita`
* `msvc-diagnostico`
* PostgreSQL

## Versión y runtime

* Spring Boot `3.5.9`
* Spring Cloud OpenFeign `2025.0.1`
* Java `25`
* PostgreSQL Driver gestionado por Spring Boot `3.5.9`

## Caso de uso real

* Registro de un nuevo paciente.
* Consulta del historial de citas.
* Actualización de estado de una cita desde un flujo asistencial.

## Ejemplo

```bash
curl -X POST http://localhost:8083/pacientes \
  -H "Content-Type: application/json" \
  -d "{
    \"nombres\":\"Ana\",
    \"apellidos\":\"Lopez\",
    \"fechaNacimiento\":\"1998-04-20\",
    \"genero\":\"FEMENINO\",
    \"dni\":\"70001234\",
    \"telefono\":\"912345678\",
    \"email\":\"ana.lopez@correo.com\",
    \"direccion\":\"Av. Principal 123\",
    \"estado\":\"ACTIVO\"
  }"
```

{% hint style="warning" %}
Este módulo depende de `msvc-cita` para historial y estado de citas. En desarrollo usa `ddl-auto=create-drop`. No es un valor para producción.
{% endhint %}
