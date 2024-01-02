# Easy Docker

`Easy Docker` is a repository of Dockerfiles, Docker Compose scripts, and other Docker resources, aimed at simplifying the deployment and management of popular applications and services.

## Table of Contents

1. [Getting Started](#getting-started)
   1. [Understanding Docker](#understanding-docker)
   2. [Docker Terminology](#docker-terminology)
2. [Dockerfile](#dockerfile)
   1. [Understanding Dockerfile](#understanding-dockerfile)
   2. [Dockerfile Instructions](#dockerfile-instructions)
   3. [Dockerfile Examples](#dockerfile-examples)
3. [Docker Compose](#docker-compose)
4. [Contributing](#contributing)
5. [License](#license)

<a id="getting-started"></a>

## 1. Getting Started

<a id="understanding-docker"></a>

### 1.1. Understanding Docker

- Facilitates consistent development, testing, and deployment environments, ensuring that the software behaves the same way in every stage.
- Supports a microservices architecture, allowing each service to be packaged into a separate container.
- Provides version control for containers, making it easy to roll back to a previous version if needed.
- Offers a vast repository of pre-built images for various software, reducing the setup time.
- Enhances resource utilization as containers are lightweight and start quickly compared to traditional virtual machines.

<a id="docker-terminology"></a>

### 1.2. Docker Terminology
<details>
  <summary>Click me</summary>

| Term              | Description                                                                                                                                                         |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Docker Registry   | A storage system for Docker images that hosts and manages them, facilitating their sharing and distribution.                                                        |
| Docker Repository | A collection of Docker images that are related, identified by a common name, and differentiated by their versions.                                                  |
| Docker Images     | Self-contained packages that include everything necessary to run applications.                                                                                      |
| Docker Container  | Lightweight, runnable instances of Docker images.                                                                                                                   |
| Dockerfile        | A text file that contains all the commands or instructions needed to build a Docker image.                                                                          |
| Docker Compose    | A tool for defining and running multi-container Docker applications. It uses YAML files to configure application's services.                                        |
| Docker Swarm      | A native clustering and scheduling tool for Docker containers. It turns a pool of Docker hosts into a single, virtual host.                                         |
| Docker Hub        | A cloud-based registry service for building and shipping application or service containers. It provides a centralized resource for container image discovery.       |
| Docker Engine     | The runtime that runs and manages containers on a host machine. It's the core of Docker and it consists of a server, a REST API and a command line interface (CLI). |
| Docker Volume     | Provides persistent storage for Docker containers, managing data beyond the container's lifecycle and enabling data persistence.                                    |
| Docker Network    | Enables communication among Docker containers and between containers and the host, providing networking and connectivity.                                           |
</details>

<a id="dockerfile"></a>

## 2. Dockerfile

<a id="understanding-dockerfile"></a>

### 2.1. Understanding Dockerfile

A Dockerfile is a text file that contains all the commands or instructions needed to build a Docker image. It is a simple way to automate the image creation process. Docker reads the Dockerfile and executes the instructions in it to build a Docker image.

<a id="dockerfile-instructions"></a>

### 2.2. Dockerfile Instructions
<details>
  <summary>Click me</summary>
  
| Instruction      | Description                                                                                                                               |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| FROM             | Specifies the base image for the Docker image                                                                                             |
| WORKDIR          | Defines the working directory for the following Dockerfile instructions                                                                   |
| COPY / ADD       | Transfers files and directories from the host machine to the Docker image. ADD supports URLs and automatic decompression of files         |
| ENV              | Establishes environment variables within the Docker image                                                                                 |
| RUN              | Runs commands during the Docker image build process                                                                                       |
| EXPOSE           | Indicates the ports the container listens on                                                                                              |
| ENTRYPOINT / CMD | Sets the default command for a container. CMD can be overridden at runtime, ENTRYPOINT cannot                                             |
| ARG              | Defines a variable that users can pass at build-time to the builder with the docker build command                                         |
| USER             | Sets the user name or UID to use when running the image and for any RUN, CMD and ENTRYPOINT instructions that follow it in the Dockerfile |
| VOLUME           | Creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers     |
</details>

<a id="dockerfile-examples"></a>

### 2.3. Dockerfile Examples

- [Dockerize static application (React, Angular, Vue + Nginx)](/Dockerfile/with-react-angular-vue/README.md)
- [Dockerize Next.js application](/Dockerfile/with-nextjs/README.md)

<a id="docker-compose"></a>

## 3. Docker Compose (Coming Soon)

<a id="contributing"></a>

## 4. Contributing

Contributions are welcome! Please read [full text](/.github/CONTRIBUTING.md) for more information.

<a id="license"></a>

## 5. License

This project is open and does not have a specific license. You may use this project as you wish.
