# msvc-medico

## Propósito y responsabilidad

Administra datos de médicos, especialidades y coordinación de operaciones clínicas relacionadas con citas y diagnósticos.

## Endpoints principales

| Método | Endpoint | Entrada | Salida |
|---|---|---|---|
| GET | `/medicos` | Sin body | `List<MedicoEntity>` |
| GET | `/medicos/{id}` | `id: Long` | `MedicoEntity` |
| GET | `/medicos/{id}/citas` | `id: Long` | `List<Cita>` |
| POST | `/medicos` | `CrearMedicoDto` | `MedicoEntity` |
| PUT | `/medicos/{id}` | `MedicoEntity` | `MedicoEntity` |
| DELETE | `/medicos/{id}` | `id: Long` | `204` |
| DELETE | `/medicos/{id}/force` | `id: Long` | `204` |
| POST | `/medicos/agendar-cita` | `Cita` | `Cita` |
| POST | `/medicos/registrar-diagnostico` | `Diagnostico` | `Diagnostico` |

## Entradas, salidas y validaciones

### Entrada `MedicoEntity` (vía `CrearMedicoDto`)

- `nombres: String` obligatorio.
- `apellidos: String` obligatorio.
- `especialidad: Enum` obligatoria.
- `telefono: String` obligatorio y validado por regex.
- `email: String` obligatorio y formato email.
- `dni: String` obligatorio, único y 8 dígitos.
- `estado: Enum` obligatorio.

### Validaciones de negocio

- Registro de diagnóstico depende de existencia de cita.
- Borrado lógico por defecto, físico por endpoint `force`.

## Dependencias

### Internas

- `MedicoController`
- `MedicoServiceImpl`
- `MedicoRepository`

### Externas

- `msvc-cita` (OpenFeign)
- `msvc-diagnostico` (OpenFeign)
- MySQL (runtime)

### Versiones relevantes

- Spring Boot: `3.5.9`
- Spring Cloud OpenFeign: `2025.0.1`
- Java: `25`
- MySQL Connector/J: gestionado por BOM de Spring Boot `3.5.9`

## Ejemplo de implementación funcional

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

## Casos de uso reales

- Alta de médico por especialidad.
- Obtención de agenda médica por ID.
- Registro de diagnóstico desde consulta médica.

## Consideraciones importantes

- El contrato de especialidades debe mantenerse consistente con frontend y parser semántico.
- Cualquier cambio en enum de especialidad impacta consultas de lenguaje natural.
- La disponibilidad final de agenda se valida en `msvc-cita`.

## Referencias cruzadas

- [msvc-cita](msvc-cita.md)
- [Consulta semántica](../funcionalidades/consulta-semantica.md)
- [Estructura de código](../estructura-codigo.md)
