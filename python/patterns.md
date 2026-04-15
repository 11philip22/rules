---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Patterns

## Readability

- Python prioritizes readability. Code should be obvious and easy to understand.

```python
# Good: Clear and readable
def get_active_users(users: list[User]) -> list[User]:
    """Return only active users from the provided list."""
    return [user for user in users if user.is_active]


# Bad: Clever but confusing
def get_active_users(u):
    return [x for x in u if x.a]
```

## Explicitness

- Avoid magic; be clear about what your code does.

```python
# Good: Explicit configuration
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)

# Bad: Hidden side effects
import some_module
some_module.setup()  # What does this do?
```

## Type Hints

- Use type annotations on input parameters.
- Annotate return values explicitly.
- Prefer clear modern built-in generics when the project's Python version supports them.
- Use type aliases and `TypeVar` when they make repeated or generic types easier to read.

## Comprehensions And Generators

- Use list comprehensions for simple transformations and filters.
- Expand complex comprehensions into loops or helper functions.
- Prefer generator expressions over building large intermediate lists for reducers such as `sum(...)`.
- Use generator functions to stream large inputs lazily.

```python
from collections.abc import Iterable, Iterator


names = [user.name for user in users if user.is_active]
total = sum(x * x for x in range(1_000_000))


def filter_and_transform(items: Iterable[int]) -> list[int]:
    result = []
    for item in items:
        if item > 0 and item % 2 == 0:
            result.append(item * 2)
    return result


def read_large_file(path: str) -> Iterator[str]:
    with open(path) as f:
        for line in f:
            yield line.strip()
```

## Data Modeling

- Use `@dataclass` for DTOs and entities with typed fields.
- Use `field(default_factory=...)` for dynamic defaults.
- Use `__post_init__` for validation and invariants.
- Prefer immutable data structures when they fit, such as `@dataclass(frozen=True)` and `NamedTuple`.
- Use `NamedTuple` for small immutable records.

```python
from dataclasses import dataclass, field
from datetime import datetime
from typing import NamedTuple


@dataclass
class User:
    email: str
    created_at: datetime = field(default_factory=datetime.now)

    def __post_init__(self):
        if "@" not in self.email:
            raise ValueError(f"Invalid email: {self.email}")


class Point(NamedTuple):
    x: float
    y: float
```

## Error Handling

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

## Context Managers

- Use `with` for files and other resources instead of manual cleanup.
- Use `@contextmanager` for small scoped helpers.
- Use class-based context managers for stateful setup and teardown such as transactions.
- Return `False` from `__exit__` unless suppressing exceptions is intentional.

```python
import time
from contextlib import contextmanager


def process_file(path: str) -> str:
    with open(path) as f:
        return f.read()


@contextmanager
def timer(name: str):
    start = time.perf_counter()
    yield
    print(f"{name} took {time.perf_counter() - start:.4f} seconds")


class DatabaseTransaction:
    def __init__(self, connection):
        self.connection = connection

    def __enter__(self):
        self.connection.begin_transaction()
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        if exc_type is None:
            self.connection.commit()
        else:
            self.connection.rollback()
        return False
```

## Decorators

- Use decorators for cross-cutting concerns such as timing, retries, caching, or registration.
- Preserve wrapped metadata with `functools.wraps`.
- Use parameterized decorators when configuration is part of the API.
- Use class-based decorators only when they need state.

```python
import functools
from collections.abc import Callable


def repeat(times: int):
    def decorator(func: Callable) -> Callable:
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            return [func(*args, **kwargs) for _ in range(times)]
        return wrapper
    return decorator


class CountCalls:
    def __init__(self, func: Callable):
        functools.update_wrapper(self, func)
        self.func = func
        self.count = 0
```

## Concurrency

- Use `ThreadPoolExecutor` for I/O-bound work.
- Use `ProcessPoolExecutor` for CPU-bound work.
- Keep process-pool workers serializable and light on shared state.
- Handle per-task failures explicitly.

```python
import concurrent.futures


def fetch_all_urls(urls: list[str]) -> dict[str, str]:
    with concurrent.futures.ThreadPoolExecutor(max_workers=10) as executor:
        futures = {executor.submit(fetch_url, url): url for url in urls}
        results = {}
        for future, url in futures.items():
            try:
                results[url] = future.result()
            except Exception as e:
                results[url] = f"Error: {e}"
        return results


def process_all(datasets: list[list[int]]) -> list[int]:
    with concurrent.futures.ProcessPoolExecutor() as executor:
        return list(executor.map(process_data, datasets))
```

## Memory And Performance

- Use `__slots__` for many small mutable objects when the attribute set is fixed and memory matters.
- Stream large inputs with generators instead of building full lists in memory.
- Avoid repeated string concatenation in loops; prefer `"".join(...)` or `StringIO`.

```python
from collections.abc import Iterator
from io import StringIO


class Point:
    __slots__ = ["x", "y"]

    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y


def read_lines(path: str) -> Iterator[str]:
    with open(path) as f:
        for line in f:
            yield line.strip()


result = "".join(str(item) for item in items)

buffer = StringIO()
for item in items:
    buffer.write(str(item))
result = buffer.getvalue()
```
