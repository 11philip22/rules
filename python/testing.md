---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Testing

## Framework

- Use **pytest** as the testing framework.

## Coverage

- Run coverage with `pytest --cov=src --cov-report=term-missing`.

## Test Organization

- Use `pytest.mark` for test categorization.
- Prefer categories such as `@pytest.mark.unit` and `@pytest.mark.integration`.
