---
globs:
  - "**/*.rs"
agent:
  - build
  - rust-reviewer
match: all
---

# Rust Testing

- When changing behavior, add or update the narrowest relevant test. If you cannot add coverage, call out the gap.
- Prefer deterministic tests over live network calls, real time, or external services when practical.
- Test public behavior and module boundaries rather than private implementation details.
- Use unit tests near the code and integration tests in `tests/` for cross-module behavior.
- Keep tests focused and fast; use synthetic data and temporary directories instead of machine-specific paths.
- Follow the repo's test setup; if unspecified, prefer `cargo test`.
