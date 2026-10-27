# 04 — Port Binding 🐳

## 1. What Is Port Binding?

Port binding, also called port mapping, allows us to access a service running inside a Docker container through a port on the host machine.

- **Host:** Your laptop or computer.
- **Container:** The isolated environment running the application.
- **Container port:** The port on which the application listens inside the container.
- **Host port:** The port exposed on your computer.

By default, a container's service ports are not automatically published to the host.

## 2. Syntax

```bash
docker run -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
```

The `-p` option publishes a container port on a host port.

## 3. Example Using Nginx

```bash
docker run -d --name my-web -p 8080:80 nginx
```

Here:

- `-d` runs the container in the background.
- `--name my-web` gives the container a custom name.
- `-p 8080:80` maps host port `8080` to container port `80`.
- `nginx` is the image used to create the container.

**How it works:**

```text
┌─────────────────────────────┐
│        Your Laptop          │
│                             │
│  Browser: localhost:8080    │
│             │               │
│             ▼               │
│      Host Port 8080         │
└─────────────┬───────────────┘
              │ Port Mapping
              ▼
┌─────────────────────────────┐
│       Docker Container      │
│                             │
│        Nginx: Port 80       │
└─────────────────────────────┘
```

Open `http://localhost:8080` in your browser to see the Nginx welcome page.

## 4. Different Host Ports, Same Container Port

Multiple containers can use the same internal port while publishing it through different host ports.

```bash
docker run -d --name web1 -p 8080:80 nginx
docker run -d --name web2 -p 8081:80 nginx
```

- `web1` uses host port `8080` and container port `80`.
- `web2` uses host port `8081` and container port `80`.

You can access them at:

- `http://localhost:8080`
- `http://localhost:8081`

The host ports must be available and not already occupied by another service or published container.

## 5. Important Points

1. Port mapping uses the `-p` option.
2. The syntax is `HOST_PORT:CONTAINER_PORT`.
3. The host and container ports can be different.
4. Multiple containers can use the same internal port.
5. Two containers generally cannot publish the same host IP and port combination simultaneously.
6. Port mapping makes a service reachable through the host; the application must also be listening on the container port.
7. You can check published ports using `docker ps`.
