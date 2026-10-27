# 09 — Dockerfile and Dockerizing an Application 🐳

## 1. What Is a Dockerfile?

A Dockerfile is a text file containing instructions used to build a Docker image.

It tells Docker which base image to use, where to place application files, and which command to execute when a container starts.

**Flow:**

```text
Application Files
       ↓
   Dockerfile
       ↓
   Docker Image
       ↓
    Container
```

## 2. Important Dockerfile Instructions

### A. FROM

```dockerfile
FROM node
```

**Meaning:** Specifies the base image used to build our image.

**Explanation:** Since our application uses Node.js, we use the Node.js image, which provides the Node.js runtime and its base environment.

### B. RUN

```dockerfile
RUN mkdir -p testapp
```

**Meaning:** Executes a command while building the Docker image.

**Explanation:**
- `mkdir` creates a directory.
- `-p` creates missing parent directories if necessary.

Creating a separate folder this way is optional because `WORKDIR` can create and select a working directory.

### C. COPY

```dockerfile
COPY . /testapp
```

**Meaning:** Copies files and folders from the build context into the image.

**Explanation:**
- `.` represents the source files in the build context.
- `/testapp` is the destination inside the image's filesystem.

Files excluded through `.dockerignore` are not copied.

### D. WORKDIR

```dockerfile
WORKDIR /app
```

**Meaning:** Sets the working directory inside the image.

Docker creates `/app` if it does not exist. Subsequent instructions use this directory as their working directory unless another directory is specified.

### E. ENV

```dockerfile
ENV MONGO_DB_USERNAME=admin
```

**Meaning:** Sets an environment variable inside the image.

Applications can read environment variables for configuration. However, setting a variable does not automatically connect an application to a database.

**Important:** Avoid hardcoding real passwords or secrets in a Dockerfile.

### F. CMD

```dockerfile
CMD ["node", "server.js"]
```

**Meaning:** Specifies the default command to run when a container starts.

- `node` starts the Node.js runtime.
- `server.js` is the JavaScript file being executed.

`CMD` does not run the application during image building; it specifies the default startup command.

## 3. RUN vs CMD

| RUN | CMD |
|---|---|
| Executes during image building. | Specifies the default command for container startup. |
| Used to install dependencies or create files. | Used to start the application. |
| Example: `RUN npm install` | Example: `CMD ["node", "server.js"]` |

## 4. Understanding the Image Filesystem

When we use `FROM node`, Docker starts with the filesystem provided by the Node.js image.

Examples of directories inside a Linux-based image:

- `/bin` contains system commands.
- `/usr` contains many system files and installed software.
- `/etc` contains configuration files.
- `/app` can contain our application files.

The image filesystem is separate from our Windows project directory. The container's root directory `/` is the top-level directory inside its filesystem, not the Windows `C:\` directory.

## 5. Example Dockerfile

```dockerfile
FROM node
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "server.js"]
```

**Explanation:**

1. `FROM node` selects the Node.js base image.
2. `WORKDIR /app` creates and selects the application directory.
3. `COPY package*.json ./` copies the package files into `/app`.
4. `RUN npm install` installs the dependencies declared in `package.json`.
5. `COPY . .` copies the remaining application files into `/app`.
6. `CMD ["node", "server.js"]` starts the application when the container runs.

**Note:** This example assumes the project has a `package.json` and a `server.js` entry point. The actual startup command depends on your application.

## 6. Build and Run the Application

### Build the image

```bash
docker build -t mynode-app .
```

- `build` builds an image from a Dockerfile.
- `-t mynode-app` assigns a name to the image.
- `.` specifies the build context, usually the current project directory.

### Run a container

```bash
docker run --name myapp mynode-app
```

This creates and starts a container from the `mynode-app` image.

If the application listens on a port, publish the appropriate port using `-p HOST_PORT:CONTAINER_PORT`.

## 7. Important Points

1. A Dockerfile contains instructions for building an image.
2. `FROM` specifies the base image.
3. `RUN` executes commands during image building.
4. `COPY` copies files from the build context into the image.
5. `WORKDIR` sets the working directory.
6. `ENV` defines environment variables.
7. `CMD` specifies the default startup command.
8. `docker build` creates the image.
9. `docker run` creates and starts a container from the image.

## Conclusion

A Dockerfile packages an application's files and required environment into a Docker image. When the image is run, Docker creates a container in which the application can execute.
