# 03 — Docker Image Layers 🐳

## 1. What Are Docker Image Layers?

A Docker image is made up of multiple layers. Each layer represents filesystem changes that contribute to the final image.

The base layer often comes from a base image such as Ubuntu, Alpine Linux, or Debian.

**Example Dockerfile:**

```dockerfile
FROM ubuntu
RUN apt update
RUN apt install -y nodejs
COPY . .
```

These instructions contribute to building the image. Filesystem-changing instructions commonly create image layers, although not every Dockerfile instruction creates a separate filesystem layer.

## 2. Read-Only Image Layers

- Image layers are read-only and immutable.
- When a container is created, Docker adds a writable container layer on top of the image.
- Changes made inside the container are stored in this writable layer.
- The original image layers remain unchanged.

**Example:** Imagine the image is an original printed notebook. When you run a container, it is like getting a temporary writable sheet on top. Your changes do not modify the original notebook.

## 3. Layer Sharing

Docker can reuse common image layers instead of storing or downloading duplicate copies of the same layers.

**Example:**

### Image A

```text
┌──────────────────────┐
│       App 1          │  ← Application layer
├──────────────────────┤
│       Node.js        │  ← Shared layer
├──────────────────────┤
│       Ubuntu         │  ← Shared base layer
└──────────────────────┘
```

### Image B

```text
┌──────────────────────┐
│       App 2          │  ← Application layer
├──────────────────────┤
│       Node.js        │  ← Shared layer
├──────────────────────┤
│       Ubuntu         │  ← Shared base layer
└──────────────────────┘
```

Here, both images use the same Ubuntu and Node.js layers, while their application layers are different.

Docker can reuse the common layers, helping save disk space and reduce repeated downloads.

**Benefits:**
- Saves disk space.
- Reduces repeated downloads.
- Can make image downloads and builds more efficient.

## 4. Important Points

1. An image is a read-only template.
2. A container has a writable layer on top of its image.
3. Multiple containers can be created from the same image.
4. Deleting a container does not automatically delete its image.
5. An image generally cannot be removed while existing containers still reference it.
6. Common image layers can be shared between images.
7. Removing a container removes its writable container layer; data stored in volumes can persist separately.
