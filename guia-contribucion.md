# guia contribucion

## Objetivo

Establecer reglas de trabajo para mantener coherencia técnica, estabilidad de contratos y calidad del código/documentación.

## Flujo recomendado

1. Crear rama por cambio (`feature/*`, `fix/*`, `docs/*`).
2. Implementar cambios acotados por módulo.
3. Ejecutar validaciones locales.
4. Abrir PR con descripción técnica y evidencia.

## Estándares de código

### Backend

* Mantener patrón por capas.
* No exponer entidades JPA directamente cuando se requiera composición de datos.
* Preservar compatibilidad de endpoints existentes.
* Centralizar validaciones en backend con anotaciones y lógica de negocio.

### Frontend

* Servicios API separados por dominio.
* Componentes de UI reutilizables y desacoplados.
* Tipado explícito de contratos.
* Manejo de errores HTTP consistente.

## Estándares de documentación

* Markdown con títulos jerárquicos.
* Tablas para contratos de API.
* Ejemplos ejecutables con bloques de código.
* Enlaces relativos entre documentos.
* Terminología consistente entre transaccional y semántico.

## Checklist mínimo antes de integrar

```bash
mvn test
cd nova-frontend
npm run lint
npm run check
```

## Reglas para cambios semánticos

* Si se modifica la ontología, documentar impacto en parser y consultas.
* Si se agregan nuevos enums clínicos, actualizar sugerencias y filtros del chat semántico.
* Ejecutar carga masiva para validar coherencia del grafo.

## Buenas prácticas de rendimiento

* Evitar consultas SPARQL excesivamente abiertas sin `LIMIT`.
* Limitar llamadas encadenadas Feign en rutas de alta frecuencia.
* Diseñar endpoints enriquecidos solo cuando se requiera contexto compuesto.

## Referencias cruzadas

* [Arquitectura](/broken/pages/175413b179896bd6cc6f42f137b94cffe60ff6a4)
* [Consulta semántica](/broken/pages/e978f473fec2979725627041eeab2cb4cb313288)
* [Integración Feign](/broken/pages/f53bdf00f5a4cb0b3ee033e5d271afebbc62192d)
