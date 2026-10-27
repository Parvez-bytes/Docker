# 05 — Docker Troubleshooting 🐳

## 1. What Is Docker Troubleshooting?

Docker troubleshooting means investigating problems in containers and applications to understand why they are not working correctly.

Docker provides commands to view logs and execute commands inside a running container.

## 2. View Container Logs — `docker logs`

The `docker logs` command displays the output produced by a container's main process. It helps us investigate application errors and understand what happened.

**Syntax:**

```bash
docker logs CONTAINER_NAME
```

**Example:**

```bash
docker logs my-web
```

Here, `my-web` is the container name.

To follow new log output continuously:

```bash
docker logs -f my-web
```

Use `Ctrl + C` to stop following the logs.

## 3. Enter a Running Container — `docker exec`

The `docker exec` command lets us execute a command inside an already-running container.

**Using Bash:**

```bash
docker exec -it my-web bash
```

**Using Shell (`sh`):**

```bash
docker exec -it my-web sh
```

- `exec` executes a command inside an existing container.
- `-i` keeps standard input open.
- `-t` provides a terminal.
- `bash` or `sh` opens a shell, if available in the image.

**Note:** Some lightweight images do not include Bash, so `sh` may be needed. Nginx images commonly provide `sh`.

## 4. Check Container Status

Before troubleshooting, check whether the container is running.

```bash
docker ps
```

This lists running containers.

```bash
docker ps -a
```

This lists all containers, including stopped ones.

If a container has stopped, inspect its logs:

```bash
docker logs CONTAINER_NAME
```

## 5. Important Points

1. `docker logs` displays the container's main-process output.
2. `docker logs -f` follows new log output.
3. `docker exec` runs a command inside an existing running container.
4. `-it` is commonly used when opening an interactive shell.
5. Use `bash` or `sh` depending on which shell the image provides.
6. `docker ps` lists running containers.
7. `docker ps -a` includes stopped containers.
