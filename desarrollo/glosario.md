---
description: Términos clave usados en el proyecto.
icon: book
---

# Glosario

* **JWT:** token JSON Web firmado. Se menciona como concepto histórico. No se usa en la versión actual.
* **Feign:** cliente HTTP declarativo para invocar endpoints de otros microservicios.
* **Propiedad:** regla de negocio que limita acceso o modificación a dueños del recurso.
* **Solape:** intersección de rangos de horas en citas. Es inválido para médico y paciente.
* **EstadoCita:** `PROGRAMADA`, `CANCELADA`, `REALIZADA`.
* **Soft delete:** desactivar en lugar de borrar. En diagnósticos se usa `activo=true`.
* **@PreAuthorize:** anotación de Spring para verificar roles o authorities. Se menciona como concepto histórico. No se aplica en la versión actual.
* **Repositorio:** capa de acceso a datos con consultas JPA o HQL.
* **DTO:** objeto de transferencia para solicitudes o respuestas. Evita exponer el modelo completo.
* **Auditoría:** registro de cambios y actores. Se recomienda para futuras migraciones.
