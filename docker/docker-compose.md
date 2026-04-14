---
globs:
  - "docker-compose.yml"
  - "**/docker-compose.yml"
---

# Docker Compose

- Order top-level definitions as `networks`, then `volumes`, then `services`.
- Within each service, keep definitions in this order when present: `image`, `hostname`, `restart`, `command`, `environment`, `ports`, `networks`, `volumes`, `depends_on`, `labels`, `healthcheck`, `logging`.
- Each service must define `logging` using the `json-file` driver with `options.max-size` configured, for example:

```yaml
logging:
  driver: "json-file"
  options:
    max-size: "250m"
```
