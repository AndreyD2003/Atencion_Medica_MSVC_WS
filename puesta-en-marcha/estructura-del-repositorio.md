---
description: Mapa del código y convenciones de organización.
icon: folder-tree
---

# Estructura del repositorio

## Mapa general

```
Atencion_Medica_MSVC_WS/
├─ msvc-medico/
│  ├─ src/main/java/.../controllers
│  ├─ src/main/java/.../services
│  ├─ src/main/java/.../repositories
│  ├─ src/main/java/.../models
│  └─ src/main/resources/application.properties
├─ msvc-paciente/
│  ├─ src/main/java/.../controllers
│  ├─ src/main/java/.../services
│  ├─ src/main/java/.../repositories
│  ├─ src/main/java/.../models
│  └─ src/main/resources/application.properties
├─ msvc-cita/
│  ├─ src/main/java/.../controllers
│  ├─ src/main/java/.../services
│  ├─ src/main/java/.../repositories
│  ├─ src/main/java/.../models
│  ├─ src/main/java/.../clients
│  └─ src/main/resources/application.properties
├─ msvc-diagnostico/
│  ├─ src/main/java/.../controllers
│  ├─ src/main/java/.../services
│  ├─ src/main/java/.../repositories
│  ├─ src/main/java/.../models
│  ├─ src/main/java/.../clients
│  └─ src/main/resources/application.properties
├─ msvc-web-semantica/
│  ├─ src/main/java/.../controllers
│  ├─ src/main/java/.../services
│  ├─ src/main/java/.../repositories
│  ├─ src/main/java/.../parsers
│  ├─ src/main/java/.../clients
│  ├─ src/main/java/.../dtos
│  └─ src/main/resources/ontology/atencion-medica.ttl
├─ nova-frontend/
│  ├─ src/api
│  ├─ src/components
│  ├─ src/context
│  ├─ src/pages
│  ├─ src/services
│  ├─ src/types
│  └─ vite.config.ts
├─ documentacion/
├─ docs/
├─ run-backend.bat
├─ run-frontend.bat
└─ pom.xml
```

## Qué representa cada directorio

* `msvc-*`: módulos clínicos con base de datos propia.
* `msvc-web-semantica`: RDF, OWL, SPARQL y consultas semánticas.
* `nova-frontend`: SPA para operación y consulta.
* `documentacion`: documentación histórica previa.
* `docs`: documentación técnica vigente.

## Archivos y carpetas clave

### Backend

* `controllers`: contratos HTTP.
* `services`: lógica de negocio.
* `repositories`: acceso a persistencia.
* `clients`: integración remota por Feign.
* `application.properties`: puertos, bases y parámetros.

### Frontend

* `src/App.tsx`: rutas.
* `src/components/layout/AppLayout.tsx`: navegación principal.
* `src/pages`: pantallas por dominio.
* `src/services/*.service.ts`: contratos hacia backend.
* `vite.config.ts`: proxy local por microservicio.

## Convenciones que ya usa el proyecto

* Paquetes Java por responsabilidad.
* DTOs separados de entidades.
* Servicios frontend alineados por dominio.
* Rutas frontend equivalentes a módulos funcionales del backend.
