# msvc-cita

## Propósito y responsabilidad

Es el núcleo de agenda clínica. Orquesta creación y consulta de citas, valida reglas de disponibilidad y sincroniza eventos relevantes hacia la capa semántica.

## Endpoints principales

| Método | Endpoint | Entrada | Salida |
|---|---|---|---|
| GET | `/citas` | Sin body | `List<CitaEntity>` |
| GET | `/citas/{id}` | `id: Long` | `CitaEntity` |
| GET | `/citas/con-detalle/{id}` | `id: Long` | `CitaDetalle` |
| GET | `/citas/paciente/{id}` | `id: Long` | `List<CitaEntity>` |
| GET | `/citas/medico/{id}` | `id: Long` | `List<CitaEntity>` |
| POST | `/citas` | `CitaEntity` | `CitaEntity` |
| PUT | `/citas/{id}` | `CitaEntity` | `CitaEntity` |
| DELETE | `/citas/{id}` | `id: Long` | `204` |
| DELETE | `/citas/{id}/force` | `id: Long` | `204` |

## Entradas, salidas y validaciones

### Entrada `CitaEntity`

- `fechaCita: Date` obligatoria.
- `horaInicio: Time` obligatoria.
- `horaFin: Time` obligatoria.
- `motivo: String` obligatorio.
- `estado: Enum` obligatorio.
- `pacienteId: Long` obligatorio.
- `medicoId: Long` obligatorio.

### Salida enriquecida `CitaDetalle`

- `cita: CitaEntity`
- `paciente: Paciente`
- `medico: Medico`
- `diagnosticos: List<Diagnostico>`

### Validaciones de negocio

- Evita solapamiento de horarios por médico y paciente.
- Valida existencia/estado de paciente y médico en servicios remotos.
- Normaliza fecha/hora antes de persistir.
- Sincroniza cita con `msvc-web-semantica` luego de guardar/actualizar.

## Dependencias

### Internas

- `CitaController`
- `CitaServiceImpl`
- `CitaRepository`

### Externas

- `msvc-paciente` (OpenFeign)
- `msvc-medico` (OpenFeign)
- `msvc-diagnostico` (OpenFeign)
- `msvc-web-semantica` (OpenFeign)
- MySQL (runtime)

### Versiones relevantes

- Spring Boot: `3.5.9`
- Spring Cloud OpenFeign: `2025.0.1`
- Java: `25`
- MySQL Connector/J: gestionado por BOM de Spring Boot `3.5.9`

## Ejemplo de implementación funcional

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

## Casos de uso reales

- Programación de consulta médica.
- Visualización de cita con contexto completo de paciente/médico/diagnósticos.
- Listado de citas por paciente para historia clínica.

## Consideraciones importantes

- Es el principal punto de fallo en cascada por alta integración.
- Si falla sincronización semántica debe revisarse conectividad al servicio semántico.
- Dependencias Feign con URL estática requieren control estricto en staging/producción.

## Referencias cruzadas

- [msvc-web-semantica](msvc-web-semantica.md)
- [Integración Feign](../funcionalidades/integracion-feign.md)
- [Flujos de datos](../arquitectura/flujos-datos.md)
