---
globs:
  - "docker-compose.yml"
  - "**/docker-compose.yml"
---

# Docker Compose

- Top-level order: `networks`, `volumes`, `services`.
- Service key order when present: `image`, `hostname`, `restart`, `command`, `environment`, `ports`, `networks`, `volumes`, `depends_on`, `labels`, `healthcheck`, `logging`.
- Put secrets in `.env`, not inline in `docker-compose.yml`.
- For external dependencies, keep both secrets and connection-target settings in `.env` such as hostnames, URLs, ports, names, and similar stable identifiers.
- For dependencies inside the same compose stack, keep only secrets in `.env`; internal service names, ports, and other non-secret connection settings may be hardcoded.
- Every service must define `logging` as `driver: "json-file"` with `options.max-size` set, for example `"250m"`.
