---
globs:
  - "**/*.py"
  - "**/*.pyi"
agent:
  - build
  - python-reviewer
match: all
---

# Python Coding Style

- Follow **PEP 8** conventions.
- Use the repo's configured formatter and linter; if unspecified, prefer **black** and **ruff**.
- Within a package, prefer explicit relative imports for sibling modules and submodules.
- Use absolute imports for external packages and top-level package entry points.
- Keep imports at the top of Python project files; do not place imports inside `try`/`except` blocks unless the file is an `__init__.py` that intentionally gates optional imports.