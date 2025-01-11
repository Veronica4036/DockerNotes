# Docker Basics: Essential Commands and Best Practices

## Introduction

Docker is a platform for developing, shipping, and running applications in containers. This guide covers essential Docker commands, best practices, and common pitfalls to help you effectively work with Docker containers and images, with detailed explanations for beginners.

## Table of Contents

1. [Basic Docker Commands](#basic-docker-commands)
2. [Working with Containers](#working-with-containers)
3. [Dockerfile Best Practices](#dockerfile-best-practices)
4. [Security Considerations](#security-considerations)
5. [Common Pitfalls](#common-pitfalls)
6. [Further Reading](#further-reading)

## Basic Docker Commands

### Listing Containers

```bash
docker ps -a
```

- `docker ps`: Lists running containers.
- `-a`: Shows all containers, including stopped ones.
- Without `-a`, you'd only see currently running containers.

### Executing Commands in Containers

```bash
docker exec <container_name> <command>
```

- Runs a command inside a running container.
- `<container_name>`: The name or ID of your container.
- `<command>`: The command you want to run inside the container.

Example:
```bash
docker exec my_container ls -l /app
```
This runs `ls -l /app` inside a container named `my_container`, listing the contents of the `/app` directory.

### Removing Containers

```bash
docker rm <container_name> --force
```

- Removes a container.
- `<container_name>`: The name or ID of the container to remove.
- `--force`: Stops the container if it's running, then removes it.

### Running Containers

```bash
docker run --name=<name> <image_name> <command>
```

- Creates and starts a new container from an image.
- `--name=<name>`: Assigns a name to the new container.
- `<image_name>`: The name of the Docker image to use.
- `<command>`: (Optional) A command to run in the container.

Example:
```bash
docker run --name my_nginx -d nginx:alpine
```
Creates a container named `my_nginx` from the `nginx:alpine` image, running in detached mode (`-d`).

### Sharing PID Namespace

```bash
docker run --name app2 --pid=container:app1 -d nginx:alpine sleep infinity
```

- Runs a new container that shares the Process ID (PID) namespace with another container.
- `--name app2`: Names the new container `app2`.
- `--pid=container:app1`: Shares the PID namespace with a container named `app1`.
- `-d`: Runs in detached mode.
- `nginx:alpine`: The image to use.
- `sleep infinity`: A command to keep the container running indefinitely.

### Run an instance of the image webapp-color and publish port 8080 on the container to 8282 on the host.

```bash
docker run -p 8282:8080 webapp-color
```

- Runs a new container from the webapp-color image.
- `-p 8282:8080`: Maps port 8080 from the container to port 8282 on the host.
- The format is `-p <host_port>:<container_port>`.
- The container will be accessible from the host machine on port 8282.

### Inspecting Images

```bash
docker inspect <image>
```

- Provides detailed information about a Docker image.
- `<image>`: The name or ID of the image you want to inspect.

## Working with Containers

### Building Images

```bash
docker build -t <image_name> <path_to_dockerfile>
```

- Builds a Docker image from a Dockerfile.
- `-t <image_name>`: Tags the image with a name.
- `<path_to_dockerfile>`: The directory containing the Dockerfile.

Example:
```bash
docker build -t my_app:v1 .
```
Builds an image named `my_app` with tag `v1` using the Dockerfile in the current directory.

### Running Containers with Environment Variables

```bash
docker run -e VAR_NAME=value -d <image_name>
```

- Runs a container with environment variables.
- `-e VAR_NAME=value`: Sets an environment variable inside the container.
- `-d`: Runs in detached mode.
- `<image_name>`: The image to use for the container.

### Accessing Container Logs

```bash
docker logs <container_name>
```

- Displays the logs of a running container.
- `<container_name>`: The name or ID of the container.
## Further Reading

1. [Docker Documentation](https://docs.docker.com/)
2. [Docker Security Best Practices](https://snyk.io/blog/10-docker-image-security-best-practices/)
3. [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
4. [Docker Networking Guide](https://docs.docker.com/network/)
5. [Docker Compose for Multi-Container Applications](https://docs.docker.com/compose/)

This comprehensive guide covers the basics of Docker, including essential commands with detailed explanations, best practices for writing Dockerfiles, security considerations, and common pitfalls to avoid. By following these guidelines, you can create more efficient, secure, and maintainable Docker-based applications, even as a beginner to Docker.
