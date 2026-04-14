---
globs:
  - "docker-compose.yml"
  - "**/docker-compose.yml"
---

# Docker Compose

- Order top-level definitions as `networks`, then `volumes`, then `services`.
- Within each service, keep definitions in this order when present: `image`, `hostname`, `restart`, `command`, `environment`, `ports`, `networks`, `volumes`, `depends_on`, `labels`, `healthcheck`, `logging`.
- Store credentials and other secrets in a `.env` file and reference them from `docker-compose.yml`; do not hardcode them directly in the compose file.
- When a service connects to something external to the compose stack, keep the connection details in `.env` as well, including stable identifiers such as hostnames, URLs, ports, database names, bucket names, or similar connection-target settings.
- When a service connects only to another service in the same compose stack, keep only the sensitive values in `.env`; stable internal service names, ports, and other non-secret connection-target settings may be hardcoded in `docker-compose.yml`.
- Each service must define `logging` using the `json-file` driver with `options.max-size` configured, for example:

```yaml
logging:
  driver: "json-file"
  options:
    max-size: "250m"
```
