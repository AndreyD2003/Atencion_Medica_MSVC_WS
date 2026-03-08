# Estructura de Código

## Mapa del repositorio

```text
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

## Explicación por directorio

- `msvc-*`: cada módulo implementa un bounded context clínico con base de datos propia.
- `msvc-web-semantica`: integra conocimiento RDF/OWL y consultas SPARQL.
- `nova-frontend`: aplicación SPA para operación y consulta.
- `documentacion`: documentación histórica previa.
- `docs`: documentación técnica vigente.

## Archivos clave por módulo

- Backend:
  - `.../controllers/*Controller.java`: contratos HTTP.
  - `.../services/*ServiceImpl.java`: lógica de negocio.
  - `.../repositories/*Repository.java`: acceso a persistencia.
  - `.../clients/*ClientRest.java`: integración remota Feign.
  - `.../resources/application.properties`: puertos, DB, parámetros.
- Frontend:
  - `src/App.tsx`: rutas.
  - `src/components/layout/AppLayout.tsx`: navegación principal.
  - `src/pages/*`: pantallas por dominio.
  - `src/services/*.service.ts`: contratos hacia backend.
  - `vite.config.ts`: proxy local por microservicio.

## Convenciones de organización

- Código Java en paquetes por responsabilidad.
- DTOs separados de entidades para evitar acoplamiento de API.
- Servicios frontend alineados por dominio.
- Rutas frontend equivalentes a módulos funcionales del backend.

## Referencias cruzadas

- [Arquitectura](arquitectura/arquitectura-sistema.md)
- [Módulos](README.md#módulos)
- [Guía de contribución](guia-contribucion.md)
