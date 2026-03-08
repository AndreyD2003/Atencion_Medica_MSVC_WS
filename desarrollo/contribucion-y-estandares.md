---
description: Flujo de trabajo, validaciones y reglas de cambio.
icon: code-branch
---

# Contribución y estándares

## Objetivo

Mantener coherencia técnica, estabilidad de contratos y calidad del código y la documentación.

## Flujo recomendado

1. Crear una rama por cambio: `feature/*`, `fix/*`, `docs/*`.
2. Implementar cambios acotados por módulo.
3. Ejecutar validaciones locales.
4. Abrir PR con descripción técnica y evidencia.

## Estándares de código

### Backend

* Mantener patrón por capas.
* No exponer entidades JPA directamente cuando se requiera composición.
* Preservar compatibilidad de endpoints.
* Centralizar validaciones en backend.

### Frontend

* Separar servicios API por dominio.
* Reutilizar componentes de UI.
* Mantener tipado explícito.
* Manejar errores HTTP de forma consistente.

## Estándares de documentación

* Títulos jerárquicos.
* Tablas para contratos de API.
* Ejemplos ejecutables.
* Enlaces relativos entre documentos.
* Terminología consistente entre lo transaccional y lo semántico.

## Checklist mínimo

```bash
mvn test
cd nova-frontend
npm run lint
npm run check
```

## Reglas para cambios semánticos

* Documentar impacto en parser y consultas cuando cambie la ontología.
* Actualizar sugerencias y filtros del chat semántico si cambian enums clínicos.
* Ejecutar carga masiva para validar coherencia del grafo.

## Buenas prácticas de rendimiento

* Evitar consultas SPARQL demasiado abiertas sin `LIMIT`.
* Limitar llamadas Feign encadenadas en rutas de alta frecuencia.
* Diseñar endpoints enriquecidos solo cuando se requiera contexto compuesto.
