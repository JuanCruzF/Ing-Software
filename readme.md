# Proyecto - Ingeniería del Software

## Resumen

La aplicación consiste en un único archivo `index.html` que es servido por un contenedor Nginx. El propósito es mostrar el flujo de trabajo básico para construir una imagen de Docker personalizada y ejecutarla.

---

## Prerrequisitos

Para poder construir y ejecutar este proyecto, es necesario tener instalado el siguiente software en el sistema:

* **Git:** Para la clonación del repositorio.
* **Docker Desktop:** Para la gestión de imágenes y contenedores.

---

## Estructura del Proyecto

El repositorio contiene los siguientes archivos en su raíz:

```
/
├── Dockerfile
├── index.html
└── README.md
```

* **`Dockerfile`**: Contiene las instrucciones para que Docker construya la imagen de la aplicación.
* **`index.html`**: Es la página web estática que se mostrará.
* **`README.md`**: Archivo de documentación.

---

## Instrucciones de Ejecución

### Paso 1: Construir la Imagen de Docker

Utilizar el siguiente comando para construir la imagen de Docker a partir del `Dockerfile`. La imagen será etiquetada con el nombre `mi-app-web`.

```bash
docker build -t mi-app-web .
```

### Paso 2: Ejecutar el Contenedor Docker

Con el siguiente comando vamos a iniciar un contenedor basado en esa imagen.

```bash
docker run -d -p 8080:80 mi-app-web
```

**Detalle de los parámetros:**

* `-d`: Ejecuta el contenedor en modo "detached" (en segundo plano).
* `-p 8080:80`: Mapea el puerto 8080 del host al puerto 80 del contenedor, donde Nginx está escuchando.
* `mi-app-web`: Especifica la imagen a utilizar para crear el contenedor.

### Paso 3: Verificación

Para verificar que el contenedor se está ejecutando correctamente, abrí el siguiente enlace:

`http://localhost:8080`

Se deberá visualizar el contenido del archivo `index.html`.

---

## Contenido de los archivos fuente

### `index.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ing. Software</title>
    <style>
        body { 
            background-color: #282c34;
            color: white;
            font-family: Arial, Helvetica, sans-serif; 
            text-align: center; 
            padding-top: 50px; 
            padding-bottom: 50px;
        }
        h1 {
            color: #61dafb;
        }
        p {
            font-size: 1.2rem;
        }
        img {
            max-width: 90%;
            width: 350px;
            height: auto;
            border-radius: 15px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Hola!!</h1>
    <p>No pude entregar la tarea en tiempo y forma.</p>
    <p>Pero lo pude hacer. Disculpas.</p>
    <img src="https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExbGxtNmRhZWZ5Mzh0cGZ6cjgwNXdsbzJtZHlseTB6cHozb25sZWhhaiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xT0BKFyZt9MMx9xkpW/giphy.gif" alt="Animación de la ballena de Docker">
    
</body>
</html>
```

### `Dockerfile`

```dockerfile
# Usar una imagen base oficial de Nginx desde Docker Hub.
# 'stable-alpine' hace referencia al tamaño reducido.
FROM nginx:stable-alpine

# Copiar el archivo local 'index.html' al directorio por defecto de Nginx
# dentro del contenedor, desde donde sirve el contenido estático.
COPY index.html /usr/share/nginx/html

# Exponer el puerto 80, que es el puerto por defecto en el que
# Nginx escucha las conexiones entrantes.
EXPOSE 80
