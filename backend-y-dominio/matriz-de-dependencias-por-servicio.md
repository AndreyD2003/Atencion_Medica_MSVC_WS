---
description: Qué consume cada componente y para qué lo usa.
icon: project-diagram
---

# Matriz de dependencias por servicio

## Frontend

### Consume

* `msvc-paciente`
* `msvc-medico`
* `msvc-cita`
* `msvc-diagnostico`
* `msvc-web-semantica`

### Para qué

* operación clínica,
* formularios,
* listados,
* consulta semántica.

## msvc-paciente

### Consume

* `msvc-cita`
* `msvc-diagnostico`

### Para qué

* historial de citas,
* estado de citas,
* historial médico.

## msvc-medico

### Consume

* `msvc-cita`
* `msvc-diagnostico`

### Para qué

* agenda médica,
* registro clínico complementario.

## msvc-cita

### Consume

* `msvc-paciente`
* `msvc-medico`
* `msvc-diagnostico`
* `msvc-web-semantica`

### Para qué

* validar paciente,
* validar médico,
* enriquecer detalle de cita,
* sincronizar conocimiento semántico.

## msvc-diagnostico

### Consume

* `msvc-cita`
* `msvc-paciente`
* `msvc-web-semantica`

### Para qué

* validar contexto de cita,
* validar contexto de paciente,
* sincronizar diagnóstico en el grafo.

## msvc-web-semantica

### Consume

* `msvc-paciente`
* `msvc-medico`
* `msvc-cita`
* `msvc-diagnostico`
* Fuseki

### Para qué

* carga masiva,
* sincronización incremental,
* ejecución de consultas RDF.

## Qué leer de esta matriz

* `msvc-cita` es el servicio más acoplado.
* `msvc-web-semantica` depende de todos los datos clínicos.
* `frontend` concentra el consumo pero no reemplaza validaciones backend.

## Regla práctica

Si cambias un contrato en un servicio, revisa primero a sus consumidores directos.
