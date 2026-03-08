# msvc-web-semantica

## Propósito y responsabilidad

Transforma datos clínicos transaccionales en conocimiento semántico y habilita consultas avanzadas mediante SPARQL y lenguaje natural.

## Función de Web Semántica en el proyecto

- Define un vocabulario formal del dominio médico (`atencion-medica.ttl`).
- Representa entidades como tripletas RDF (`sujeto-predicado-objeto`).
- Aplica restricciones OWL para consistencia del grafo.
- Permite consultas declarativas sobre relaciones clínicas.
- Expone una interfaz de consulta amigable para usuarios no expertos.

## Endpoints principales

| Método | Endpoint | Entrada | Salida |
|---|---|---|---|
| GET | `/api/v1/semantic/buscar?texto=...` | `texto: String` | `List<Map<String,String>>` |
| POST | `/api/v1/semantic/sync` | `SyncRequestDTO` | `String` |
| POST | `/api/v1/semantic/sync/diagnostico` | `DiagnosticoSyncDTO` | `String` |
| POST | `/api/v1/semantic/bulk-load` | Sin body | `String` |
| POST | `/api/v1/semantic/sparql` | `{ query: String }` | `List<Map<String,String>>` |

## Entradas, salidas y validaciones

### Entrada `SyncRequestDTO`

- `citaId: Long`
- `fechaCita: String`
- `horaInicio: String`
- `horaFin: String`
- `motivo: String`
- `estadoCita: String`
- `pacienteId: Long`
- `dniPaciente: String`
- `nombrePaciente: String`
- `apellidoPaciente: String`
- `generoPaciente: String`
- `emailPaciente: String`
- `medicoId: Long`
- `dniMedico: String`
- `nombreMedico: String`
- `apellidoMedico: String`
- `especialidad: String`
- `diagnosticos: List<DiagnosticoSyncDTO>`

### Validaciones de negocio

- Consulta vacía en `/buscar` devuelve lista vacía.
- Body de `/sparql` requiere `query`; si está ausente responde `400`.
- Sincronización usa patrón `DELETE + INSERT` para evitar duplicados.

## Dependencias

### Internas

- `SemanticController`
- `SemanticServiceImpl`
- `BulkSyncService`
- `FusekiRepository`
- `QueryParser`
- `SparqlBuilder`

### Externas

- Apache Jena Fuseki (query/update URL)
- OpenFeign hacia `msvc-paciente`, `msvc-medico`, `msvc-cita`, `msvc-diagnostico`
- Librerías: Jena 5.3.0, Lucene 9.9.1, OWL API 5.1.20

### Versiones relevantes

- Spring Boot: `3.5.9`
- Spring Cloud OpenFeign: `2025.0.1`
- Java: `25`
- Jena: `5.3.0`
- Lucene: `9.9.1`
- OWL API: `5.1.20`

## Ejemplo de implementación funcional

### Carga masiva

```bash
curl -X POST http://localhost:8084/api/v1/semantic/bulk-load
```

### Consulta semántica por lenguaje natural

```bash
curl "http://localhost:8084/api/v1/semantic/buscar?texto=top%205%20medicos%20con%20mas%20citas"
```

### Consulta SPARQL directa

```bash
curl -X POST http://localhost:8084/api/v1/semantic/sparql \
  -H "Content-Type: application/json" \
  -d "{\"query\":\"PREFIX med: <http://org.nova.atencion.medica/ontologia#> SELECT ?medico ?esp WHERE { ?medico a med:Medico ; med:especialidad ?esp . } LIMIT 5\"}"
```

## Casos de uso reales

- Preguntar por disponibilidad médica en una fecha/hora.
- Identificar ranking de médicos con mayor volumen de citas.
- Filtrar citas por especialidad, estado, DNI o rango temporal.

## Limitaciones y rendimiento

- El parser de lenguaje natural está orientado a patrones clínicos definidos.
- El tiempo de respuesta depende de estado de Fuseki y volumen de tripletas.
- El grafo puede quedar desactualizado si falla sincronización incremental y no se ejecuta carga masiva.

## Observaciones de integración actuales

- Se mantiene alineado el endpoint de sincronización de diagnóstico con `msvc-diagnostico`.
- Los clientes Feign de integración se encuentran normalizados con esquema `http://`.

## Buenas prácticas

- Ejecutar `/bulk-load` tras cambios de datos históricos o restauraciones.
- Versionar cambios de ontología y revisar impacto en consultas.
- Alinear nombres de especialidad y estado entre backend transaccional y vocabulario semántico.

## Referencias cruzadas

- [Consulta semántica](../funcionalidades/consulta-semantica.md)
- [Flujos de datos](../arquitectura/flujos-datos.md)
- [Integración Feign](../funcionalidades/integracion-feign.md)
