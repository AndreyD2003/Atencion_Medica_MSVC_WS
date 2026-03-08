---
description: Recorridos funcionales más importantes del sistema.
icon: list-check
---

# Casos de uso principales

## 1. Registrar un paciente

### Qué interviene

* Frontend
* `msvc-paciente`
* PostgreSQL

### Qué ocurre

1. Se envía un formulario con datos personales.
2. El backend valida campos obligatorios, DNI, teléfono y email.
3. El paciente queda disponible para agenda e historial.

## 2. Registrar un médico

### Qué interviene

* Frontend
* `msvc-medico`
* MySQL

### Qué ocurre

1. Se registra identidad y especialidad.
2. El backend valida formato y unicidad de datos.
3. El médico queda disponible para programar citas.

## 3. Crear una cita

### Qué interviene

* Frontend
* `msvc-cita`
* `msvc-paciente`
* `msvc-medico`
* `msvc-web-semantica`
* Fuseki

### Qué ocurre

1. Se envía fecha, hora, motivo, paciente y médico.
2. `msvc-cita` valida existencia y estado de paciente y médico.
3. `msvc-cita` valida solapes.
4. Si la cita se guarda, se sincroniza la capa semántica.

## 4. Registrar un diagnóstico

### Qué interviene

* Frontend
* `msvc-diagnostico`
* `msvc-cita`
* `msvc-paciente`
* `msvc-web-semantica`
* Fuseki

### Qué ocurre

1. Se registra descripción, tipo, fecha, cita y paciente.
2. Se validan referencias remotas cuando aplica.
3. El diagnóstico se sincroniza hacia el grafo.

## 5. Consultar conocimiento semántico

### Qué interviene

* Frontend
* `msvc-web-semantica`
* QueryParser
* SparqlBuilder
* Fuseki

### Qué ocurre

1. El usuario escribe lenguaje natural o SPARQL.
2. El servicio interpreta la intención o ejecuta la consulta directa.
3. Se devuelven resultados estructurados.

## Qué muestran estos casos

* La operación diaria vive en la capa transaccional.
* La exploración avanzada vive en la capa semántica.
* `msvc-cita` conecta la mayor parte del dominio clínico.
* El frontend concentra la experiencia de uso.
