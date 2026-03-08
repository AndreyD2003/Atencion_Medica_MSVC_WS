---
description: Pasos para levantar el entorno y preparar Fuseki.
icon: play
---

# Ejecución local

## Secuencia base

1. Ejecuta todos los microservicios.
2. Levanta Fuseki.
3. Crea el dataset.
4. Carga la ontología.
5. Inicia el frontend.

## Levantar Fuseki

### Entrar a la carpeta del servicio

```bash
cd msvc-web-semantica\target\apache-jena-fuseki-6.0.0
```

### Iniciar el servidor

```bash
java -jar .\fuseki-server.jar
```

### Abrir Fuseki

```
http://localhost:3030/
```

## Crear el dataset

Usa estos valores:

* `Dataset name`: `atencion_medica`
* `Dataset type`: `Persistent (TDB2)`

## Cargar el archivo TTL

Sube el archivo `atencion-medica.ttl` al dataset.

En la carga manual:

* Selecciona el archivo `.ttl`.
* En `actions`, usa `upload now`.

## Levantar el frontend

### Entrar a la carpeta

```bash
cd nova-frontend
```

### Iniciar desarrollo

```bash
npm run dev
```

### Si falla el frontend

Ejecuta primero:

```bash
npm run build
```

Luego vuelve a ejecutar:

```bash
npm run dev
```

{% hint style="success" %}
Si Fuseki, el dataset y el frontend están activos, ya puedes probar la parte semántica y la operación clínica.
{% endhint %}
