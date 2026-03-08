---
description: Relación entre rutas del frontend y los servicios del backend.
icon: table-cells-large
---

# Pantallas y APIs consumidas

## Relación principal

* `/pacientes` consume operaciones de `msvc-paciente`.
* `/medicos` consume operaciones de `msvc-medico`.
* `/citas` consume operaciones de `msvc-cita`.
* `/diagnosticos` consume operaciones de `msvc-diagnostico`.
* `/semantic` consume operaciones de `msvc-web-semantica`.

## Proxy de desarrollo

```
/api/pacientes    -> http://localhost:8083/pacientes
/api/medicos      -> http://localhost:8080/medicos
/api/citas        -> http://localhost:8081/citas
/api/diagnosticos -> http://localhost:8082/diagnosticos
/api/v1/semantic  -> http://localhost:8084/api/v1/semantic
```

## Cómo leer una pantalla

### Pantallas transaccionales

* Toman datos de formularios.
* Llaman a servicios API por dominio.
* Delegan la validación fuerte al backend.
* Muestran tablas, listados y mensajes de error o éxito.

### Pantalla semántica

* Acepta texto libre.
* Puede aceptar SPARQL manual.
* Devuelve resultados estructurados según la consulta.

## Puntos de acoplamiento visibles

* Los enums deben coincidir con backend.
* Las sugerencias del chat deben coincidir con `QueryParser`.
* El proxy solo resuelve desarrollo local.

{% hint style="info" %}
Si una pantalla falla, primero distingue si el error está en formulario, proxy local, contrato HTTP o sincronización semántica.
{% endhint %}
