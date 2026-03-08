---
description: Qué leer primero según seas nuevo en el proyecto o ya vengas con experiencia.
icon: route
---

# Ruta de lectura según tu perfil

## Si eres nuevo en el tema

Sigue este orden:

1. [Visión general](vision-general.md)
2. [Arquitectura del sistema](arquitectura-del-sistema.md)
3. [Flujos principales](flujos-principales.md)
4. [Aplicación web](../frontend/aplicacion-web.md)
5. [Visión general de la capa semántica](../capa-semantica/vision-general-de-la-capa-semantica.md)

### Qué deberías entender al terminar

* Qué problema resuelve cada microservicio.
* Por qué existe una capa semántica aparte.
* Cómo entra una acción desde frontend y dónde termina.
* Qué partes son operativas y cuáles son analíticas.

## Si ya eres desarrollador senior

Sigue este orden:

1. [Arquitectura del sistema](arquitectura-del-sistema.md)
2. [Integración entre microservicios](../backend-y-dominio/integracion-entre-microservicios.md)
3. [Panorama del backend](../backend-y-dominio/panorama-del-backend.md)
4. [Sincronización con Fuseki](../capa-semantica/sincronizacion-con-fuseki.md)
5. [Contribución y estándares](../desarrollo/contribucion-y-estandares.md)

### Qué deberías detectar rápido

* Puntos de acoplamiento por Feign.
* Riesgos de latencia y cascada.
* Dependencia de consistencia entre modelo transaccional y grafo.
* Impacto de cambios en enums, ontología y contratos.

## Si vienes solo a levantar el entorno

1. [ejecucion-local.md](../puesta-en-marcha/ejecucion-local.md "mention")
2. [problemas-frecuentes.md](../puesta-en-marcha/problemas-frecuentes.md "mention")
3. [estructura-del-repositorio.md](../puesta-en-marcha/estructura-del-repositorio.md "mention")

{% hint style="info" %}
La ruta cambia, pero el proyecto siempre se entiende mejor desde tres preguntas: qué datos guarda, qué valida y qué sincroniza.
{% endhint %}
