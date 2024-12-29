Hashtags #️⃣ : #devops #docker #linux #automation #ci #github-actions #dokku #java-springboot #nginx

# ✅️ DockerGHA


![Build Status](https://github.com/Pascua2020/DockerGHA/actions/workflows/main.yml/badge.svg)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Docker](https://img.shields.io/badge/container-Docker-blue?logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/CI-GitHub%20Actions-blue?logo=githubactions&logoColor=white)
![Dokku](https://img.shields.io/badge/deployment-Dokku-blueviolet?logo=dokku)
![No License](https://img.shields.io/badge/license-None-red)

( Docker, GitHub Actions, Java Spring Boot, and Dokku )

![DevOps Logo](https://globalittrainers.com/wp-content/uploads/2021/06/Devops-logo1.png)

```diff
- This project demonstrates how to integrate Docker, GitHub Actions, Java Spring Boot, and Dokku to create an automated development and deployment workflow.

- The application is a basic Spring Boot service running inside a Docker container, automated with GitHub Actions, and deployed using Dokku.
```

## 1️⃣🟥 Features

*⚡️ Docker:*

Packages the Spring Boot application in a container to ensure it runs consistently in any environment.

*⚡️ GitHub Actions:*

Automates the build, test, and deployment processes for the application with each change in the repository.

*⚡️ Java Spring Boot:*

Backend framework for web application development.

*⚡️ Dokku:*

A Heroku-like deployment platform that uses Docker containers to manage applications easily.

### Differences between DockerGHA 1, 2, 3, and 4:

*All Dockerfiles are identical:*

- Use the base image busybox:latest.

- Copy a run.sh script into the container, which prints the current time in the console in an infinite loop.

- Configure the run.sh script as the container's entry point.


*Main.yml - General differences:*

1. Repositories:


- 1 and 2 push images only to Docker Hub.

- 3 pushes only to GHCR.

- 4 pushes to both registries (Docker Hub and GHCR).


2. Automation:

- Repositories 2, 3, and 4 use docker/metadata-action for automatic tagging, while 1 does not.


3. Image names:

- Repository 1 has a fixed name: clockbox:latest.

- The other repositories use dynamic or specific configurations.


## 2️⃣🟧 Project Structure
```
DockerGHA/
│
├── .github/
│   └── workflows/
│       └── main.yml             # GitHub Actions workflow
├── Dockerfile                   # Dockerfile for containerizing the app
├── README.md                    # Project documentation
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └──  DominioApplication.java   # Spring Boot main class
│   │   └── resources/
│   │       └── application.properties         # App configuration
├── target/                       # Build directory (generated by Maven/Gradle)
├── pom.xml                       # Maven configuration file (if using Maven)
└── .gitignore                    # Files and directories to ignore in Git
```
*💾 Dockerfile:*

Defines how to build the Docker image for the Spring Boot project.

*💾 main.yml:*

GitHub Actions configuration file to automate building, testing, and deployment.

*💾 src/:*

Contains the source code for the Spring Boot application.

*💾 pom.xml:*

Maven configuration file for dependencies and project build.

*💾 dokku-deploy.sh:*

Script that automates the deployment process of the application to a remote server using Dokku.

## 3️⃣🟩 Objectives of the Project

The purpose of this repository is to demonstrate the use of Docker, GitHub Actions, and Dokku in a unified DevOps workflow for building, testing, and deploying applications.

This workflow is highly modular and follows standard practices to ensure scalability and automation:

Containerize the application using Docker.

Implement CI/CD pipelines using GitHub Actions.

Automate deployment processes via Dokku.

## 4️⃣🟨 Technologies Used

*Backend:*

💡Java Spring Boot: Provides a framework for developing microservices and REST APIs.

*Containers:*

💡Docker: Used to create, deploy, and run the application in containers, ensuring consistency across environments.

*Automation:*

💡GitHub Actions: Configured to automate the build, test, and deployment processes.

*Deployment:*

💡Dokku: Used to manage and deploy the application to a virtualized environment, simplifying application hosting.

*Others:*

💡Nginx: Used as a reverse proxy for the application to enhance performance and security.

## 5️⃣🟦 Project Status

☑️ Completed.

## 6️⃣👤 Collaboration

This project is for personal use and is not open to external contributions.
However, if you find it interesting or have any questions, I’ll be happy to hear them! Feel free to contact me on my GitHub profile.

## 7️⃣🟪 License

This project does not have an assigned license. Without an explicit license, all rights are reserved. If you wish to use this project, please contact me.

## 8️⃣🟫 Authors

-Pascua2020 (https://github.com/Pascua2020)

-UTN


## 9️⃣📒 Official Documentation:

-Docker:
https://docs.docker.com

-GitHub Actions:
https://docs.github.com/en/actions

-Dokku:
https://dokku.com/docs/getting-started/installation/

## 🔟🔄 Notes

Security Considerations

-This project uses secret variables (DOCKER_USERNAME, DOCKER_PASSWORD, GITHUB_TOKEN).

-Make sure to configure the secrets in the "Settings > Secrets and Variables > Actions" section of your repository.


Project Limitations

-This project does not include advanced orchestration setups like Kubernetes.

-It is designed for simple deployments in Docker-compatible environments.


Additional Notes

-This project is an educational example. 

-It is not recommended for use in production environments without making specific adjustments.