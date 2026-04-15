---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Patterns

## Data Modeling

- Use `@dataclass` for DTOs such as request payload types with typed fields and optional values.

## Resource And Iteration Patterns

- Use context managers (`with`) for resource management.
- Use generators for lazy evaluation and memory-efficient iteration.
