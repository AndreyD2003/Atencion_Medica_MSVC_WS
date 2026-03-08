---
description: >-
  Recorrido corto para validar que la operación y la parte semántica están
  vivas.
icon: vial
---

# Prueba mínima end-to-end

## Objetivo

Validar que el entorno levantó bien y que la capa transaccional y la semántica responden.

## Verificación mínima

### 1. Confirma que el frontend abre

Si la aplicación no inicia, revisa:

* [Checklist de arranque rápido](checklist-de-arranque-rapido.md)
* [Problemas frecuentes](problemas-frecuentes.md)

### 2. Confirma que la operación clínica funciona

La señal esperada es esta:

* puedes operar pacientes,
* puedes operar médicos,
* puedes operar citas,
* puedes operar diagnósticos.

### 3. Confirma que la semántica funciona

La señal esperada es esta:

* puedes ejecutar consultas semánticas,
* los cambios recientes aparecen también en la búsqueda semántica.

### 4. Si la semántica no refleja cambios

Revisa en este orden:

1. estado de `msvc-web-semantica`,
2. estado de Fuseki,
3. existencia del dataset,
4. y si hace falta ejecuta `POST /api/v1/semantic/bulk-load`.

## Qué valida esta prueba

* que el frontend está operativo,
* que los servicios clínicos responden,
* que Fuseki está disponible,
* que el grafo no está desfasado.

{% hint style="success" %}
Si esta prueba pasa, el entorno ya está en un estado útil para desarrollo y revisión funcional.
{% endhint %}
