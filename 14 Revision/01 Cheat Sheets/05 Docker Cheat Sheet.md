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

> Mid-level recall for [[Docker]] — image efficiency, security, and runtime gotchas.

## Model
- Image = read-only layered template; container = writable layer on top. Container shares host kernel (lighter than a VM).
- Each Dockerfile instruction = a cached layer. Order least→most frequently changing to maximize cache reuse.

## Efficient Images
- **Multi-stage build**: compile in a build stage, copy only the artifact into a slim runtime → small, no build tools shipped.
- Small/secure base: `alpine`, **distroless**, or `-jre`/`jlink` runtime for Java.
- Copy dependency manifests (`pom.xml`/`package.json`) and resolve deps *before* copying source → cache deps across code changes.
- `.dockerignore` to shrink build context; BuildKit for cache mounts + parallelism.

## Common Commands
```bash
docker build -t app:1.0 .
docker run -d -p 8080:8080 --memory=512m --cpus=1 --name app app:1.0
docker logs -f app; docker exec -it app sh
docker compose up -d; docker system prune -af
```

## Runtime Gotchas
- **PID 1 / signals**: use exec-form `ENTRYPOINT ["java","-jar","app.jar"]` so the process gets SIGTERM (graceful shutdown). Shell-form swallows signals.
- **JVM in containers**: modern JDKs honor cgroup limits; set `-XX:MaxRAMPercentage` rather than fixed `-Xmx`.
- `ENTRYPOINT` (fixed) vs `CMD` (default, overridable). `HEALTHCHECK` for liveness.
- Volumes (managed, portable) vs bind mounts (host path). Don't store state in the container layer.

## Security
- Run as non-root (`USER`), read-only FS where possible, drop capabilities.
- Scan images (Trivy/Grabber), pin base tags/digests, don't bake secrets into layers (they persist even if deleted later).

## Sharp Interview Answers
- Container vs VM; why multi-stage builds.
- Why isn't my layer cache hitting? (deps copied after source; changing early layers).
- ENTRYPOINT vs CMD; PID-1 signal handling.
- How the JVM sees container memory.

## Revision Checklist
- [ ] Layers + cache ordering
- [ ] Multi-stage + distroless
- [ ] Signals/PID 1 + graceful shutdown
- [ ] Resource limits + JVM cgroup awareness
- [ ] Non-root + image scanning
