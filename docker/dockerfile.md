---
globs:
  - "Dockerfile"
  - "**/Dockerfile"
---

# Dockerfile

- Use multi-stage builds with builder images so build tooling stays out of the runtime image.
- Keep each container to one concern; one main process is the default, with exceptions like init processes or well-understood worker models when they still serve that single concern.
- Order instructions for cache reuse: stable steps early, frequently changing steps late.
- Prefer `COPY` over `ADD`; use `ADD` only for intentional local tar auto-extraction, never for remote URLs.
- With `apt-get`, combine `update` and `install` in one `RUN`, then remove `/var/lib/apt/lists/*` in that same step.
