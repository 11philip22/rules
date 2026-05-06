---
globs:
  - "**/*.py"
  - "**/*.pyi"
keywords:
  - "generator"
  - "comprehension"
  - "iterator"
  - "stream"
agent:
  - build
  - python-reviewer
match: all
---

# Python Comprehensions And Generators

## Patterns

- Use list comprehensions for simple transformations and filters.
- Expand complex comprehensions into loops or helper functions.
- Prefer generator expressions over building large intermediate lists for reducers such as `sum(...)`.
- Use generator functions to stream large inputs lazily.
