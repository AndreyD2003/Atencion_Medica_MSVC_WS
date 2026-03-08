---
description: Verificación mínima para saber si el entorno local quedó bien levantado.
icon: list-check
---

# Checklist de arranque rápido

## Antes de probar el sistema

Confirma estos puntos:

* Los microservicios están levantados.
* Fuseki está corriendo.
* El dataset `atencion_medica` existe.
* El dataset usa `Persistent (TDB2)`.
* El archivo `atencion-medica.ttl` fue cargado.
* El frontend inició con `npm run dev`.

## Secuencia mínima

1. Levanta backend.
2. Inicia Fuseki.
3. Crea el dataset.
4. Carga el `.ttl`.
5. Inicia frontend.

## Si algo falla

### El frontend no inicia

1. Ejecuta `npm run build`.
2. Luego repite `npm run dev`.

### La parte semántica responde mal

Revisa:

* estado de Fuseki,
* existencia del dataset,
* carga del `.ttl`,
* y luego ejecuta `POST /api/v1/semantic/bulk-load` si el grafo quedó desactualizado.

## Señal de entorno sano

* Puedes operar pacientes, médicos, citas y diagnósticos.
* Puedes lanzar consultas semánticas.
* Los cambios recientes aparecen también en la búsqueda semántica.
