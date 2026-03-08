---
description: Gestión de médicos, especialidades y operaciones clínicas relacionadas.
icon: user-doctor
---

# msvc-medico

## Responsabilidad

Administra datos de médicos, especialidades y coordinación de operaciones clínicas relacionadas con citas y diagnósticos.

## Endpoints principales

* `GET /medicos`
* `GET /medicos/{id}`
* `GET /medicos/{id}/citas`
* `POST /medicos`
* `PUT /medicos/{id}`
* `DELETE /medicos/{id}`
* `DELETE /medicos/{id}/force`
* `POST /medicos/agendar-cita`
* `POST /medicos/registrar-diagnostico`

## Contrato principal de entrada

### `CrearMedicoDto`

* `nombres`: obligatorio.
* `apellidos`: obligatorio.
* `especialidad`: obligatoria.
* `telefono`: obligatorio y validado por regex.
* `email`: obligatorio y con formato email.
* `dni`: obligatorio, único y de 8 dígitos.
* `estado`: obligatorio.

## Reglas de negocio

* Registrar diagnóstico requiere que exista la cita relacionada.
* El borrado por defecto es lógico.
* El borrado físico usa el endpoint `force`.

## Dependencias

### Internas

* `MedicoController`
* `MedicoServiceImpl`
* `MedicoRepository`

### Externas

* `msvc-cita`
* `msvc-diagnostico`
* MySQL

## Versión y runtime

* Spring Boot `3.5.9`
* Spring Cloud OpenFeign `2025.0.1`
* Java `25`
* MySQL Connector/J gestionado por Spring Boot `3.5.9`

## Casos de uso reales

* Alta de médico por especialidad.
* Consulta de agenda médica por ID.
* Registro de diagnóstico desde una consulta.

## Ejemplo

```bash
curl -X POST http://localhost:8080/medicos \
  -H "Content-Type: application/json" \
  -d "{
    \"nombres\":\"Julio\",
    \"apellidos\":\"Perez\",
    \"especialidad\":\"CARDIOLOGIA\",
    \"telefono\":\"987654321\",
    \"email\":\"julio.perez@hospital.com\",
    \"dni\":\"71234567\",
    \"estado\":\"ACTIVO\"
  }"
```

{% hint style="info" %}
La disponibilidad final de agenda se valida en `msvc-cita`. Cualquier cambio en enums de especialidad impacta al frontend y a la capa semántica.
{% endhint %}
