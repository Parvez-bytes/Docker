# 11 — Docker Volumes 🐳

## 1. What is a Docker Volume?

A Docker volume is used to store data outside a container's writable layer so that the data can persist even if the container is removed.

**Example:** Suppose a MongoDB container stores user records. If the container is removed, data stored only inside its writable layer may be lost. A volume helps preserve that data.

## 2. Why Do We Need Volumes?

1. To preserve data after a container is removed.
2. To store database files.
3. To share persistent data between containers when required.
4. To separate application data from the container's lifecycle.

## 3. Types of Storage

### A. Named Volume

A named volume has a specific name and is managed by Docker.

**Step 1: Create a volume**

```bash
docker volume create mydata
```

**Step 2: Use the volume in a container**

```bash
docker run -it --name myubuntu -v mydata:/app/data ubuntu
```

- `mydata` is the named volume.
- `/app/data` is the directory inside the container.
- `-v` mounts the volume at the specified container path.

The data written to `/app/data` is stored in the volume and can persist after the container is removed.

### B. Anonymous Volume

An anonymous volume is created without specifying a volume name.

```bash
docker run -it -v /app/data ubuntu
```

Docker creates and mounts an anonymous volume at `/app/data`. Its generated name is managed by Docker.

### C. Bind Mount

A bind mount connects a specific directory or file on the host computer to a path inside the container.

```bash
docker run -it -v "/host/data:/app/data" ubuntu
```

- `/host/data` represents a directory on the host computer.
- `/app/data` is the directory inside the container.
- Changes can be shared between the host and container through the mounted directory.

**Note:** Replace `/host/data` with a real path on your computer. The exact path syntax depends on your operating system and terminal.

## 4. Docker Volume Commands

| Command | Purpose |
|---|---|
| `docker volume create mydata` | Creates a named volume |
| `docker volume ls` | Lists volumes |
| `docker volume inspect mydata` | Shows volume details |
| `docker volume rm mydata` | Removes a volume if it is not in use |
| `docker volume prune` | Removes unused anonymous and named volumes, subject to Docker's cleanup rules |

**Important:** Be careful with `docker volume prune` because it can remove volumes containing data you still need.

## 5. Where Is Volume Data Stored?

Docker manages the storage location of volumes.

- On many Linux installations, named volume data is stored under `/var/lib/docker/volumes/`.
- With Docker Desktop on Windows using WSL 2, Docker-managed data is commonly stored inside its Linux environment rather than at a directly accessible Windows folder.

The exact storage location depends on the Docker installation.

## 6. Volume vs Bind Mount

| Named Volume | Bind Mount |
|---|---|
| Managed by Docker | Uses a specific host path |
| Created using Docker commands or automatically | Uses an existing or specified host file or directory |
| Useful for persistent application data | Useful for sharing project files between host and container |

## 7. Important Points

1. Volumes help preserve data independently of a container's lifecycle.
2. Removing a container does not normally remove its named volumes.
3. A bind mount connects a host path to a container path.
4. Docker manages named volume storage.
5. Do not remove volumes containing important data.
6. A volume must be mounted at the path where the application expects to read or write data.

## Conclusion

Docker volumes provide persistent storage for containerized applications. They are particularly useful for databases and applications whose data must remain available even when containers are recreated.