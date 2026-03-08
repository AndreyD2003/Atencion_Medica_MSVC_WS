---
description: Rutas, responsabilidades y consumo de APIs desde el frontend.
icon: desktop
---

# Aplicación web

## Responsabilidad

Entrega la interfaz web de operación clínica y el acceso a capacidades semánticas del backend.

## Rutas funcionales

* `/`: dashboard general.
* `/pacientes`: gestión de pacientes.
* `/medicos`: gestión de médicos.
* `/citas`: gestión de citas.
* `/diagnosticos`: gestión de diagnósticos.
* `/semantic`: chat y consultas semánticas.

## Qué entra y qué sale

### Entradas

* Formularios de alta y edición para paciente, médico, cita y diagnóstico.
* Texto libre para búsqueda semántica.
* Query SPARQL manual para administración.

### Salidas

* Tablas y listados por dominio.
* Mensajes de éxito y error.
* Resultados semánticos estructurados.

## Validaciones

* Validación HTML en formularios.
* Validación fuerte delegada al backend.
* Interceptor Axios para manejo central de errores HTTP.

## Dependencias internas

* `App.tsx`
* `AppLayout.tsx`
* `src/services/*.ts`
* `SemanticChat.tsx`

## Dependencias externas

* React `18.3.1`
* TypeScript `5.8.3`
* Vite `6.3.5`
* Axios `1.13.6`
* React Router DOM `7.3.0`
* Tailwind CSS `3.4.17`

## Runtime recomendado

* Node.js `20+`
* npm `10+`

## Proxy de desarrollo

```
/api/pacientes    -> http://localhost:8083/pacientes
/api/medicos      -> http://localhost:8080/medicos
/api/citas        -> http://localhost:8081/citas
/api/diagnosticos -> http://localhost:8082/diagnosticos
/api/v1/semantic  -> http://localhost:8084/api/v1/semantic
```

## Ejemplo de consumo del servicio semántico

```ts
import { semanticService } from '@/services/semantic.service';

const resultados = await semanticService.buscar('citas de hoy');
console.log(resultados);
```

{% hint style="info" %}
La consistencia de enums depende de contratos backend. El proxy de Vite aplica solo en desarrollo local.
{% endhint %}
