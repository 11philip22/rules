---
globs:
  - "Dockerfile"
  - "**/Dockerfile"
---

# Dockerfile

- Use builder images via multi-stage builds so build tooling stays out of the final runtime image.
- Each container should have one concern. Keep images focused on a single responsibility so services can be scaled, replaced, and reused independently.
- Treat one main process per container as the default, but not as an absolute rule; init processes and well-understood worker models are acceptable when they support the same single concern.
- Order Dockerfile instructions to make good use of the build cache. Put stable steps earlier and frequently changing steps later so rebuilds stay fast and cache invalidation is minimized.
- Prefer `COPY` over `ADD`. Use `ADD` only when you intentionally need local tar archive auto-extraction.
- Do not use `ADD` with remote URLs. Fetch remote artifacts explicitly and verify them as needed instead of relying on `ADD` URL handling.
- When using `apt-get`, combine `apt-get update` and `apt-get install` in the same `RUN` instruction so package indexes are fresh when packages are installed.
- In the same `RUN`, clean up package lists after installation, for example with `rm -rf /var/lib/apt/lists/*`, to reduce image size.
