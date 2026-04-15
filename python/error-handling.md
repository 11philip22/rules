---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Error Handling

## Patterns

- Catch specific exceptions; do not use bare `except`.
- Do not silently swallow failures or return `None` from broad catches.
- Raise domain-specific errors with actionable messages.
- Chain exceptions with `raise ... from e` to preserve traceback.
- Prefer a small custom exception hierarchy rooted in one application base exception.

```python
import json


class AppError(Exception):
    pass


class ConfigError(AppError):
    pass


class NotFoundError(AppError):
    pass


def load_config(path: str) -> Config:
    try:
        with open(path) as f:
            return Config.from_json(f.read())
    except FileNotFoundError as e:
        raise ConfigError(f"Config file not found: {path}") from e
    except json.JSONDecodeError as e:
        raise ConfigError(f"Invalid JSON in config: {path}") from e


def get_user(user_id: str) -> User:
    user = db.find_user(user_id)
    if not user:
        raise NotFoundError(f"User not found: {user_id}")
    return user
```
