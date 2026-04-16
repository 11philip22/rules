---
globs:
  - "**/*.rs"
---

# Rust Security

## Secrets

- Never hardcode API keys, tokens, or credentials.
- Read secrets from environment variables such as `std::env::var("API_KEY")`.
- Fail fast if required secrets are missing at startup.
- Keep `.env` files in `.gitignore`.

## SQL Injection

- Always use parameterized queries; never format user input into SQL strings.
- Prefer query builders or ORMs such as `sqlx`, `diesel`, or `sea-orm` with bind parameters.

## Input Validation

- Validate user input at system boundaries before processing.
- Use the type system to enforce invariants, including newtypes where they help.
- Parse, do not validate: convert unstructured input into typed values at the boundary.
- Reject invalid input with clear error messages.

## Unsafe Code

- Minimize `unsafe`; prefer safe abstractions.
- Every `unsafe` block must have a `// SAFETY:` comment explaining the invariant.
- Never use `unsafe` to bypass the borrow checker for convenience.
- Audit all `unsafe` code during review and justify it clearly.
- Prefer safe FFI wrappers around C libraries.

## Dependencies

- Run `cargo audit` for known dependency advisories.
- Run `cargo deny check` for advisory and license compliance.
- Use `cargo tree` to inspect transitive dependencies and duplicates.
- Keep dependencies updated with tooling such as Dependabot or Renovate.
- Minimize dependency count and evaluate new crates before adding them.

## Error Messages

- Never expose internal paths, stack traces, or raw database errors in API responses.
- Log detailed errors server-side and return generic messages to clients.
- Use structured logging with `tracing` or `log`.
