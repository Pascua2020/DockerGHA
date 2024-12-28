✅️ DockerGHA ( Docker, GitHub Actions, Java Spring Boot y Dokku )

Este proyecto demuestra cómo integrar Docker, GitHub Actions, Java Spring Boot y Dokku para crear un flujo de trabajo de desarrollo y despliegue automatizado. La aplicación es un servicio básico de Spring Boot que se ejecuta dentro de un contenedor Docker, se automatiza con GitHub Actions y se despliega usando Dokku.

🟥 Características

⚡️Docker: Empaqueta la aplicación Spring Boot en un contenedor para garantizar que se ejecute de la misma manera en cualquier entorno.

⚡️GitHub Actions: Automatiza el proceso de construcción, prueba y despliegue de la aplicación con cada cambio en el repositorio.

⚡️Java Spring Boot: Framework backend para el desarrollo de la aplicación web.

⚡️Dokku: Plataforma de despliegue similar a Heroku que usa contenedores Docker para gestionar aplicaciones de forma sencilla.


🟧 Estructura del Proyecto

```
DockerGHA/
│
├── .github/
│   └── workflows/
│       └── main.yml             # Flujo de trabajo de GitHub Actions
├── Dockerfile                   # Dockerfile para contenerizar la app
├── README.md                    # Documentación del proyecto
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └──  DominioApplication.java   # Clase principal de Spring Boot
│   │   └── resources/
│   │       └── application.properties         # Configuración de la app
├── target/                       # Directorio de build (generado por Maven/Gradle)
├── pom.xml                       # Archivo de configuración de Maven (si usas Maven)
└── .gitignore                    # Archivos y directorios que Git debe ignorar
```

💾Dockerfile: Archivo que define cómo crear la imagen Docker para el proyecto Spring Boot.

💾main.yml: Archivo de configuración para GitHub Actions que automatiza la construcción, pruebas y despliegue.

💾src/: Contiene el código fuente de la aplicación Spring Boot.

💾pom.xml: Archivo de configuración de Maven para las dependencias y construcción del proyecto.

💾dokku-deploy.sh: Script que automatiza el proceso de despliegue de la aplicación en un servidor remoto usando Dokku.


🟨 Instalación

Requisitos

Docker: Necesario para construir y ejecutar la aplicación en contenedores.

GitHub Actions: Se utiliza para la integración continua y automatización de procesos de despliegue.

Dokku: Necesitas un servidor remoto con Dokku instalado para gestionar el despliegue.

Java: Debes tener instalado Java y Maven para desarrollar la aplicación de backend con Spring Boot.

⬜️ Código

Dockerfile
```
# syntax=docker/dockerfile:1
FROM busybox:latest
COPY --chmod=755 <<EOF /app/run.sh
#!/bin/sh
while true; do
  echo -ne "The time is now $(date +%T)\\r"
  sleep 1
done
EOF

ENTRYPOINT /app/run.sh
```

Este Dockerfile crea una imagen basada en busybox que ejecuta un script en un bucle infinito. El script imprime continuamente la hora actual en formato HH:MM:SS, actualizándola en la misma línea cada segundo.

Usa la imagen base minimalista busybox:latest.

Copia un script (run.sh) al contenedor con permisos de ejecución (chmod=755).

Configura el script como el punto de entrada (ENTRYPOINT).


Main.yml
```
name: ci

on:
  push:
    branches:
      - "main"

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      -
        name: Checkout
        uses: actions/checkout@v4
      -
        name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      -
        name: Build and push
        uses: docker/build-push-action@v5
        with:
          context: .
          file: ./Dockerfile
          push: true
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/clockbox:latest
```
Este archivo main.yml configura un flujo de integración continua (CI) en GitHub Actions para construir y publicar una imagen de Docker en Docker Hub cada vez que se hace un push a la rama main.

1. Trigger (Disparador):

Se ejecuta automáticamente en un push a la rama main.

2. Job (build):

Se ejecuta en un sistema operativo ubuntu-latest.

3. Pasos del Job:

Checkout: Clona el repositorio en el entorno de GitHub Actions.

Login to Docker Hub: Inicia sesión en Docker Hub usando las credenciales almacenadas en los secretos (DOCKERHUB_USERNAME y DOCKERHUB_TOKEN).

Set up Docker Buildx: Configura Docker Buildx, que permite construir imágenes multiplataforma.

Build and push: Construye la imagen de Docker definida en Dockerfile y la sube a Docker Hub con la etiqueta clockbox:latest.

Propósito:

Automatizar la creación y despliegue de imágenes Docker en Docker Hub para mantenerlas actualizadas con los cambios en la rama principal del repositorio.

🟦 Estado del Proyecto

    ☑️ Terminado.

🟪 Licencia  

Este proyecto no tiene licencia asignada. Al no contar con una licencia explícita, se considera que todos los derechos están reservados. Si deseas usar este proyecto, por favor, contáctame.

🟫 Autores  
- Pascua2020 (https://github.com/Pascua2020)
- UTN