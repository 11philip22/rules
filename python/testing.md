---
globs:
  - "**/*.py"
  - "**/*.pyi"
agent:
  - build
  - python-reviewer
match: all
---

# Python Testing

- When changing behavior, add or update the narrowest relevant test.
- Prefer deterministic tests over live network calls, real time, or external services when practical.
- Keep tests focused and readable; cover the behavior under change and relevant failure paths.
- Follow the repo's test framework, layout, fixtures, and marker conventions.
