# 02 — Docker Container Options 🐳

## 1. Image Tags and Versions

A Docker image can have different versions, identified using **tags**.

**Example:**

```bash
docker pull nginx:latest
docker pull nginx:alpine
```

- `nginx` is the image name.
- `latest` and `alpine` are tags identifying image variants.
- `latest` does not always mean the newest stable version; it is simply a tag.

To run a specific tag:

```bash
docker run nginx:alpine
```

## 2. Detached Mode (`-d`)

Detached mode runs a container in the background, allowing you to continue using the terminal.

```bash
docker run -d nginx
```

**Example:** Nginx runs in the background while you can type other commands in the same terminal.

To check running containers:

```bash
docker ps
```

A container stays running only while its main process continues running.

## 3. Environment Variables (`-e`)

Environment variables let you pass configuration values to a container when starting it.

```bash
docker run -d --name my-nginx -e MY_ENV=hello nginx
```

- `-e` sets an environment variable.
- `MY_ENV` is the variable name.
- `hello` is its value.

The application inside the container must read the variable for it to have an effect.

## 4. Custom Container Names (`--name`)

The `--name` option assigns a meaningful name to a container instead of relying on an automatically generated name.

```bash
docker run -d --name my-web nginx
```

Here, `my-web` is the container name.

You can use that name to manage the container:

```bash
docker stop my-web
docker start my-web
docker logs my-web
```

## Quick Revision

| Option | Purpose |
|---|---|
| `nginx:alpine` | Specifies an image tag |
| `-d` | Runs the container in the background |
| `-e` | Passes an environment variable |
| `--name` | Assigns a custom container name |

**Remember:** Tags identify image versions or variants, `-d` controls how the container runs in the terminal, `-e` passes configuration, and `--name` makes the container easier to identify.
