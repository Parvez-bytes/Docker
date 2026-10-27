# 07 — Docker Networking 🐳

## 1. What Is Docker Networking?

Docker networking allows containers to communicate with one another and with external networks.

**Example:** A web application container needs to communicate with a database container. Docker networking allows them to communicate when they are connected to a suitable network.

## 2. Types of Docker Networks

### A. Bridge Network

- The default network driver for standalone containers.
- Containers on the same user-defined bridge network can communicate with each other.
- It is commonly used for applications running in separate containers on one Docker host.

**Create a network:**

```bash
docker network create my-network
```

**Run containers on that network:**

```bash
docker run -dit --name container1 --network my-network ubuntu
docker run -dit --name container2 --network my-network ubuntu
```

The containers can communicate using container names, provided the relevant services are running and listening.

### B. Host Network

- The container shares the host's network namespace.
- It does not use a separate container network namespace in the usual way.
- Port publishing with `-p` is generally unnecessary and ignored in host network mode.

**Example:**

```bash
docker run --network host nginx
```

*Note: Host networking behaves differently across operating systems. On Docker Desktop, support and behavior depend on the version and configuration.*

### C. None Network

- Disables normal external container networking.
- The container has no ordinary external network connectivity, apart from its loopback interface.

**Example:**

```bash
docker run --network none -dit --name isolated ubuntu
```

## 3. Container Communication Diagram

```text
┌────────────────────────────────────┐
│            Docker Host             │
│                                    │
│  ┌──────────────────────────────┐  │
│  │       User-Defined Bridge    │  │
│  │                              │  │
│  │  ┌──────────┐  ┌──────────┐  │  │
│  │  │ Web App  │  │ Database │  │  │
│  │  │Container │  │Container │  │  │
│  │  └──────────┘  └──────────┘  │  │
│  │         ↔ Communication      │  │
│  └──────────────────────────────┘  │
└────────────────────────────────────┘
```

## 4. Useful Networking Commands

| Command | Purpose |
|---|---|
| `docker network ls` | Lists Docker networks |
| `docker network create my-network` | Creates a network |
| `docker network inspect my-network` | Displays network details |
| `docker network connect my-network CONTAINER` | Connects a container to a network |
| `docker network disconnect my-network CONTAINER` | Disconnects a container from a network |
| `docker network rm my-network` | Removes a network when it is no longer in use |

## 5. Important Points

1. Docker networking enables communication between containers.
2. Bridge is the default network driver for standalone containers.
3. User-defined bridge networks support communication using container names.
4. Host networking shares the host's network namespace.
5. The none network driver disables normal external networking.
6. Containers must be connected to a suitable network to communicate over that network.
7. Port mapping (`-p`) and Docker networking are related but serve different purposes.

## Conclusion

Docker networking connects containers and enables communication between applications and services. Bridge, host, and none are three important network drivers.
