---
title: Docker Cheat Sheet
aliases:
  - Docker Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Easy
priority: Medium
interview: 4
revision: Weekly
order: 5
tags:
  - revision
  - docker
---

# Docker Cheat Sheet

> Fast recall for [[Docker]]. See the [[Docker Index|Docker domain]] for depth.

## Concepts
- Image = read-only layered template; container = running instance.
- Layers are cached; order Dockerfile from least- to most-frequently changing.
- Container vs VM: containers share the host kernel (lighter, faster).

## Common Commands
```
docker build -t app:1.0 .
docker run -d -p 8080:8080 --name app app:1.0
docker ps / logs / exec -it app sh
docker images / rmi / system prune
docker compose up -d
```

## Dockerfile Essentials
- `FROM`, `WORKDIR`, `COPY`, `RUN`, `EXPOSE`, `ENV`, `ENTRYPOINT` vs `CMD`.
- Multi-stage build: compile in a build stage, copy only artifacts into a slim runtime image.
- `.dockerignore` to shrink build context.

## Storage & Networking
- Volumes (managed, persistent) vs bind mounts (host path).
- Bridge network (default), host, none; Compose creates a shared network by service name.

## Best Practices
- Small base images (alpine/distroless), pin versions, run as non-root, one process per container.
- Combine `RUN` layers; leverage build cache.

## Top Interview One-Liners
- `ENTRYPOINT` (fixed) vs `CMD` (default args, overridable).
- Why multi-stage? Small final image, no build tools shipped.
- Volume vs bind mount: portability vs direct host access.

## Revision Checklist
- [ ] Image vs container vs layer
- [ ] Dockerfile instructions
- [ ] Multi-stage builds
- [ ] Volumes vs bind mounts
- [ ] Networking modes
