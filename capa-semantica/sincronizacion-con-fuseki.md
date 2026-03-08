---
description: Carga incremental y masiva del grafo semántico.
icon: arrows-rotate
---

# Sincronización con Fuseki

## Dos modos de sincronización

### Sincronización incremental

Se usa cuando cambia una cita o un diagnóstico.

#### Endpoints

* `POST /api/v1/semantic/sync`
* `POST /api/v1/semantic/sync/diagnostico`

#### Comportamiento

* Reúne datos clínicos necesarios.
* Ejecuta un patrón `DELETE + INSERT`.
* Evita duplicados en el grafo.

### Sincronización masiva

Se usa para reconstruir el conocimiento completo.

#### Endpoint

* `POST /api/v1/semantic/bulk-load`

#### Comportamiento

1. Limpia el grafo por defecto.
2. Consulta pacientes.
3. Consulta médicos.
4. Consulta citas.
5. Consulta diagnósticos.
6. Inserta datos en Fuseki por entidad.

## Entrada principal para cita

### `SyncRequestDTO`

* `citaId`
* `fechaCita`
* `horaInicio`
* `horaFin`
* `motivo`
* `estadoCita`
* `pacienteId`
* `dniPaciente`
* `nombrePaciente`
* `apellidoPaciente`
* `generoPaciente`
* `emailPaciente`
* `medicoId`
* `dniMedico`
* `nombreMedico`
* `apellidoMedico`
* `especialidad`
* `diagnosticos`

## Preparación manual de Fuseki

### Ruta de arranque documentada

```bash
cd msvc-web-semantica\target\apache-jena-fuseki-6.0.0
java -jar .\fuseki-server.jar
```

### Dataset esperado

* Nombre: `atencion_medica`
* Tipo: `Persistent (TDB2)`

### Archivo a cargar

* `atencion-medica.ttl`

## Buenas prácticas

* Ejecutar `bulk-load` tras cambios de datos históricos.
* Ejecutar `bulk-load` después de restauraciones.
* Ejecutar `bulk-load` al iniciar ambientes si el grafo no es confiable.

## Riesgos operativos

* El grafo puede quedar desactualizado si falla la sincronización incremental.
* El tiempo de respuesta depende del estado de Fuseki y del volumen de tripletas.
* La conectividad entre servicios debe mantenerse alineada.
