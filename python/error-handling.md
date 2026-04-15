---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Error Handling

- Catch specific exceptions; do not use bare `except`.
- Do not silently swallow failures.
- Raise actionable errors and preserve the cause with `raise ... from e` when useful.
- Prefer small, clear exception types when the codebase already uses them.
