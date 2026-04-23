---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Coding Style

- Follow **PEP 8** conventions.
- Use the repo's configured formatter and linter; if unspecified, prefer **black** and **ruff**.
- Within a package, prefer explicit relative imports for sibling modules and submodules.
- Use absolute imports for external packages and top-level package entry points.
