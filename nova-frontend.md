# nova frontend

## Propósito y responsabilidad

Entrega la interfaz web de operación clínica y consumo de capacidades semánticas del backend.

## Rutas funcionales

| Ruta            | Responsabilidad             |
| --------------- | --------------------------- |
| `/`             | Dashboard general           |
| `/pacientes`    | Gestión de pacientes        |
| `/medicos`      | Gestión de médicos          |
| `/citas`        | Gestión de citas            |
| `/diagnosticos` | Gestión de diagnósticos     |
| `/semantic`     | Chat y consultas semánticas |

## Entradas, salidas y validaciones

### Entradas principales

* Formularios de alta/edición para paciente, médico, cita y diagnóstico.
* Texto libre para búsqueda semántica.
* Query SPARQL manual para administración.

### Salidas principales

* Tablas y listados por dominio.
* Mensajes de éxito/error por operación.
* Resultados semánticos estructurados (`SparqlResult[]`).

### Validaciones

* Validación HTML en formularios (`required`, tipos de campo).
* Validación fuerte delegada al backend.
* Interceptor Axios para manejo central de errores HTTP.

## Dependencias

### Internas

* `App.tsx` (enrutamiento)
* `AppLayout.tsx` (layout)
* `src/services/*.ts` (cliente API por módulo)
* `SemanticChat.tsx` (interacción semántica)

### Externas

* React 18.3.1
* TypeScript 5.8.3
* Vite 6.3.5
* Axios 1.13.6
* React Router DOM 7.3.0
* Tailwind CSS 3.4.17

### Versiones relevantes de runtime

* Node.js: `20+` recomendado
* npm: `10+` recomendado

## Ejemplo de implementación funcional

### Consumo del endpoint semántico desde frontend

```ts
import { semanticService } from '@/services/semantic.service';

const resultados = await semanticService.buscar('citas de hoy');
console.log(resultados);
```

### Proxy de desarrollo (Vite)

```
/api/pacientes    -> http://localhost:8083/pacientes
/api/medicos      -> http://localhost:8080/medicos
/api/citas        -> http://localhost:8081/citas
/api/diagnosticos -> http://localhost:8082/diagnosticos
/api/v1/semantic  -> http://localhost:8084/api/v1/semantic
```

## Casos de uso reales

* Operación diaria de agenda médica.
* Registro y consulta de diagnósticos.
* Exploración de conocimiento clínico sin escribir SPARQL.

## Consideraciones importantes

* La consistencia de enums depende de contratos backend.
* El proxy Vite aplica solo en desarrollo local.
* Debe mantenerse alineación entre sugerencias de chat y capacidades de `QueryParser`.

## Referencias cruzadas

* [msvc-web-semantica](/broken/pages/d81bb281e79814d86cfe60da521efb84dc68e6ea)
* [Consulta semántica](/broken/pages/e978f473fec2979725627041eeab2cb4cb313288)
* [Estructura de código](/broken/pages/79c7abd49a828d4c5dbe23c463c41a25f1b1d850)
