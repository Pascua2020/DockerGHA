##### Hashtags #️⃣ : #devops #docker #linux #automation #ci #github-actions #dokku #java-springboot #nginx #####

##### README en Español.To read the English versión,go to README-English.md

## ✅️ **DockerGHA** 

![DevOps Logo](https://globalittrainers.com/wp-content/uploads/2021/06/Devops-logo1.png)

( Docker, GitHub Actions, Java Spring Boot y Dokku )

![Build Status](https://github.com/Pascua2020/DockerGHA/actions/workflows/main.yml/badge.svg)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Docker](https://img.shields.io/badge/container-Docker-blue?logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI-GitHub%20Actions-blue?logo=githubactions&logoColor=white)
![Dokku](https://img.shields.io/badge/deployment-Dokku-blueviolet?logo=dokku)
![No License](https://img.shields.io/badge/license-None-red)
![Español](https://img.shields.io/badge/idioma-español-red?style=flat-square&logo=google-translate)  

```diff 

- Este proyecto demuestra cómo integrar Docker, GitHub Actions, Java Spring Boot y Dokku para crear un flujo de trabajo de desarrollo y despliegue automatizado. 

- La aplicación es un servicio básico de Spring Boot que se ejecuta dentro de un contenedor Docker, se automatiza con GitHub Actions y se despliega usando Dokku.

```

## 1️⃣🟥 **Características**

#### ⚡️ *Docker :* 

![Docker Logo](https://dwglogo.com/wp-content/uploads/2017/09/Docker_container_engine_logo.png)

Empaqueta la aplicación Spring Boot en un contenedor para garantizar que se ejecute de la misma manera en cualquier entorno.

#### ⚡️ *GitHub Actions :* 

![GHA Logo](https://miro.medium.com/v2/resize:fit:1075/0*w5Fsp29pbWIUpW7Q.png)

Automatiza el proceso de construcción, prueba y despliegue de la aplicación con cada cambio en el repositorio.

#### ⚡️ *Java Spring Boot :* 

![Java SB Logo](https://miro.medium.com/v2/resize:fit:720/format:webp/1*MvUFlFTbiU40ae1SK69-Jg.png)

Framework backend para el desarrollo de la aplicación web.

#### ⚡️ *Dokku :* 

![Dokku Logo](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6mNvZ4G3tFQpY1qcVDQdWGSVUW5ljKhyUxfgTeFAZUX5r48Xm8M6mMf55h3IkCw1DC3ERygHIWgsvguq1cYntoluBXdW4-7W_Uhw8JHrvQIeW5T1lIGOuk7WTvkP5O-M_XR4J-6W9Gg-vfhG6B-Q6w75EaJ_eHlGvjxcbEGB3_xckw6OnTwxuBWsL-TRQ/s2800/A%20Deep%20Dive%20with%20Dokku.webp)

Plataforma de despliegue similar a Heroku que usa contenedores Docker para gestionar aplicaciones de forma sencilla.

☢️ **Diferencias entre DockerGHA 1 con 2 , 3 y 4 :**

#### ⚙️ *Todos los Dockerfiles son idénticos :*

- Usan la imagen base busybox:latest.

- Copian un script run.sh en el contenedor que imprime la hora actual en la consola en un bucle infinito.

- Configuran el script run.sh como el punto de entrada del contenedor.

#### ⚙️ *Main.yml - Diferencias generales :*

*🔷️ 1. Repositorios :*

- 1 y 2 suben imágenes solo a Docker Hub.

- 3 sube solo a GHCR.

- 4 sube a ambos registries (Docker Hub y GHCR).

*🔷️ 2. Automatización :*

- Repositorios 2, 3 y 4 usan docker/metadata-action para etiquetas automáticas, mientras que el 1 no.

*🔷️ 3. Nombres de imagen :*

- Repositorio 1 tiene un nombre fijo: clockbox:latest.

- Los demás repositorios usan configuraciones dinámicas o específicas.

## 2️⃣🟧 **Estructura del Proyecto**

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

#### 💾 *Dockerfile :* 

Archivo que define cómo crear la imagen Docker para el proyecto Spring Boot.

#### 💾 *main.yml :* 

Archivo de configuración para GitHub Actions que automatiza la construcción, pruebas y despliegue.

#### 💾 *src/ :* 

Contiene el código fuente de la aplicación Spring Boot.

#### 💾 *pom.xml :* 

Archivo de configuración de Maven para las dependencias y construcción del proyecto.

#### 💾 *dokku-deploy.sh :* 

Script que automatiza el proceso de despliegue de la aplicación en un servidor remoto usando Dokku.


## 3️⃣🟨 **Instalación**

#### 🖱 *Requisitos*

ℹ️ *Docker :* 

Necesario para construir y ejecutar la aplicación en contenedores.

ℹ️ *GitHub Actions :* 

Se utiliza para la integración continua y automatización de procesos de despliegue.

ℹ️ *Dokku :* 

Necesitas un servidor remoto con Dokku instalado para gestionar el despliegue.

ℹ️ *Java :* 

Debes tener instalado Java y Maven para desarrollar la aplicación de backend con Spring Boot.

## 4️⃣⬜️ **Código**

#### 💡 *Dockerfile*
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


#### 💡 *Main.yml*
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

##### 📀 *1. Trigger (Disparador) :*

Se ejecuta automáticamente en un push a la rama main.

##### 📀 *2. Job (build) :*

Se ejecuta en un sistema operativo ubuntu-latest.

##### 📀 *3. Pasos del Job :*

✨️ *Checkout :*

Clona el repositorio en el entorno de GitHub Actions.

✨️ *Login to Docker Hub :*

Inicia sesión en Docker Hub usando las credenciales almacenadas en los secretos (DOCKERHUB_USERNAME y DOCKERHUB_TOKEN).

✨️ *Set up Docker Buildx :*

Configura Docker Buildx, que permite construir imágenes multiplataforma.

✨️ *Build and push :*

Construye la imagen de Docker definida en Dockerfile y la sube a Docker Hub con la etiqueta clockbox:latest.

### 🔑 Propósito :

Automatizar la creación y despliegue de imágenes Docker en Docker Hub para mantenerlas actualizadas con los cambios en la rama principal del repositorio.

## 5️⃣🟦 **Estado del Proyecto**

    ☑️ Terminado.

## 6️⃣👤 **Colaboración**

Este proyecto es de uso personal y no está abierto a colaboraciones externas.  
Sin embargo, si encuentras algo interesante o tienes alguna pregunta, ¡estaré encantado de escuchar! Puedes contactarme en mi perfil de Github.

## 7️⃣🟪 **Licencia**

Este proyecto no tiene licencia asignada. Al no contar con una licencia explícita, se considera que todos los derechos están reservados. Si deseas usar este proyecto, por favor, contáctame.

## 8️⃣🟫 **Autores**

- Pascua2020 (https://github.com/Pascua2020)
- UTN

## 9️⃣📒**Documentación Oficial:**

*Docker :*
https://docs.docker.com

*Github Actions :*
https://docs.github.com/es/actions

*Dokku :*
https://dokku.com/docs/getting-started/installation/

## 🔟🔄 **Notas**

🍪 *Consideraciones de seguridad*
- Este proyecto utiliza variables secretas (`DOCKER_USERNAME`, `DOCKER_PASSWORD`, `GITHUB_TOKEN`).  
- Asegúrate de configurar los secretos en la sección "Settings > Secrets and Variables > Actions" de tu repositorio.

🍪 *Límites del proyecto*
- Este proyecto no incluye configuraciones avanzadas de orquestación como Kubernetes.  
- Está diseñado para despliegues simples en entornos compatibles con Docker.

🍪 *Notas adicionales*
- Este proyecto es un ejemplo educativo. No se recomienda utilizarlo en entornos de producción sin realizar ajustes específicos.