---
description: Dependencias Feign y composición de datos entre módulos.
icon: share-nodes
---

# Integración entre microservicios

## Propósito

La comunicación síncrona se usa para validar reglas de negocio y enriquecer respuestas.

## Mapa de dependencias

* `msvc-cita -> msvc-paciente`: validar y obtener paciente.
* `msvc-cita -> msvc-medico`: validar y obtener médico.
* `msvc-cita -> msvc-diagnostico`: incluir diagnósticos en detalle.
* `msvc-cita -> msvc-web-semantica`: sincronizar citas.
* `msvc-paciente -> msvc-cita`: historial y estado de citas.
* `msvc-paciente -> msvc-diagnostico`: historial médico.
* `msvc-medico -> msvc-cita`: agenda médica.
* `msvc-medico -> msvc-diagnostico`: registro clínico complementario.
* `msvc-diagnostico -> msvc-cita`: contexto de cita.
* `msvc-diagnostico -> msvc-paciente`: contexto de paciente.
* `msvc-diagnostico -> msvc-web-semantica`: sincronizar diagnóstico.
* `msvc-web-semantica -> todos los transaccionales`: carga masiva del grafo.

## Qué entra y qué sale

* Entradas típicas: IDs y DTOs de dominio.
* Salidas típicas: entidades o DTOs enriquecidos con datos remotos.
* Códigos esperados: `200`, `201`, `204`.

## Ejemplo de cliente Feign

```java
@FeignClient(name = "msvc-paciente", url = "http://localhost:8083/pacientes")
public interface PacienteClientRest {
    @GetMapping("/{id}")
    Paciente detalle(@PathVariable Long id);
}
```

## Escenario representativo

Al crear una cita, `msvc-cita` consulta paciente y médico, valida disponibilidad y devuelve la entidad persistida.

## Riesgos de esta integración

* Aumenta la latencia acumulada.
* Puede generar fallos en cascada.
* Obliga a mantener contratos alineados.

## Buenas prácticas ya documentadas

* Evitar lógica compleja dentro de clientes Feign.
* Mantener DTOs explícitos.
* Aislar adaptaciones de datos en `Service`.
* Configurar timeout y reintentos por ambiente cuando corresponda.
