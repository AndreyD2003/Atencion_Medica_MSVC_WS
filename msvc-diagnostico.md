# msvc diagnostico

## Propósito y responsabilidad

Gestiona diagnósticos clínicos y su relación con citas y pacientes, incluyendo sincronización del diagnóstico hacia el grafo semántico.

## Endpoints principales

| Método | Endpoint                         | Entrada             | Salida                    |
| ------ | -------------------------------- | ------------------- | ------------------------- |
| GET    | `/diagnosticos`                  | Sin body            | `List<DiagnosticoEntity>` |
| GET    | `/diagnosticos/{id}`             | `id: Long`          | `DiagnosticoEntity`       |
| GET    | `/diagnosticos/con-detalle/{id}` | `id: Long`          | `DiagnosticoDetalle`      |
| GET    | `/diagnosticos/cita/{id}`        | `id: Long`          | `List<DiagnosticoEntity>` |
| GET    | `/diagnosticos/paciente/{id}`    | `id: Long`          | `List<DiagnosticoEntity>` |
| POST   | `/diagnosticos`                  | `DiagnosticoEntity` | `DiagnosticoEntity`       |
| PUT    | `/diagnosticos/{id}`             | `DiagnosticoEntity` | `DiagnosticoEntity`       |
| DELETE | `/diagnosticos/{id}`             | `id: Long`          | `204`                     |
| DELETE | `/diagnosticos/{id}/force`       | `id: Long`          | `204`                     |

## Entradas, salidas y validaciones

### Entrada `DiagnosticoEntity`

* `descripcion: String` obligatoria.
* `tipoDiagnostico: Enum` obligatorio.
* `fechaDiagnostico: Date` obligatoria.
* `citaId: Long` obligatorio.
* `pacienteId: Long` obligatorio.

### Salida enriquecida `DiagnosticoDetalle`

* `diagnostico: DiagnosticoEntity`
* `cita: Cita`
* `paciente: Paciente`

### Validaciones de negocio

* Borrado lógico por defecto.
* Actualización y creación sincronizan diagnóstico en capa semántica.
* Las referencias de cita/paciente se validan vía servicios remotos cuando aplica.

## Dependencias

### Internas

* `DiagnosticoController`
* `DiagnosticoServiceImpl`
* `DiagnosticoRepository`

### Externas

* `msvc-cita` (OpenFeign)
* `msvc-paciente` (OpenFeign)
* `msvc-web-semantica` (OpenFeign)
* PostgreSQL (runtime)

### Versiones relevantes

* Spring Boot: `3.5.9`
* Spring Cloud OpenFeign: `2025.0.1`
* Java: `25`
* PostgreSQL Driver: gestionado por BOM de Spring Boot `3.5.9`

## Ejemplo de implementación funcional

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

## Casos de uso reales

* Registro de diagnóstico posterior a consulta.
* Consulta de diagnósticos de una cita específica.
* Historial de diagnósticos por paciente.

## Consideraciones importantes

* Cambios de estructura en diagnóstico impactan ontología y consultas SPARQL.
* El endpoint configurado en Feign para sincronización debe mantenerse alineado con `msvc-web-semantica`.
* Conviene ejecutar carga masiva semántica tras migraciones de datos históricos.

## Referencias cruzadas

* [msvc-web-semantica](/broken/pages/d81bb281e79814d86cfe60da521efb84dc68e6ea)
* [Consulta semántica](/broken/pages/e978f473fec2979725627041eeab2cb4cb313288)
* [Flujos de datos](/broken/pages/f3d0853081df61a06e18c4acc8041a91b4154e56)
