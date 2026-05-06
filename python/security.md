---
globs:
  - "**/*.py"
  - "**/*.pyi"
agent:
  - build
  - python-reviewer
match: all
---

# Python Security

- Secrets come from environment variables; fail fast if missing.
