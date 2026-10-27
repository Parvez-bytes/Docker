# 01 — Docker Basics 🐳

## 1. What is Docker?

Docker is a platform used to build, package, and run applications inside containers.

In simple words, Docker helps an application run consistently on different systems without requiring you to manually configure everything on each machine.

**Example:** If an application works on your laptop, Docker helps package the application and its required environment so it can run on another computer too.

## 2. What is a Docker Image?

A Docker image is a template used to create containers. It contains the application and the filesystem components and dependencies packaged into the image.

**Example:** An image is like a recipe used to prepare a dish.

## 3. What is a Docker Container?

A container is a running instance of a Docker image.

**Example:** If an image is a recipe, the container is the dish prepared using that recipe.

One image can be used to create multiple containers.

## 4. Important Docker Commands

| Command | Purpose |
|---|---|
| `docker --version` | Checks the installed Docker version |
| `docker images` | Lists locally available images |
| `docker ps` | Lists running containers |
| `docker ps -a` | Lists all containers, including stopped ones |
| `docker pull nginx` | Downloads the Nginx image |
| `docker run nginx` | Creates and starts a container from the Nginx image |
| `docker stop CONTAINER_ID` | Stops a running container |
| `docker start CONTAINER_ID` | Starts a stopped container |
| `docker rm CONTAINER_ID` | Removes a container |
| `docker rmi IMAGE_NAME` | Removes an image when it is no longer in use |

Replace `CONTAINER_ID` with the actual container ID or name.

## 5. Image vs Container

- **Image:** The packaged template used to create a container.
- **Container:** The isolated environment created from an image to run an application.

**Remember:** Image = template; container = running instance.
