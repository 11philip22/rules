---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Patterns

## Readability

- Python prioritizes readability. Code should be obvious and easy to understand.

## Explicitness

- Avoid magic; be clear about what your code does.

## Type Hints

- Use type annotations on input parameters.
- Annotate return values explicitly.
- Prefer clear built-in generics and simple aliases when they improve readability.

## Context Managers

- Use `with` for files and other resources instead of manual cleanup.
- Use helper functions when scoped setup and teardown make the code clearer.

## Python Error Handling

- Catch specific exceptions; do not use bare `except`.
- Do not silently swallow failures.
- Raise actionable errors and preserve the cause with `raise ... from e` when useful.
- Prefer small, clear exception types when the codebase already uses them.
