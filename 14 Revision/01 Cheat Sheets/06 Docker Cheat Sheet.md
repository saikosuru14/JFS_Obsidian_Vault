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
order: 6
tags:
  - revision
  - docker
---

# Docker Cheat Sheet

> Interview-ready revision for [[Docker]] (4–5 YOE). Concepts, code, tables, and Q&A with answers.

---

## 1. Model
- **Image** = read-only layered filesystem template; **container** = image + a thin writable layer + isolated process (namespaces) with resource limits (cgroups). Shares the host **kernel** → lighter/faster than a VM.
- Each Dockerfile instruction = a cached layer keyed by instruction + context. Order **least → most frequently changing** to maximize cache reuse.

## 2. Efficient, Secure Image (Java multi-stage)
```dockerfile
# ---- build stage ----
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn -q dependency:go-offline        # cache deps: changes rarely
COPY src ./src
RUN mvn -q clean package -DskipTests

# ---- runtime stage ----
FROM eclipse-temurin:21-jre AS runtime  # or distroless/gcr.io/distroless/java21
WORKDIR /app
COPY --from=build /app/target/app.jar app.jar
RUN useradd -r app && chown app:app app.jar
USER app                                 # non-root
EXPOSE 8080
ENTRYPOINT ["java","-XX:MaxRAMPercentage=75","-jar","app.jar"]  # exec form → gets SIGTERM
```
- Copy dependency manifests before source so a code change doesn't bust the dependency layer.
- **Multi-stage** ships only the artifact (no Maven/JDK) → small, fewer CVEs. Prefer `-jre`/distroless base.
- `.dockerignore` shrinks build context; enable **BuildKit** for cache mounts + parallel stages.

## 3. Common Commands
```bash
docker build -t app:1.0 .
docker run -d -p 8080:8080 --memory=512m --cpus=1 --name app app:1.0
docker logs -f app ; docker exec -it app sh
docker compose up -d ; docker compose logs -f
docker system prune -af --volumes     # reclaim space
```

## 4. Runtime Gotchas (interview-relevant)
- **PID 1 / signals:** use **exec form** `ENTRYPOINT ["..."]` so the app is PID 1 and receives `SIGTERM` for graceful shutdown. Shell form (`ENTRYPOINT java -jar ...`) runs under `/bin/sh` and swallows signals. Add `--init` or `tini` if your process doesn't reap children.
- **ENTRYPOINT vs CMD:** ENTRYPOINT = the executable (fixed); CMD = default args (overridable at `docker run`).
- **JVM in containers:** modern JDKs honor cgroup limits; set `-XX:MaxRAMPercentage` instead of a fixed `-Xmx`.
- `HEALTHCHECK` for liveness. Don't store state in the container layer.

| Feature | Volume | Bind mount |
|---------|--------|-----------|
| Location | Docker-managed | host path |
| Portability | high | host-coupled |
| Use | prod data, DBs | local dev, config |

## 5. Networking
- Default **bridge**; user-defined bridge gives DNS by container name. `host` (no isolation), `none`. Compose creates a network where services resolve each other by service name.
- Publish ports `-p host:container`. Overlay networks for multi-host (Swarm).

## 6. Security
- Run as **non-root** (`USER`), read-only root FS where possible, drop Linux capabilities.
- Pin base image tags/digests; **scan** (Trivy/Grype); never bake secrets into layers (they persist in history even if later removed) — inject at runtime.

---

## 7. Interview Q&A (with answers)

**Q: Container vs VM?**
A: Containers virtualize the OS (share the host kernel, isolate via namespaces/cgroups) → seconds to start, MBs. VMs virtualize hardware with a full guest OS → heavier, stronger isolation.

**Q: Why multi-stage builds?**
A: Compile in a fat build image, then copy only the artifact into a slim runtime image. Result: small images, no build tools/secrets shipped, fewer vulnerabilities.

**Q: My layer cache never hits — why?**
A: You copy source before installing dependencies, or change an early instruction — every layer after a changed one is rebuilt. Copy dependency manifests and install deps first.

**Q: ENTRYPOINT vs CMD, and why does my app ignore SIGTERM?**
A: ENTRYPOINT is the fixed executable, CMD is default args. Shell-form ENTRYPOINT runs your app as a child of `/bin/sh`, which doesn't forward signals → use exec form so the app is PID 1 and shuts down gracefully.

**Q: How does the JVM see container memory?**
A: Modern JDKs are cgroup-aware and size the heap from the container limit; use `-XX:MaxRAMPercentage` rather than a fixed `-Xmx` so it adapts to the limit.

**Q: Volume vs bind mount?**
A: Volumes are Docker-managed and portable (use for persistent/prod data); bind mounts map a host path (use for local dev/config). Neither should live in the ephemeral container layer.

---

## Revision Checklist
- [ ] Image/container/layer + cache ordering
- [ ] Multi-stage + distroless + non-root
- [ ] ENTRYPOINT vs CMD + PID-1 signal handling
- [ ] Resource limits + JVM cgroup awareness
- [ ] Networking (bridge/DNS) + volumes vs bind mounts
- [ ] Image scanning + secrets handling
