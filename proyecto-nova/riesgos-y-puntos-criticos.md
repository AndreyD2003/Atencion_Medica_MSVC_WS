---
description: Dónde puede romperse el sistema y qué revisar primero.
icon: triangle-exclamation
---

# Riesgos y puntos críticos

## 1. Acoplamiento síncrono entre servicios

### Qué lo hace crítico

La composición de datos depende de OpenFeign. Eso acumula latencia y puede generar cascadas.

### Dónde se nota más

* `msvc-cita`
* `msvc-diagnostico`
* `msvc-web-semantica`

### Qué revisar primero

* disponibilidad del servicio remoto,
* alineación de endpoints,
* conectividad entre servicios.

## 2. Desfase entre datos operativos y grafo semántico

### Qué lo causa

* fallo en sincronización incremental,
* restauraciones,
* cambios históricos de datos.

### Qué revisar primero

* estado de `msvc-web-semantica`,
* estado de Fuseki,
* ejecución de `bulk-load`.

## 3. Cambios en enums y vocabulario clínico

### Qué impactan

* frontend,
* parser semántico,
* ontología,
* filtros y sugerencias,
* consultas SPARQL.

### Casos sensibles

* especialidades,
* estados de cita,
* tipos de diagnóstico.

## 4. Consultas demasiado abiertas

### Qué impactan

* tiempo de respuesta,
* costo de ejecución en Fuseki,
* experiencia del usuario.

### Recomendación ya documentada

Evitar consultas SPARQL excesivamente abiertas sin `LIMIT`.

## 5. Configuración distinta por ambiente

### Qué lo hace peligroso

* URLs Feign estáticas,
* diferencias entre staging y producción,
* variables no centralizadas.

### Qué revisar primero

* configuración de endpoints,
* proxy local del frontend,
* parámetros por ambiente.

## 6. Persistencia con comportamientos distintos

### Qué tener presente

* `msvc-medico` y `msvc-cita` usan MySQL.
* `msvc-paciente` y `msvc-diagnostico` usan PostgreSQL.
* `msvc-paciente` usa `ddl-auto=create-drop` en desarrollo.

## Qué módulo merece más atención

### `msvc-cita`

Es el centro operativo del sistema.

* valida disponibilidad,
* integra varios servicios,
* y dispara sincronización semántica.

### `msvc-web-semantica`

Es el centro de consistencia semántica.

* depende de Fuseki,
* depende del vocabulario,
* y depende de que el grafo esté alineado.

{% hint style="warning" %}
Cuando un error cruza backend transaccional y capa semántica, empieza por validar el flujo transaccional. Luego revisa sincronización y grafo.
{% endhint %}
