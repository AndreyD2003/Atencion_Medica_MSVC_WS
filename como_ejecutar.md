# COMO\_EJECUTAR

{% stepper %}
{% step %}
### Ejecutar todos los msvc

Ejecuta primero todos los msvc necesarios.
{% endstep %}

{% step %}
### Acceder a la carpeta de Fuseki

Ingresa a la carpeta del servidor Fuseki:

```bash
cd msvc-web-semantica\target\apache-jena-fuseki-6.0.0
```
{% endstep %}

{% step %}
### Ejecutar el .jar de Fuseki

Inicia el servidor Fuseki:

```bash
java -jar .\fuseki-server.jar
```
{% endstep %}

{% step %}
### Abrir la interfaz web de Fuseki

Abre en el navegador:

```
http://localhost:3030/
```
{% endstep %}

{% step %}
### Crear el dataset

En la interfaz web crea un nuevo dataset (New dataset):

* Dataset name: `atencion_medica`
* Dataset type: `Persistent (TDB2) – dataset will persist across Fuseki restarts`
{% endstep %}

{% step %}
### Subir el archivo .ttl

*   Selecciona el archivo .ttl (atencion-medica.ttl):

    [atencion-medica.ttl](/broken/pages/457c2fcd10b86bec699ce710e4ebf100fad7fc76)
* En la columna actions seleccionar `upload now`.
{% endstep %}

{% step %}
### Ejecutar el Frontend — entrar a la carpeta

En un terminal ingresa a la carpeta del frontend:

```bash
cd nova-frontend
```
{% endstep %}

{% step %}
### Ejecutar el frontend

Inicia el frontend:

```bash
npm run dev
```

Si hay errores con el frontend, primero ejecutar:

```bash
npm run build
```

y luego:

```bash
npm run dev
```
{% endstep %}
{% endstepper %}

¡GRACIAS!
