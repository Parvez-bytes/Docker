# 10 — Docker Hub 🐳

## 1. What is Docker Hub?

Docker Hub is an online platform used to store, share, and download Docker images.

**Example:** If we build an image on our laptop, we can upload it to Docker Hub and download it on another computer.

## 2. Steps to Push an Image to Docker Hub

### Step 1: Login to Docker Hub

```bash
docker login
```

Logs in to Docker Hub using your credentials. Follow the prompts to authenticate.

### Step 2: Build the Docker Image

```bash
docker build -t my-web-app .
```

- `docker build` builds an image using a Dockerfile.
- `-t my-web-app` gives the image a name.
- `.` tells Docker to use the current directory as the build context.

### Step 3: Tag the Image

```bash
docker tag my-web-app YOUR_DOCKERHUB_USERNAME/my-web-app:v1.0
```

Replace `YOUR_DOCKERHUB_USERNAME` with your Docker Hub username.

**Image naming format:**

`username/repository-name:tag`

- `username` — your Docker Hub username
- `repository-name` — the image repository name
- `v1.0` — the version tag

### Step 4: Push the Image

```bash
docker push YOUR_DOCKERHUB_USERNAME/my-web-app:v1.0
```

Uploads the tagged image to Docker Hub. The repository may be created automatically during the push if your account and permissions allow it; otherwise, create it on Docker Hub first.

### Step 5: Pull the Image

```bash
docker pull YOUR_DOCKERHUB_USERNAME/my-web-app:v1.0
```

Downloads the image from Docker Hub to another computer.

### Step 6: Run the Image

```bash
docker run YOUR_DOCKERHUB_USERNAME/my-web-app:v1.0
```

Creates and starts a container from the downloaded image. If the application needs a port mapping or environment variables, provide them when running the container.

## 3. Complete Workflow

**Build → Tag → Push → Pull → Run**

## 4. Important Points

1. Docker Hub is used to store and share Docker images.
2. `docker login` authenticates with Docker Hub.
3. `docker tag` assigns a repository name and version to an image.
4. `docker push` uploads an image.
5. `docker pull` downloads an image.
6. `docker run` creates and starts a container from an image.
7. Docker must be installed on the computer that will run the container.

## Conclusion

Docker Hub makes it easier to share Docker images and run applications on different computers without manually installing the application's runtime and dependencies separately. Docker itself must still be installed.