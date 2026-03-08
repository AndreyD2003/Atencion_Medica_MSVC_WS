# msvc paciente

## Propósito y responsabilidad

Gestiona el ciclo de vida de pacientes y expone operaciones relacionadas con su historial médico y coordinación de citas.

## Endpoints principales

| Método | Endpoint                                        | Entrada              | Salida                 |
| ------ | ----------------------------------------------- | -------------------- | ---------------------- |
| GET    | `/pacientes`                                    | Sin body             | `List<PacienteEntity>` |
| GET    | `/pacientes/{id}`                               | `id: Long`           | `PacienteEntity`       |
| GET    | `/pacientes/{id}/citas`                         | `id: Long`           | `List<Cita>`           |
| GET    | `/pacientes/{id}/historial-medico`              | `id: Long`           | `List<Diagnostico>`    |
| POST   | `/pacientes`                                    | `CrearPacienteDto`   | `PacienteEntity`       |
| PUT    | `/pacientes/{id}`                               | `PacienteEntity`     | `PacienteEntity`       |
| DELETE | `/pacientes/{id}`                               | `id: Long`           | `204`                  |
| DELETE | `/pacientes/{id}/force`                         | `id: Long`           | `204`                  |
| POST   | `/pacientes/agendar-cita`                       | `Cita`               | `Cita`                 |
| PATCH  | `/pacientes/{pacienteId}/citas/{citaId}/estado` | `{ estado: string }` | `Cita`                 |

## Entradas, salidas y validaciones

### Entrada `PacienteEntity` (vía `CrearPacienteDto`)

* `nombres: String` obligatorio.
* `apellidos: String` obligatorio.
* `fechaNacimiento: Date` obligatoria.
* `genero: Enum` obligatorio.
* `dni: String` obligatorio, único y con regex de 8 dígitos.
* `telefono: String` obligatorio y validado por regex.
* `email: String` obligatorio y formato email.
* `direccion: String` obligatoria.
* `estado: Enum` obligatorio.

### Validaciones de negocio

* Cambios de estado de cita: valida que la cita pertenezca al paciente.
* Borrado lógico por defecto y borrado físico explícito por endpoint `force`.

## Dependencias

### Internas

* `PacienteController`
* `PacienteServiceImpl`
* `PacienteRepository`

### Externas

* `msvc-cita` (OpenFeign)
* `msvc-diagnostico` (OpenFeign)
* PostgreSQL (runtime)

### Versiones relevantes

* Spring Boot: `3.5.9`
* Spring Cloud OpenFeign: `2025.0.1`
* Java: `25`
* PostgreSQL Driver: gestionado por BOM de Spring Boot `3.5.9`

## Ejemplo de implementación funcional

{% code title="curl" %}
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
{% endcode %}

## Casos de uso reales

* Registro de nuevo paciente al primer contacto.
* Consulta de historial de citas de un paciente.
* Actualización de estado de cita desde un flujo asistencial.

{% hint style="warning" %}
Consideraciones importantes:

* El módulo depende de disponibilidad de `msvc-cita` para historial y estado de citas.
* En desarrollo usa `ddl-auto=create-drop`; no usar este valor en producción.
* Validaciones del backend son la fuente de verdad aunque exista validación en frontend.
{% endhint %}

## Referencias cruzadas

* [msvc-cita](/broken/pages/48f9fcfa52879b8ec08a1bbfbb215ffa70e2c0a1)
* [Integración Feign](/broken/pages/f53bdf00f5a4cb0b3ee033e5d271afebbc62192d)
* [Estructura de código](/broken/pages/79c7abd49a828d4c5dbe23c463c41a25f1b1d850)
