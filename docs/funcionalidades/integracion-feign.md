# Integración entre Microservicios con OpenFeign

## Propósito

Documentar la comunicación síncrona entre microservicios para enriquecimiento de respuestas y validaciones de negocio.

## Mapa de dependencias Feign

| Origen | Destino | Uso |
|---|---|---|
| `msvc-cita` | `msvc-paciente` | Validar/obtener paciente |
| `msvc-cita` | `msvc-medico` | Validar/obtener médico |
| `msvc-cita` | `msvc-diagnostico` | Incluir diagnósticos en detalle |
| `msvc-cita` | `msvc-web-semantica` | Sincronización semántica de cita |
| `msvc-paciente` | `msvc-cita` | Historial y estado de citas |
| `msvc-paciente` | `msvc-diagnostico` | Historial médico |
| `msvc-medico` | `msvc-cita` | Agenda de médico |
| `msvc-medico` | `msvc-diagnostico` | Registro clínico complementario |
| `msvc-diagnostico` | `msvc-cita` | Contexto de cita |
| `msvc-diagnostico` | `msvc-paciente` | Contexto de paciente |
| `msvc-diagnostico` | `msvc-web-semantica` | Sincronización de diagnóstico |
| `msvc-web-semantica` | Todos los transaccionales | Carga masiva del grafo |

## Contratos de entrada y salida

- Entrada principal: IDs de entidades (`Long`) y DTOs de dominio.
- Salida principal: DTOs enriquecidos con entidades remotas.
- Códigos HTTP esperados: `200`, `201`, `204`; errores remotos deben propagarse/controlarse.

## Ejemplo funcional

```java
@FeignClient(name = "msvc-paciente", url = "http://localhost:8083/pacientes")
public interface PacienteClientRest {
    @GetMapping("/{id}")
    Paciente detalle(@PathVariable Long id);
}
```

## Escenario real

Al crear una cita, `msvc-cita` consume paciente y médico por Feign, valida reglas de disponibilidad y retorna entidad persistida.

## Consideraciones de diseño y rendimiento

- Integración síncrona aumenta latencia acumulada en rutas compuestas.
- Timeout/reintentos deben configurarse por ambiente para evitar cascadas.
- Cambios de endpoints requieren actualización coordinada de interfaces Feign.
- Se recomienda incorporar pruebas de contrato en evolución futura.

## Buenas prácticas

- Evitar lógica compleja dentro de clientes Feign.
- Mantener DTOs de integración explícitos y versionables.
- Aislar adaptaciones de datos en capa `Service`.

## Referencias cruzadas

- [Arquitectura del sistema](../arquitectura/arquitectura-sistema.md)
- [msvc-cita](../modulos/msvc-cita.md)
- [msvc-web-semantica](../modulos/msvc-web-semantica.md)
