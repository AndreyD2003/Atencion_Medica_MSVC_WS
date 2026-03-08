---
description: Componentes, dependencias y decisiones de diseño.
icon: sitemap
---

# Arquitectura del sistema

## Objetivo arquitectónico

NOVA implementa una arquitectura distribuida. El objetivo es desacoplar responsabilidades clínicas por dominio y añadir una capa de conocimiento semántico.

### Vista de componentes

```mermaid
graph TD
    FE[Frontend React]
    PAC[MSVC Paciente]
    MED[MSVC Medico]
    CIT[MSVC Cita]
    DIA[MSVC Diagnostico]
    SEM[MSVC Web Semantica]
    FUS[(Fuseki)]
    PSQL[(PostgreSQL)]
    MYSQL[(MySQL)]

    FE --> PAC
    FE --> MED
    FE --> CIT
    FE --> DIA
    FE --> SEM

    PAC --> CIT
    MED --> CIT
    CIT --> PAC
    CIT --> MED
    CIT --> DIA
    CIT --> SEM
    DIA --> CIT
    DIA --> PAC
    DIA --> SEM

    PAC --> PSQL
    DIA --> PSQL
    MED --> MYSQL
    CIT --> MYSQL
    SEM --> FUS
```

### Responsabilidades por componente

* `msvc-paciente`: ciclo de vida del paciente e historial desde su perspectiva.
* `msvc-medico`: gestión de médicos y especialidades.
* `msvc-cita`: validación de agenda, solapes y enriquecimiento de respuestas.
* `msvc-diagnostico`: diagnósticos vinculados a cita y paciente.
* `msvc-web-semantica`: RDF, SPARQL y lenguaje natural.
* `nova-frontend`: interfaz de operación clínica y exploración semántica.

### Patrones que aparecen en el proyecto

* Backend por capas: `Controller -> Service -> Repository/Feign Client`.
* Integración síncrona mediante OpenFeign.
* Persistencia políglota por dominio.
* Separación entre datos operativos y conocimiento.

{% hint style="info" %}
La capa semántica no reemplaza al modelo transaccional. Lo complementa.
{% endhint %}

### Persistencia por módulo

* `msvc-medico`: MySQL.
* `msvc-cita`: MySQL.
* `msvc-paciente`: PostgreSQL.
* `msvc-diagnostico`: PostgreSQL.
* `msvc-web-semantica`: Apache Jena Fuseki.

### Riesgos ya visibles en el diseño

* Desalineación de endpoints entre servicios.
* Desfase entre datos operativos y grafo semántico.
* Cascadas por integración síncrona en rutas compuestas.
* Diferencias entre ambientes si no se centralizan variables.

### Mitigaciones documentadas

* Mantener contratos claros entre servicios.
* Ejecutar carga masiva cuando el grafo pueda quedar desactualizado.
* Revisar conectividad y configuración por ambiente.
* Limitar consultas abiertas y llamadas encadenadas frecuentes.
