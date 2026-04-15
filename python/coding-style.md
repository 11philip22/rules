---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Coding Style

## Standards

- Follow **PEP 8** conventions.
- Use **type annotations** on all function signatures.

## Data Modeling

- Prefer immutable data structures such as `@dataclass(frozen=True)` and `NamedTuple`.

## Tooling

- Use **black** for code formatting.
- Use **isort** for import sorting.
- Use **ruff** for linting.
