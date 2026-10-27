# 08 — Docker Compose 🐳

## 1. What Is Docker Compose?

Docker Compose is a tool used to define and manage multi-container applications through a YAML file, usually named `compose.yaml` or `docker-compose.yml`.

Instead of starting every container manually, we define the services in one file and manage them using Compose commands.

**Example:** A web application might need two services:

- Frontend: displays the user interface.
- Database: stores application data.

Docker Compose lets us configure and run both services together.

## 2. What Is a YAML File?

YAML is a human-readable format used to write configuration files.

It uses indentation to organize data, so spacing matters.

Example:

```yaml
name: my-project
services:
  web:
    image: nginx
```

Here:
- `name` specifies the project name.
- `services` defines the application's services.
- `web` is the service name.
- `image` specifies which Docker image to use.

## 3. Example: Running Nginx Using Docker Compose

Create a file named `compose.yaml` with this content:

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

This configuration defines one service called `web`, uses the Nginx image, and maps host port `8080` to container port `80`.

### Start the application

```bash
docker compose up -d
```

Compose creates and starts the required container in the background.

Open `http://localhost:8080` in your browser to view the Nginx welcome page.

### Stop the application

```bash
docker compose down
```

This stops and removes the containers and networks created for the Compose project. It does not normally remove named volumes unless requested.

## 4. Example: Multiple Services

A Compose file can define multiple services. For example:

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"

  database:
    image: mongo
```

This defines two services: `web` and `database`.

**Note:** This is a basic configuration example. A real database-backed application may need environment variables, persistent storage, and application-specific configuration.

## 5. Important Docker Compose Commands

| Command | Purpose |
|---|---|
| `docker compose up` | Creates and starts services |
| `docker compose up -d` | Starts services in the background |
| `docker compose down` | Stops and removes project containers and networks |
| `docker compose ps` | Displays the project's container status |
| `docker compose logs` | Displays service logs |
| `docker compose logs -f` | Follows service logs |
| `docker compose build` | Builds or rebuilds configured images |

Run these commands from the directory containing the Compose file.

## 6. Docker Commands vs Docker Compose

| Docker CLI | Docker Compose |
|---|---|
| Often used to manage individual containers | Designed to manage applications with one or more services |
| Configuration can be supplied through command-line options | Configuration is written in a YAML file |
| Containers are often managed with separate commands | Multiple services can be started or stopped together |

## 7. Important Points

1. Docker Compose manages multi-container applications.
2. Compose configuration is written in YAML.
3. Each service describes a component of the application.
4. `docker compose up -d` starts the services in the background.
5. `docker compose down` removes project containers and networks.
6. Services on the same Compose network can generally communicate using their service names.
7. Compose makes application configuration easier to reuse.

## Conclusion

Docker Compose simplifies the management of multi-container applications by defining services and their configuration in a YAML file.
