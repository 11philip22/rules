---
globs:
  - "**/*.rs"
agent:
  - build
  - rust-reviewer
match: all
---

# Rust Patterns

## Architecture

- Encapsulate data access behind traits and keep storage details in concrete implementations such as Postgres, SQLite, or in-memory test adapters.
- Keep business logic in service structs and inject dependencies through constructors.
- Parse unstructured input into typed domain values at the boundary instead of passing loosely validated data inward.

## Type Design

- Use distinct wrapper types for IDs and similar values to prevent argument mix-ups at call sites.
- Model important states as enums so illegal states are hard to represent.
- Match exhaustively; avoid wildcard `_` arms for business-critical enums.
- Use builders for types with many optional parameters or sensible defaults.

## Traits And Generics

- Accept generic inputs when it improves flexibility; return concrete types unless dynamic dispatch is required.
- Use trait objects for heterogeneous collections or plugin boundaries; prefer generics when static dispatch is sufficient.
- Use sealed traits when external implementations must be prevented while preserving an internal extension point.

## API Boundaries

- Use a generic response envelope for consistent API responses.
